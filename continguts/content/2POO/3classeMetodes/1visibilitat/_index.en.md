---
title: Visibilitat
weight: 2
pre: "3.1. "
chapter: false
---


### Accessibilitat de les variables

Les **variables globals** són les variables tals que el seu àmbit de validesa i disponibilitat és total, és a dir, es poden utilitzar, actualitzant-les o no, des del programa principal i des de tots els subprogrames. No és aconsellable l'ús de variables globals. Les definim just després de la declaració de la classe, per ex:

```java 
public class Main{
public static int variableGlobal;
...
```

Una **variable local** és aquella que està declarada dins d’un subprograma. L’àmbit d’ús de les variables locals és el subprograma en què s’han definit. L’àmbit d’existència d’una variable és la part de la classe en què la variable pot ser
referenciada o s’hi pot accedir pel seu nom.

En Java, quan declarem una variable, aquesta és accessible només dins l'estructura on es declarada. En el cas dels arguments, només són visibles en el mètode en el qual s'usen. Posem un exemple:

```java 
public double m2km (double m)
{
    double km;
    km = m / 1000;
    return km;
}
```

En aquest cas les variables m i km només són accessibles dins del mètode m2km.

Un altre exemple:

```java 
public int sumElements (int[] array)
{
    int sum = 0;

    for(int i = 0; i < array.length; i++)
        sum = sum + array[i];
 
    return sum;
}
```

Les variables sum i array només són accessibles dins del mètode sumElements, però
la variable i només és visible dins del for.


**Visibilitat**

Fins el moment hem observat com els atributs i mètodes públics són accessibles des de fora de la pròpia classe i els que són privats són només accessibles desde dins la pròpia classe.

Amb l'herència apareix la visibilitat `protected`, que permet tenir visibilitat d'atributs i mètodes situats en:
* la mateixa classe
* les seves subclasses
* altres classes del mateix package

![visibilitat](./images/visibilitat.png)

Com s'observa existeix l'opció `default` quan no indiquem cap atribut de visibilitat, les classes declarades com a default tenen accés a totes les classes del propi package.
