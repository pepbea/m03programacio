---
title: Conversions
weight: 3
pre: "4.3. "
chapter: false
---

En Java existeix el `type casting` que permet convertir una variable en una altra. Quan realitzem un casting estem modificant el TIPUS de la variable.

El següent exemple de casos és bastant explicatiu:


```java
public class Main
{
   public static void main(String[] args)
   {
     System.out.println(1 / 3);            // 0
     System.out.println(1.0 / 3);          // 0.3333333333333333
     System.out.println(1 / 3.0);          // 0.3333333333333333
     System.out.println((double) 1 / 3);   // 0.3333333333333333
     System.out.println((double) (1 / 3)); // 0.0
   }
}
```

Com s'observa la primera divisió utilitza `/` entre dos enters, per això, malgrat que el valor és 0.333... es queda amb la part entera que és 0. Els dos casos següents dividim un nombre de tipus double amb un enter, així que per defecte retorna com a tipus de la divisió un double. 

Els dos últims casos és on apliquem **Casting**. 
Si us hi fixeu el 4rt cas és similar al primer amb la diferència que el resultat de la divisió entre dos nombres enters el "convertim" a double, de forma que permet guardar tots els decimals que perdíem en la divisió entre dos enters.

En l'últim cas no ens apareixen els decimals ja que primer es realitza l'operació entre els dos nombres enters i el resultat és enter, i una vegada obtenim el resultat (0), el convertim a double 0.0.

El casting és molt emprat en moltes situacions diferents en programació. A mesura que avancem i veiem classes i objectes veureu com també podem aplicar Casting entre diferents classes.

#### Situacions senzilles de casting

A vegades és necessari quedar-nos amb la part entera d'un nombre decimal:

```java
float decimal = 5.45f;
int partEntera = (int)decimal;    //partEntera = 5
```

A vegades només amb la part decimal, float double no ens guarden la precisió al castejar, en aquests casos utilitzaríem BigDecimal que sí que seria exacte;

```java
float decimal = 5.45f;
float partDecimal = decimal - (int)decimal;    //partEntera = 0.49999...
```


Un altre exemple on es pot apreciar fàcilment la diferència entre els decimals que pot guardar un double (64 bits) o un float (32 bits) és:

```java
float b=1.0f;
double a = Math.PI *b;
System.out.println(a);           // 3.141592653589793
System.out.println((float)a);    // 3.1415927
```

Un altre *casting* podria ser passar un caràcter a un enter. El caràcter és un tipus que ocupa 16 bits i que es pot transformar en un nombre fàcilment  seguint la [taula ASCII](https://elcodigoascii.com.ar/). Així doncs obtenim:

```java
char a = 'a';
System.out.println(a);           // a
System.out.println((int)a);      // 97

a++;
System.out.println(a);           // b
System.out.println((int)a);      // 98
```

De la mateixa manera a la inversa també obtindríem el mateix:

```java
int a = 97;
System.out.println(a);           // 97
System.out.println((char)a);      // a
```

