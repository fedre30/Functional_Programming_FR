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





### L'immutabilité

### La transparence réferentielle

[](https://cdn-images-1.medium.com/max/1600/1*Drz5Lwh2WtLcZdrxXg7JTQ.gif)

### Le "garbage collection" 

## L'observable

### Définition

### Redux : un exemple d'observable

### Réferences

- [Functional programming principles in Javascript](https://medium.freecodecamp.org/functional-programming-principles-in-javascript-1b8fc6c3563f)
- [An intro to Functional Programming in JavaScript and React](https://medium.com/@agm1984/an-overview-of-functional-programming-in-javascript-and-react-part-one-10d75b509e9e)
- [Javascript Allongé](https://leanpub.com/javascriptallongesix/read)
- [The Observer pattern in Javascript](http://www.thedevnotebook.com/2017/08/the-observer-pattern-in-javascript.html)
