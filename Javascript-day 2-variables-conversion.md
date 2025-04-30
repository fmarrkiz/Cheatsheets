Day 2

# Variables dans JVS

*let* s'éxécute sur le bloc courant

règles de nommage
const MAJUSCULE // pour les constantes dont la valeur est connue avant exécution et directement écrite dans le code
const minuscule // pour les constantes évaluées en exécution


## Questions

const pageLoadTime =
La valeur de pageLoadTime n'est pas connu avant le chargement de la page mais ça reste une constante car elle ne change pas après l'affectation.


### Exercices

1. why is name crossed?

# Les types de données

### Types primitifs

- Number : 

 	- nombre entier et nombre décimaux

Le type “number” peut stocker des entiers plus grands (jusqu’à 1.7976931348623157 * 10308), mais en dehors de la plage d’entiers sûrs ±(2 53-1) il y aura une erreur de précision, car tous les chiffres ne rentrent pas dans le stockage 64 bits fixe. Ainsi, une valeur “approximative” peut être stockée. 

- valeur numérique spéciale 

ex: Infinity (l'infini mathématique)

nombreuses opérations possibles pour les nombres : multiplication *, division /, addition +, soustraction -, ...

ex: NaN (erreur de calcul)

- BigInt 
 
 a été rajouté pour représenter des entiers de longeurs arbitraires

utilise plus d'octets que les valeurs numérique spéciales

- String (ou chaîne de caractères)

Une chaîne de caractères en JavaScript doit être entre guillemets.

let str = "Hello";
let str2 = 'Single quotes are ok too';
let phrase = `can embed another ${str}`;

En JavaScript, il existe 3 types de guillemets.

    Double quotes: "Hello".
    Single quotes: 'Hello'.
    Backticks: `Hello`.

Les guillemets simples et doubles sont des guillemets “simples”. Il n’y a pratiquement pas de différence entre eux en JavaScript.

Les backticks sont des guillemets “à fonctionnalité étendue”. Ils nous permettent d’intégrer des variables et des expressions dans une chaîne en les encapsulant dans ${…}, par exemple :

let name = "John";

// une variable encapsulée
alert( `Hello, ${name}!` ); // Hello, John!

// une expression encapsulée
alert( `the result is ${1 + 2}` ); // le résultat est 3

et pas 

alert( "the result is ${1 + 2}" ); // le résultat est ${1 + 2} (les doubles quotes ne font rien)

- Boolean (type logique)

 le type booléen n'a que deux valeurs: **true** et **false**
Ce type est couramment utilisé pour stocker des valeurs oui/non


- la valeur "null"

En JavaScript, null n’est pas une “référence à un objet non existant” ou un “pointeur nul” comme dans d’autres langages.

C’est juste une valeur spéciale qui a le sens de “rien”, “vide” ou “valeur inconnue”.

Le code ci-dessous indique que l’age est inconnu.

let age = null;

- la valeur "undefined"

La valeur spéciale undefined se distingue des autres. C’est un type à part entière, comme null.

La signification de undefined est “la valeur n’est pas attribuée”.

Normalement, nous utilisons null pour assigner une valeur “vide” ou “inconnue” à une variable, tandis que undefined est réservé comme valeur initiale par défaut pour les éléments non attribués.

- symbol

pour les identifiants uniques

### Type de données qui servent à stocker des collections de données et des entités plus complexes - données non primitives

- **object**



### Autres

- typeof 

l'opérateur *typeof* renvoie le type de l'opérande. Il est utile lorsqu'on souhaite traiter différemment les valeurs de différents types ou de faire une vérification rapide.

#### ***Attention***

- le résultat de `typeof null` est "object", c'est une erreur reconnue dans typeof

- le résultat de `typeof alert` est "function", car `alert` est une fonction. MAIS, il n'y a pas de type "fonction" en JavaScript. Les fonctions appartiennent au type `object` mais `typeof` les traite différemment en retournant "function". Ça vient des débuts de Javascript et c'est pratique à l'usage.

`typeof (x)` est la même chose que `typeof x`

même si `typeof` est un opérateur pas une fonction!


# Les conversions  de types


`alert` convertit automatiquement toute valeur en chaîne de caractères pour l'afficher.

### String conversion

let value = true;
alert(typeof value); // boolean

value = String(value); // maintenant la valeur est une chaîne de caractères "true"
alert(typeof value); // string

Un `false` devient `"false"`, `null` devient `"null"` etc.

### Numeric Conversion

La conversion numérique dans les fonctions et expressions mathématiques s'effectue automatiquement.

ex : alert("6"/ "2"); // 3, les chaînes de caractères sont converties en nombres

 
### Boolean Conversion




