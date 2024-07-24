---
title: Operadors
weight: 2
pre: "4.2. "
chapter: false
---


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
