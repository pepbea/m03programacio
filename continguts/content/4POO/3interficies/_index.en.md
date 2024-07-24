---
date: 2016-04-09T16:50:16+02:00
title: Interfícies
weight: 3
pre: "3. "
---

Les interfícies són un pas més cap a l'abstracció. **Una interfície té tots els mètodes abstractes. Ens serveix per diferenciar la declaració dels mètodes de la seva implementació.** S'acostuma a crear interfícies per definir característiques/funcionalitats que han de tenir les classes concretes i afegir-les en la seva implementació. Desde Java8 és possible tenir mètodes `default` implementats per defecte dins les interfícies, ho veurem amb l'exemple del diamant al final de la lliçó.


Característiques de les interfícies:
- Els mètodes d'una interfície són públics, en canvi, les interfícies poden ser públiques default.
- Les interfícies només poden tenir variables públiques, estàtiques i finals, constants. Si no es posa res, es sobreentén que són públiques, estàtiques i finals. 

#### Implementació

La declaració d'una interfície la faríem de la següent manera:

```java
public interface Movible{
    int SEGONS_PARTIDA = 200;
    public void giraDreta();
    public void giraEsquerra();
    public int frena();
    public int anarEndavant();
}
```

Un cop tenim definit com volem la interfície ara cal incloure-la en les classes. Fins ara utilitzàvem `extends` ja que la relació era "ÉS UN", amb les interfícies estem afegint característiques a un objecte, usarem la paraula `implements`. 

De l'exemple anterior, si tinguéssim una simulació de vehicles i ens fes falta definir funcions per les funcions físiques de cada vehicle ho podríem fer de la següent manera:

```java
public abstract class Vehicle{
    protected int velocitat;
    protected int orientacio;
    ...
}

public class Cotxe extends Vehicle implements Movible{

    public void giraDreta(){
        orientacio = orientacio + 45;
    }
    public void giraEsquerra(){
        orientacio = orientacio - 45;
    }
    public int frena(){
        if(velocitat <=10) velocitat = 0;
        else velocitat -=10;
    }
    public int anarEndavant(){
        velocitat +=10;
    }
}

public class Moto extends Vehicle implements Movible{

    public void giraDreta(){
        orientacio = orientacio + 60;
    }
    public void giraEsquerra(){
        orientacio = orientacio - 60;
    }
    public int frena(){
        if(velocitat <=5) velocitat = 0;
        else velocitat -=5;
    }
    public int anarEndavant(){
        velocitat +=5;
    }
}

```

Si volgués incloure un nou vehicle a la meva simulació tant sols seria necessari que tingués en compte d'implementar aquells mètodes que té definits la interfície i també els mètodes abstractes que tingués la classe abstracta.

Una de les **avantatges de les interfícies és que permet més d'una implementació per classe** a diferència de les herències que en java tenim només herència simple. Podríem tenir com exemple:

```java
public interface Movible{
    public void A();
}
public interface Comercial{
    public void B();
}
public interface Navegable{
    public void C();
}

public class Taxi extends Vehicle implements Movible, Comercial{
    public void A(){
        ...
    }
    public void B(){
        ...
    }
}

public class Veler extends Vehicle implements Movible, Navegable{
    public void A(){
        ...
    }
    public void C(){
        ...
    }
}
```
També, al igual que amb les classes abstractes, podria existir **jerarquies de classe** dins una interfície, es podrien estendre. Si això passa, **les classes concretes haurien d'implementar tots aquells mètodes de totes les superclasses de la/les interfície/s utilitzades**.

```java
public interface InterficieSuper{
    public void A();
}
public interface InterficieSub extends InterficieSuper{
    public void B();
}

public class ClasseConcreta implements InterficieSub{
    public void A(){
        ...
    }
    public void B(){
        ...
    }
}
```

#### Agrupar per funcionalitat

Totes les classes que implementen una interfície són compatibles amb el tipus introduït per la interfície. Una interfície no es pot instanciar, però sí s'hi pot fer referència. Així, si I és una interface i C és una classe que implementa la interfície, es poden declarar referències al tipus I que apuntin objectes de C: I obj = new C (<paràmetres>); Exemple:

Seguint amb l'exemple anterior amb les interfícies movible, comercial i navegable. Podríem agrupar els objectes concrets en ArrayList d'una interfície i realitzar-ne el recorregut:

```java
ArrayList<Movible> movibles= new ArrayList();
mov.add(new Cotxe());
mov.add(new Taxi());
mov.add(new Veler());
for (Movible vehicleMoviment : movibles) {
    vehicleMoviment.A();
}
```

#### Herència múltiple

En java existeix el problema que les classes només hereten d'un pare, això provoca el conflicte conegut amb el problema del diamant:
[Problema diamant](https://es.wikipedia.org/wiki/Problema_del_diamante)

**Exemple**

Si tenim un mètode definit a A i sobreescrit a B i C, D quin hereta? El de B o el de C?

![Problema diamant2](../images/diamant1.gif)

Per resoldre-ho, el que faríem en Java seria el següent:

```java
interface B{
   public default void m1() {
      System.out.println("display method of m1 for B");
   }
}
interface C{
   public default void m1() {
      System.out.println("display method of m1 for C");
   }
}
public class D implements B, C{
   public void m1() {
      B.super.m1();
      //or,
      C.super.m1();
   }
   public static void main(String args[]) {
      D obj = new D();
      obj.display();
   }
}
```

Resumint:

- Una interfície pot ser implementada per múltiples classes, de manera similar a com una classe pot ser superclasse de múltiples classes.
- Les classes que implementen una interfície estan obligades a sobreescriure tots els mètodes definits en la interfície. Si la definició d'algun dels mètodes a sobreescriure coincideix amb la definició d'algun mètode heretat, aquest desapareix de la classe.
- Una classe pot implementar múltiples interfícies, a diferència de l'herència, que només es permet d'una única classe base.
- Totes les classes que implementen una interfície són compatibles amb el tipus introduït per la interfície.
- L'existència de les interfícies possibilita l'existència d'una jerarquia de tipus (que no s'ha de confondre amb la jerarquia de classes) que permet l'herència múltiple.




