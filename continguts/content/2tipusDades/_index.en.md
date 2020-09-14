---
title: Tipus de dades i operadors
weight: 2
pre: "<b>2. </b>"
chapter: false
---


#### Tipus de dades

En el llenguatge Java incorpora tipus de dades diferents d'acord amb la seva naturalesa: no és el mateix un nombre, que un text o un valor verdader/fals per exemple. Aquests tipus de dades els classifiquem en tipus de dades primitius i tipus de dades de classe:
- **Primitius**: són les dades simples que coneixem com a nombres, text, etc. i que ens defineix de forma primitiva el llenguatge.
- **Classe**: són tipus de dades més complexos que es creen a partir dels mateixos tipus de classe o de tipus primitius.

#### Tipus Primitius

En Java podem diferenciar els següents tipus de dades primitius:

* Numèrics:
  * Enters: byte, short, int i long
  * Reals: float, double 
* Textuals:
  * chars
* Lògics:
  * boolean

La diferència entre els nombres enters i reals és que els nombres enters no contenen decimals (ex: 2 | 3 | 25) i els nombres reals reserven espai pels decimals (ex: 4,45 | 6,82 | 3,141592). Tot seguit us mostro una taula de rangs:

| Nom | Longitud | Rangs de valors |
| --- | --- | --- |
| byte | 8 bits	| De -2<sup>7</sup> a 2<sup>7</sup> -1 |
| short | 16 bits | De -2<sup>15</sup> a 2<sup>15</sup> -1 |
| int | 32 bits | De -2<sup>31</sup> a 2<sup>31</sup> -1 |
| long | 64 bits | De -2<sup>63</sup> a 2<sup>63</sup> -1 |
|float | 32 bits |
|double | 64 bits |
| char | 16 bits |

Els valors que admet una variable de tipus booleà és: true o false. Un valor booleà és molt comú en el camp informàtic on moltes vegades cal prendre una decisió que es pot avaluar en "veritat" o "fals".

##### Exemple d'assignació de valors

Declarem i assignem un valor a les variables:
```java
boolean valorBoolea = true;
int valorEnter = 50;
float valorDecimal = 50.3;
char lletra =’v’;
```

En aquest cas primer declarem les variables i després li assignem un valor:
```java 
boolean valorBoolea; 
valorBoolea = true;

int valorEnter;
valorEnter = 50;

float valorDecimal;
valorDecimal = 50.3;

char lletra;
lletra =’v’;
```

#### Operadors

### Operadors aritmètics

Són les operacions que avaluen una operació i retornen un resultat numèric.

| Operació | Operador| 
| --- | --- | 
| Suma |  + | 
| Resta | - |
| Multiplicació | * | 
| Divisió | / |
| Mòdul | % |

**Altres operadors**

Existeixen altres formes que simplifiquen l'escriptura alhora de fer operacions senzilles. Seria el cas dels comptadors. D'aquesta manera existeixen expressions com:

```java
int comptador = 0;
comptador = comptador + 1;

//es pot fer de forma més simple
int comptador = 0;
comtpador++;

//Les dues expressions següents també són equivalents i s'aplica a tots els operadors aritmètics:
int comptador = 0;

comptador = comptador + 10; 
comptador =+ 10; 

comptador = comptador - 10; 
comptador =- 10; 

comptador = comptador * 10; 
comptador =* 10; 

comptador = comptador / 10; 
comptador =/ 10; 
```

Recordem l'ordre de prioritat en les operacions aritmètiques:
- 1r Parèntesi ()
- 2n Multiplicacions, divisioons i mòdul  * / %
- 3r Sumes i restes + -

### Operadors lògics i relacionals

Són les operacions que avaluen una expressió i retornen un resultat booleà (true o false).

**Operadors lògics**

| A |	B	| !A |	 A && B  |	 A \|\| B |
| --- | --- | --- | --- | --- |
|true |	true	|	false	|	true	|	true |	
|true	|	false	|	false	|	false	|	true |
|false	|	true	|	true	|	false | true |
|false	|	false	|	true	|	false	|	false |

**Operadors relacionals**

Aquests operadors els podem aplicar a diferents tipus de dades i s'avalua l'expressió a un booleà (true o false).

| Operació | Signe	| Exemple1 | Resultat1 | Exemple2 | Resultat2 | 
| --- | --- | --- | --- | --- | --- |
| Major	| > | 5 > 3  | true  | 3 > 5  | false  | 
| Major o igual	| >= | 5 >= 5  | true  | 5 >= 3 | true  | 
| Menor	| < |  5 < 5  | false  | 3 < 2 | false  | 
| Menor o igual	| <= |  6 <= 5  | false  | 4 <= 5 | true  | 
| Igual	| == |  'c' == 'd'  | false  | 5 == 3 | false  | 
| No igual	| != | 'c' != 'd'   | true  | 5 != 5 | false  | 

**Prioritat**

La prioritat alhora d'avaluar expressions que contenen operadors aritmètics, relacionals i lògics és:
- 1r. Es realitzen els càlculs aritmètics.
- 2n. S'avaluen les operacions relacionals de < > <= >=
- 3r. S'avaluen les operacions relacionals de == !=
- 4rt. S'avaluen les negacions lògiques !
- 5è. S'avaluen les operacions de conjunció &&
- 6è. S'avaluen les operacions de disjunció ||

Les operacions anteriors **s'avaluen sempre d'esquerra a dreta.**