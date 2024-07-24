---
title: Tipus de dades i variables
weight: 4
pre: "4. "
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
