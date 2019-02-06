# La programmation fonctionnelle et le patron de conception Observable  (FR)
Documentation sur la programmation fonctionnelle et l'Observable en Javascript

## Définition
>La **programmation fonctionnelle** est un paradigme de programmation de type déclaratif qui considère le calcul en tant qu'évaluation de fonctions mathématiques.

>Comme le **changement d'état** et la **mutation des données** ne peuvent pas être représentés par des évaluations de fonctions, la programmation fonctionnelle ne les admet pas, au contraire elle met en avant l'application des fonctions, contrairement au modèle de programmation impérative qui met en avant les changements d'état.

### Programmation fonctionnelle vs Programmation impérative

La **programmation fonctionnelle** a été crée pour avoir une approche fonctionnelle pure dans la résolutions des problèmes, ce qui la rend une forme de *programmation déclarative*.

Alors que la **programmation impérative** a le but de décrire à la machine toutes les étapes pour pourvoir atteindre un certain résultat, ce qui est typique de toute *programmation algorighmique*.

Voici un tableau qui résume les différences des deux approches face au même élement.

| Proprieté     | Approche impérative | Approche fonctionnelle  |
| ------------- |:-------------------:| -----------------------:|
| L'objectif du programmeur      | Comment executer les tâches (algorithmes) et comment suivre les changement d'état       | Savoir l'information dont on a besoin et les transformations requises qu'il faut appliquer                   |
| Changement d'état | Important            |    Inéxistant                   |
| L'ordre d'execution     | Important           |   Peu important                  |
| Fonctionnalités principales utilisées pour le flux de données  | Boucles, conditionnels et appels de fonctions (méthodes)            |    Appels de fonctions dont des fonctions recursives                   |
| Premier choix pour la manipulation de toute entité | Les instances des structures ou des classes            |    Les fonctions qui sont utilisées comme des objets de première catégorie et les collections de données                   |


## Concepts de base

### Les fonctions pures 

Une fonction pure est une fonction qui a comme résultat une valeur qui est l'ensemble de tous les paramètres qui sont passées à la fonction, autrement dit le nombre de paramètres et des valeurs qui composent le résultat doit être le même.

Exemple de **fonction impure**:

```
const PI = 3.14;

function calculateArea(radius) {
  return radius * radius * PI;
}

calculateArea(10); // returns 314.0
```

Le résultat est le produit du radius et du PI grec, or le PI grec n'est pas un paramètre, mais un élement externe à la fonction, ce qui rend cette fonction impure car elle n'est pas suffisante d'elle-même.

Voici le même exemple mais cette fois-ci avec une **fonction pure**

```const PI = 3.14;

function calculateArea(radius, pi) {
  return radius * radius * pi;
}

calculateArea(10, PI); // returns 314.0
```

PI est maintenant un paramètre, donc le nombre de valeurs qui composent le résultat et le nombre de paramètre est bien le même.


### Les fonctions de premier ordre

Les fonctions de premier ordre sont des fonctions qui peuvent:

- prendre une ou plusieurs fonctions comme paramètre
- avoir une fonction comme résultat

Les fonctions introduites en ES6 **Map**, **Filter** et **Reduce** sont des bons exemples de fonctions de premier ordre.

#### Map

Approche impérative:

```
const people = [
  { name: "TK", age: 26 },
  { name: "Kaio", age: 10 },
  { name: "Kazumi", age: 30 }
];

let peopleSentences = [];

for (let i = 0; i < people.length; i++) {
  var sentence = people[i].name + " is " + people[i].age + " years old";
  peopleSentences.push(sentence);
}

console.log(peopleSentences); // ['TK is 26 years old', 'Kaio is 10 years old', 'Kazumi is 30 years old']
```


Approche déclarative ou fonctionnelle où la fonction even est le paramètre de la fonction de premier ordre **map**:

```
function makeSentence(person) {
  return `${person.name} is ${person.age} years old`;
}

function peopleSentences(people) {
  return people.map(makeSentence);
}

peopleSentences(people); // ['TK is 26 years old', 'Kaio is 10 years old', 'Kazumi is 30 years old']
view raw
```


#### Filter

Approche impérative:

```
const numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let evenNumbers = [];

for (let i = 0; i < numbers.length; i++) {
  if (numbers[i] % 2 == 0) {
    evenNumbers.push(numbers[i]);
  }
}

console.log(evenNumbers); // (6) [0, 2, 4, 6, 8, 10]
```


Approche déclarative ou fonctionnelle où la fonction even est le paramètre de la fonction de premier ordre **filter**:

```
function even(number) {
  return number % 2 == 0;
}

let listOfNumbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
listOfNumbers.filter(even); // [0, 2, 4, 6, 8, 10]

```

#### Reduce

Approche impérative:

```

const orders = [
  { productTitle: "Product 1", amount: 10 },
  { productTitle: "Product 2", amount: 30 },
  { productTitle: "Product 3", amount: 20 },
  { productTitle: "Product 4", amount: 60 }
];

let totalAmount = 0;

for (let i = 0; i < orders.length; i++) {
  totalAmount += orders[i].amount;
}

console.log(totalAmount); // 120
```


Approche déclarative ou fonctionnelle où la fonction even est le paramètre de la fonction de premier ordre **reduce**:

```

let shoppingCart = [
  { productTitle: "Product 1", amount: 10 },
  { productTitle: "Product 2", amount: 30 },
  { productTitle: "Product 3", amount: 20 },
  { productTitle: "Product 4", amount: 60 }
];

const sumAmount = (currentTotalAmount, order) => currentTotalAmount + order.amount;

function getTotalAmount(shoppingCart) {
  return shoppingCart.reduce(sumAmount, 0);
}

getTotalAmount(shoppingCart); // 120

```

### Flux de données

La programmation fonctionnelle reactive traite les données d'un façon très formalisée, presque mathématique.
On peut resumer cela en deux expressions, à savoir:
- "On écoute un évenement, on déclenche une action"
- "Une action est déjà en cours, on la rédirige vers quelque chose"

Autrement dit la programmation fonctionnelle consiste à recuperer des données ou à les manipuler mais étape par étape, de façon systémique.
Ainsi tout élement dans la programmation fonctionnelle a un contexte *temporel* et *local*.

Ceci est important à retenir parce que le flux de données va des deux sens: serveur -> client et client -> serveur, mais pas sur le même canal.

Il faut imaginer les données comme un ensembles hydrique composés par diférrents tubes (*sinks*).
Chaque tube est unidirectionnel car le fluide peut suivre une seule direction, mais dans un autre tube connecté, le fluide suit la direction opposée.


### L'immutabilité

Le but de la programmation fonctionnelle est de rendre l'état (*State*) immuable une fois qu'il a été crée, ainsi si on veut changer des données il faut créer un objet avec les nouvelles valeurs.
Par exemple, la fonction **map** permet d'itérer sur un tableau en créant une nouvelle instance du tableau, autrement dit le tableau initiale ne peut pas être changé.
En général, la recursion permet de garder les variables immuables et intouchables. 

Ainsi les données ne sont jamais modifiées directement, mais on modifie l'instance ou la réference de la données (voir prochain chapitre *La transparence réferentielle*).


### La transparence réferentielle

En Javascript, tout est un objet, même les fonctions sont des objets.
Mais le fonctions sont des *citoyens de première classe*, c'est-à-dire que Javascript execute à partir de la première ligne jusqu'à la dernière en essayant d'executer toutes les fonctions le plus vite possible.
Nénanmoins, chaque fonction est executée une à la fois en suivant un certain ordre (voir chapitre *Flux de données*).
Pour une question de praticité, il vaut mieux de voir les fonctions comme des containeurs où se passe tout parce qu'ils sont un début et une fin, autrement dit elles sont *unidirectionnelles* (comme le tube qu'on a évoqué auparavant).

![](https://cdn-images-1.medium.com/max/1600/1*Drz5Lwh2WtLcZdrxXg7JTQ.gif)

### Le "garbage collection" 

## L'observable

### Redux: un exemple d'Observable

## La programmation fonctionnelle réactive

### Cycle.js

Cycle.js est un framework fondé sur la [**programmation reactive**](https://gist.github.com/staltz/868e7e9bc2a7b8c1f754) et crée par André Staltz.

[Documentation officielle](https://cycle.js.org)

[Bon Tutoriel](https://egghead.io/courses/cycle-js-fundamentals)

Exemple:

```

// FUNCTION MAIN TO INITIALIZE
function main() {
  return {
    DOM:  xs.periodic(1000)
      .fold(prev => prev + 1, 0)
      .map(i => `Seconds elapsed: ${i}`),

    log: xs.periodic(2000)
      .fold(prev => prev + 1, 0)
  }


}

// DRIVERS

function domDriver(text$) {
  text$.subscribe({
    next: str => {
      const el = document.querySelector('#app');
      el.textContent = str;
    }
  })
}

function logDriver(msg$) {
  msg$.subscribe({
    next: msg => {
      console.log(msg)}
  })
}

// CONNECTION TO MAIN

const sink = main();
domDriver(sink);
logDriver(sink);

```



## Réferences

- [Functional programming principles in Javascript](https://medium.freecodecamp.org/functional-programming-principles-in-javascript-1b8fc6c3563f)
- [An intro to Functional Programming in JavaScript and React](https://medium.com/@agm1984/an-overview-of-functional-programming-in-javascript-and-react-part-one-10d75b509e9e)
- [Javascript Allongé](https://leanpub.com/javascriptallongesix/read)
- [The Observer pattern in Javascript](http://www.thedevnotebook.com/2017/08/the-observer-pattern-in-javascript.html)
