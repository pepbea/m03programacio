---
date: 2016-04-09T16:50:16+02:00
title: Arrays Unidimensionals
weight: 1
---

{{% notice note %}}
**Arrays unidimensional**: és una estructura de dades que permet agrupar dades del mateix tipus dins un mateix bloc. 
{{% /notice %}}

### Exemple

Per exemple podríem necessitar les edats d'una classe per efectuar-ne un tractament especial. Fins ara el que podíem fer és declarar tantes variables enteres com alumnes hi hagi per tal de guardar-ne l'edat:

```java
int edatAlumne1 = 29;
int edatAlumne2 = 26;
int edatAlumne3 = 18;
...
int edatAlumne30 = 28;

```

Com podeu observar, si escaléssim el problema anterior i enlloc de 30 necessitéssim les edats dels 700 estudiants de l'institut, la declaració de variables seria una feina feixuga i amb un alt índex d'equivocar-nos, a més no permetria mantenir i modificar el programa de forma àgil. Per això hi ha les estructures de dades d'un mateix tipus. Una manera de guardar 700 edats dins una mateixa estructura seria aquesta:

```java
//Declarem una posició de memòria on comença un array
int[] edatsAlumnes;

//Aquest array és estàtic, per això abans d'usar-lo ens reservem en memòria el nombre d'enters que necessitem
edatsAlumnes = new int[700];

//Omplim les edats dels alumnes
for(int i = 0; i < edatsAlumnes.length; i++)
  edatsAlumnes[i] = sc.nextInt();
```

#### Declaració array

En les línies anteriors hem observat que per crear un objecte array, és necessari fer servir la paraula reservada ``new``, amb això el que fem és reservar en memòria l'espai necessari per allotjar la informació. En el següent exemple creem un array estàtic que l'anomeno ``arrayEstatic`` de 12 posicions.

```java
int[] arrayEstatic = new int[12];

//També es podria fer de la següent manera:
int arrayEstatic[] = new int[12];
```

Fixeu-vos que en el primer exemple he fet la declaració i la reserva d'espais dels enters en instruccions separades, en canvi en aquest últim exemple ho he fet tot junt en una única línia.

Per accedir a la posició enèssima de l'array ho puc fer de la següent manera ``arrayEstatic[n]``.

{{% notice note %}}
Els **Indexs** d'un array comencen en la **posició 0**, no en la 1. L'últim element de l'array es troba a la posició **llargària de l'array - 1**.
Així doncs en l'exemple anterior el primer enter de l'arrayEstatic es troba en la posició ``arrayEstatic[0]`` mentre que l'últim en la posició ``arrayEstatic[11]``. Hem de tenir en compte que l'**índex** no pot ser un valor negatiu, i que per exemple podria ser un càlcul numèric o fent ús de variables ``arrayEstatic[i + 1]``
{{% /notice %}}

![array](../images/array.gif?width=500px)

És important entendre que un cop declaro un arrayEstatic, es reserva en memòria espai per guardar el ``tipus de dades * Tamany de l'array``. En l'exemple anterior es demana al programa que ens reservi espai per a 12 enters consecutius. Aquests enters no tenen un valor definit (al ser enters Java els hi posa un 0), per tant cal que els inicialitzem un valor per utilitzar-los.

