---
title: Primer programa
weight: 3
pre: "3. "
chapter: false
---

#### Primer programa

```java
public class Main {

    public static void main(String[] args) {

        System.out.println("Hello world!");
        
    }
}
```

En qualsevol llenguatge de programació, el primer programa que es veu és l'Hola Mon, aquest programa l'únic que fa és imprimir per pantalla un missatge, en aquest cas "Hello world!".

Tot el codi que escrivim estarà encapsulat dins una classe Main `public class Main`, i dins una funció main `public static void main(String []args)`. Els blocs de codi estan continguts dins els caràcters **{ }**.

En aquest cas, una manera senzilla d'escriure per pantalla un text és utilitzant la instrucció: `System.out.println("Hello world!")`; Tot el que estigui contingut dins **""** serà el text que es veurà per pantalla. Java tracta el tipus de text com a cadena de caràcters tot el que vagi contingut entre "".

Quan executem un programa de Java, el que farà la JVM és buscar una funció que es digui `public static void main(String []args)` i començarà a executar totes les instruccions que estiguin dins.


