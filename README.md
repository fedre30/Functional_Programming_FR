# La programmation fonctionnelle et le patron de conception Observable  (FR)
Documentation sur la programmation fonctionnelle et l'Observable en Javascript

## Définition
>La **programmation fonctionnelle** est un paradigme de programmation de type déclaratif qui considère le calcul en tant qu'évaluation de fonctions mathématiques.

>Comme le **changement d'état** et la **mutation des données** ne peuvent pas être représentés par des évaluations de fonctions, la programmation fonctionnelle ne les admet pas, au contraire elle met en avant l'application des fonctions, contrairement au modèle de programmation impérative qui met en avant les changements d'état.

### Programmation fonctionnelle vs Programmation impérative

La **programmation fonctionnelle** a été crée pour avoir une approche fonctionnelle pure dans la résolutions des problèmes, ce qui la rend une forme de *programmation déclarative*.

Alors que la **programmation impérative** a le but de décrire à la machine toutes les étapes pour pourvoir atteindre un certain résultat, ce qui est typique de toute *programmation algorighmique*.

Voici un tableau qui résume les ddiférences des deux approches face au même élement.

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


### Les fonctions de premier niveau

### Flux de données

### L'immutabilité

### La transparence réferentielle

### Le "garbage collection" 

## L'observable

### Définition

### Redux : un exemple d'observable
