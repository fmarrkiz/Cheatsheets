Day 2

# Variables dans JVS 
[lien](https://fr.javascript.info/variables)

Une variable est un “stockage nommé” pour les données. Nous pouvons utiliser des variables pour stocker des goodies, des visiteurs et d’autres données.<br> Cela peut être fait en utilisant `var` (old school), `let` (modern use) ou `const` (pour des variables dont la valeur ne peut pas être modifiée)

`let` s'exécute sur le bloc courant

Règles de nommage pour `const` :<br>
- `const MAJUSCULE` = pour les constantes dont la valeur est connue avant exécution et directement écrite dans le code
- `const minuscule` = pour les constantes évaluées en exécution


#### Questions (answered)

`const pageLoadTime` =
La valeur de pageLoadTime n'est pas connu avant le chargement de la page mais ça reste une constante car elle ne change pas après l'affectation.


# Les types de données
[lien](https://fr.javascript.info/types)

### 7 Types primitifs

1.  ***Number***

- **nombre entier et nombre décimaux**

  ex: `42`,`3.14`,`-0`
 
   Le type “number” peut stocker des entiers plus grands (jusqu’à 1.7976931348623157 * 10308), mais en dehors de la plage d’entiers sûrs ±(2 53-1) il y aura une erreur de précision, car tous les chiffres ne rentrent pas dans le stockage 64 bits fixe. Ainsi, une valeur “approximative” peut être stockée. <br>
- **valeur numérique spéciale**


    - ex: Infinity (l'infini mathématique)<br> Nombreuses opérations possibles pour les nombres : multiplication *, division /, addition +, soustraction -, ...

    - ex: `NaN` (= Not-a-Number ou erreur de calcul)

2. ***BigInt*** (ES2020+)
 
A été rajouté pour représenter des entiers plus long que `Number.MAX_SAFE_INTERGER`

Utilise plus d'octets que les valeurs numérique spéciales

  ex : `1234567890123456789012345678901234567890n`

3. String (ou chaîne de caractères)

Une chaîne de caractères (ou textual data) en JavaScript doit être entre guillemets.

let str = "Hello";
let str2 = 'Single quotes are ok too';
let phrase = `can embed another ${str}`;

En JavaScript, il existe 3 types de guillemets.

    Double quotes: "Hello".
    Single quotes: 'Hello'.
    **Backticks**: `Hello`.

Les guillemets simples et doubles sont des guillemets “simples”. Il n’y a pratiquement pas de différence entre eux en JavaScript.

Les backticks sont des guillemets “à fonctionnalité étendue”. Ils nous permettent d’intégrer des variables et des expressions dans une chaîne en les encapsulant dans ${…}, par exemple :

```javascript
let name = "John";

// une variable encapsulée
alert( `Hello, ${name}!` ); // Hello, John!

// une expression encapsulée
alert( `the result is ${1 + 2}` ); // le résultat est 3

et pas 

alert( "the result is ${1 + 2}" ); // le résultat est ${1 + 2} (les doubles quotes ne font rien)
```


4. ***Boolean*** (type logique)

 Le type booléen n'a que deux valeurs logique: `true` et `false`
Ce type est couramment utilisé pour stocker des valeurs oui/non


5.  ***La valeur `null`***

En JavaScript, null n’est pas une “référence à un objet non existant” ou un “pointeur nul” comme dans d’autres langages.

C’est juste une valeur spéciale qui a le sens intentionnel de “rien”, “vide” ou “valeur inconnue”.

Le code ci-dessous indique que l’age est inconnu.

```javascript
let age = null;

let y = null;
```

6.  ***La valeur `undefined`***

La valeur spéciale undefined se distingue des autres. C’est un type à part entière, comme `null`.

La signification de undefined est “la valeur n’est pas attribuée”. <br>
i.e the value is declared but not initialised

Normalement, nous utilisons `null` pour assigner une valeur “vide” ou “inconnue” à une variable, tandis que `undefined` est réservé comme valeur initiale par défaut pour les éléments non attribués.

 
```javascript
let x; // x is undefined
```



7. ***Symbol*** (ES6)

pour les identifiants uniques, often used as property keys

```javascript
let sym = Symbol('id');
```





### Non-primitive ou reference types

***Object***

Type de données qui servent à stocker des collections de données et des entités plus complexes - données non primitives

```javascript
const person = { name: "Alice", age: 25};
```

Il y a plusieurs types d'object : <!--(à retravailler)-->

- *array* (list-like object)
```javascript
const numbers = [1,2,3,4];
```

- *function* (considéré first-class objects)

Functions can be assigned to variables, passed as arguments, and returned from other functions.

```javascript
function greet(name) {
return "Hello," + name;
}
```

- *Date*

Représente un moment spécifique dans le temps

```javascript
const currentDate = new Date();
```

- *RegExp* (Regular Expression)

Used for matching strings against patterns, often for pattern matching and string manipulation.

```javascript
const pattern = /abc/;
```

- *Map*

A collection of key-value pairs where keys can be of any type (including objects), unlike regular JavaScript objects.
```javascript
    const map = new Map();
    map.set("name", "Alice");
    map.set("age", 25);
```

- *Set*

    A collection of unique values. It automatically removes duplicates.

```javascript
const set = new Set([1, 2, 3, 3, 4]);
console.log(set); // Set { 1, 2, 3, 4 }
```


Résumé sur *non-primitive types* :
- Mutable: Their content can be changed after they are created.

- Stored by Reference: Instead of storing the actual data, they store a reference to the data in memory.

- Can have properties and methods: They can have methods attached to them (like push() for arrays or get() for maps).


### Autres


- ***L'opérateur `typeof`***

L'opérateur `typeof` renvoie le type de l'opérande. Il est utile lorsqu'on souhaite traiter différemment les valeurs de différents types ou de faire une vérification rapide.

```javascript
typeof undefined // "undefined"

typeof 0 // "number"

typeof 10n // "bigint"

typeof true // "boolean"

typeof "foo" // "string"

typeof Symbol("id") // "symbol"

typeof Math // "object"  (1)

typeof null // "object"  (2)

typeof alert // "function"  (3)
```

#### ***Attention***

- le résultat de `typeof null` est "object", c'est une erreur reconnue dans typeof

- le résultat de `typeof alert` est "function", car `alert` est une fonction. MAIS, il n'y a pas de type "fonction" en JavaScript. Les fonctions appartiennent au type `object` mais `typeof` les traite différemment en retournant "function". Ça vient des débuts de Javascript et c'est pratique à l'usage.

`typeof (x)` est la même chose que `typeof x`

même si `typeof` est un opérateur pas une fonction!


# Les conversions  de types
[lien](https://fr.javascript.info/type-conversions)

La plupart du temps, les opérateurs et les fonctions convertissent automatiquement les valeurs qui leur sont attribués dans le bon type

Par exemple : 
- `alert` convertit automatiquement toute valeur en **chaîne de caractères** pour l'afficher. <br>
- Les opérations mathématiques convertissent les valeurs en **nombres**.

### String conversion

La conversion `String` se produit lorsque nous avons besoin de la forme **chaîne de caractères** d'une valeur.

`alert(value)` le fait pour *afficher la valeur* (donc pas une String conversion)

- exemple d'utilisation de `String(value)`

```javascript
let value = true;
alert(typeof value); // boolean

value = String(value); // maintenant la valeur est une chaîne de caractères "true"
alert(typeof value); // string
```

Un `false` devient `"false"`, `null` devient `"null"` , etc.

### Numeric Conversion

- La conversion numérique dans les fonctions et expressions mathématiques s'effectue automatiquement.

exemple : 
```javascript
alert("6"/ "2"); // 3, les chaînes de caractères sont converties en nombres
```

- on peut utiliser une fonction `Number(value)` pour convertir explicitement une valeur :

```javascript
let str = "123";  
alert(typeof str); // string

let num = `Number(str)`; // devient un nombre 123  
alert(typeof num); // nombre
```
 
Une conversion explicite est généralement requise lorsque nous lisons une valeur à partir d'une source basée sur des chaînes de caractères, par exemple un champ texte, mais qu'un nombre doit être entré.



Si la chaîne de caractères n'est pas un nombre valide, le résultat de cette conversion est `NaN`, par exemple :

```javascript
let age = Number("une chaîne de caractères arbitraire au lieu d'un nombre")

alert(age); // NaN, la conversion a échoué
```

Règles de conversion numériques :


|Valeur |	Devient … |
| :---:| :---: |
|undefined| 	NaN|
|null |	0|
|true et false |	1 et 0|
|string 	|Les espaces blancs du début et de la fin sont supprimés. Ensuite, si la chaîne restante est vide, le résultat est 0. Sinon, le nombre est «lu» dans la chaîne. Une erreur donne `NaN`.|


- exemples :

```javascript
alert( Number("   123   ") ); // 123
alert( Number("123z") );      // NaN (erreur de lecture d'un nombre à "z")
alert( Number(true) );        // 1
alert( Number(false) );       // 0

let x = null;
alert( Number(x) ); // 0
let y;
alert( Number(y)); // NaN
```
### Boolean Conversion

La conversion booléenne se produit
- dans des opérations logiques, 
- ou peut être effectué avec `Boolean(value)`

La conversion vers boolean suit les règles suivantes :
- Les valeurs qui sont intuitivement "vides" comme `0`, une chaîne de caractères vide, `null`,`undefined`, `NaN` deviennent `false`
- Les autres valeurs deviennent `true`.

|Valeur| 	Devient …|
| ---- | -----|
|0, null, undefined, NaN, "" 	|false|
|tout autre valeur 	|true|


La plupart de ces règles sont faciles à comprendre et à mémoriser. Les exceptions notables où les gens font généralement des erreurs sont :

- `undefined` est `NaN` en tant que number, non 0.
- "0" et les espaces dans les chaines de caractères comme " " sont “true” en booléen.
 
# Opérateurs de base, mathématiques

opérateurs connus : additions `+`, multiplications `*`, soustractions `-`,...


### Terminologie

- **Operands** are used in expressions and operations (e.g., `5 + 3`), whereas **arguments** are passed to functions (e.g., `add(5, 3)`).

- **Operands** are usually directly involved in mathematical or logical operations, while **arguments** are values provided to functions to influence their behavior.

- Un **opérateur** est *unaire* s'il a une seul opérande.<br> Par exemple, la négation unaire `-` :
```javascript
let x = 1;

x = -x;
alert( x); //-1, le moins unaire a été appliqué
```
- Un **opérateur** est *binaire* s'il a deux opérandes. <br> Négation dans la forme binaire :
```javascript
let x = 1, y = 3;
alert( y - x); // 2, le moins binaire soustrait des valeurs
```

D’un point de vue formel, dans les exemples ci-dessus, nous avons deux opérateurs différents qui partagent le même symbole : l’opérateur de négation, un opérateur unaire qui inverse le signe, et l’opérateur de soustraction, un opérateur binaire qui soustrait un nombre d’un autre.

### Opérations mathématiques

Les opérations mathématiques suivantes sont supportées :

- Addition `+`
- Soustraction `-`
- Multiplication `*`
- Division `/`
- Reste `%`

Le résultat de `a % b` est le reste de la division entière de `a` par `b`.
```javascript
alert( 5 % 2); // 1
alert( 8 % 3; // 2
alert( 8 % 4); // 0
```


- Exponentiation `**`

L’opérateur d’exponentiation `a ** b` multiplie a par lui-même b fois. En mathématiques à l’école, nous écrivons cela a<sup>b</sup>.

```javascript
alert( 2 ** 2); // 4
alert( 2 ** 3); // 8
alert (2 ** 4); // 16
```

L'opérateur d'exponentiation est également défini pour les nombres non entiers.

exemple,une racine carré est une exponentiation de ½ :

```javascript
alert( 4 ** (1/2) ); // 2, racine carré
alert( 8 ** (1/3) ); // 2, racine cubique
```

## Opérateurs JVS
### Concaténation de chaînes de caractères, (binaire +)

Habituellement, l’opérateur `+` additionne des chiffres.

Mais si le binaire `+` est appliqué aux chaînes de caractères, il les fusionne (concatène) :

```javascript
let s = "my" + "string";
alert(s); // mystring
```

Si l’un des opérandes est une chaîne de caractères, l’autre est automatiquement converti en chaîne de caractères.

```javascript
alert( "1" + 2); // 12
alert( "2" + 1); // 21
```

Notez que les opérations se déroulent de gauche à droite. S’il y a deux nombres suivis d’une chaîne, les nombres seront ajoutés avant d’être convertis en chaîne 

```javascript
alert(2 + 2 + "1"; // 41
alert("1" + 2 + 2); // 122
```

Le binaire `+` est le seul opérateur qui prend en charge les chaînes de caractères de cette manière. <br>D’autres opérateurs arithmétiques ne fonctionnent qu’avec des nombres et convertissent toujours leurs opérandes en nombres.



```javascript
alert( 6 + "2" ); // 62

alert( 6 - "2" ); // 4
alert( "6" / "2" ); // 3
```

### Conversion numérique, (unaire +)

L’unaire plus ou, en d’autres termes, l’opérateur plus `+ `appliqué à une seule valeur, ne fait rien avec les nombres, mais si l’opérande n’est pas un nombre, alors il est converti en nombre.

```javescript
let x = 1;
alert( +x); // 1

let y = -2;
alert( +y); // -2

alert( +true ); // 1
alert( +""); // 0
// Comme Number() mais en plus court
```


autre exemple
```javascript
let apples = "2";
let oranges = "3";

alert( apples + oranges); // 23

alert( +apples + +oranges ); // 5
//équivalent de ( Number(apples) + Number(oranges) );
```

**Question**
Pourquoi ne pas directement faire `let apples = 2;`

En programmation, les plus unaires sont appliqués en premier, ils convertissent les chaînes de caractères en nombres, puis le plus binaire les additionne.

### Précédence des opérateurs

**Operator precedence** determines how operators are parsed concerning each other. Operators with higher precedence become the operands of operators with lower precedence.

Il y a beaucoup d’opérateurs en JavaScript. Chaque opérateur a un numéro correspondant à sa priorité de précédence. Celui qui est plus haut sur le tableau s’exécute en premier. Si la priorité est la même, l’ordre d’exécution est de gauche à droite.

Aussi, les opérateurs unaires ont une priorité plus élevée que les binaires correspondants.

cf [tableau de précédence](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_precedence)

### Affectation

`=` a une faible précédence

```javascript
let x = 2 * 2 + 1;

alert( x ); // 5
```
attention in jvs `=` est un opérateur donc il renvoie une valeur

application : 

```javascript
let a = 1;
let b = 2;

let c = 3 - (a = b + 1 )

alert( a ); // 3
alert( c ); // 0
```

Nous le voyons parfois dans les bibliothèques JavaScript.

Mais n’écrivez pas le code comme ça, ça le rend moins lisible.










