---
title: Operadors
weight: 2
pre: "4.2. "
chapter: false
---


Les **expressions** són una combinació de variables i operadors que retornen un valor determinat. El tipus de dada retornat depèn de l'operació realitzada en l'expressió i dels tipus de dades de les variables implicades.

Els **operadors** són els símbols especials que s'utilitzen per operar en les expressions.

### Operadors aritmètics

Són les operacions que avaluen una operació i retornen un resultat numèric.

| Operació | Operador| 
| --- | --- | 
| Suma |  + | 
| Resta | - |
| Multiplicació | * | 
| Divisió | / |
| Mòdul | % |

El mòdul és el residu d'una divisió, per exemple  `10 % 2 = 0`, o `16 % 3 = 1`. És una operació molt útil en camp informàtic ja que ens ajuda a saber per exemple si una divisió és entera i per tant a saber si un nombre és divisible per un altre, veurem exemples més endavant.

Recordem l'ordre de prioritat en les operacions aritmètiques:
- 1r Parèntesi ()
- 2n Multiplicacions, divisioons i mòdul  * / %
- 3r Sumes i restes + -


### Operadors d'increment/decrement

En Java existeix la possibilitat de realitzar un postincrement o un preincrement a una variable, per exemple: `a++  ++a  a--  --a`.

```java
//PostIncrement
a = 2;
System.out.println(a++);   // a = 2
System.out.println(a);     // a = 3

//Preincrement
a = 2;
System.out.println(++a);   // a = 3
System.out.println(a);     // a = 3

//PostDecrement
a = 2;
System.out.println(a--);   // a = 2
System.out.println(a);     // a = 1

//PreDecrement
a = 2;
System.out.println(--a);   // a = 1
System.out.println(a);     // a = 1
```

### Operadors d'assignació

| Operació | Operador| Exemple
| --- | --- | --- |
| Assignació |  = | a = b |
| Suma i assignació |  += | a += b  (a = a + b) | 
| Resta i assignació| -= | a -= b  (a = a - b)| 
| Multiplicació i assignació| *= |  a *= b  (a = a * b)| 
| Divisió i assignació| /= | a /= b  (a = a / b)| 
| Mòdul i assignació| %= | a %= b  (a = a % b)| 


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
