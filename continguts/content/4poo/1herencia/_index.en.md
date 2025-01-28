---
date: 2016-04-09T16:50:16+02:00
title: Herència
weight: 1
pre: "1. "
---

L'herència permet a una classe nova crear-se a partir d'una classe existent, aquesta característica permet crear una estructura jeràrquica de classes cada vegada més especialitzada. L'herència es basa en la reutilització de classes on es crea una classe nova incorporant atributs i mètodes de la classe pare. Els mètodes heretats poden ser sobreescrits i adoptar un comportament nou o ampliant-ne la seva funcionalitat. Aquesta reutilització permet estalviar molt de temps i adoptar components creats i ja testats.

**Atribut final en l'herència**

A vegades, pels requisits de la nostra aplicació no ens interessa que hi pugui haver una herència en una classe, en aquests casos indicaríem mitjançant l'atribut final. Per exemple si vull que Persona sigui una classe final i que per tant no es pugui extendre ho marcaria de la següent manera:

```java
public final class Persona{
    ...
}
```

El mateix passa quan apliquem `final` a un mètode o a un atribut.

- En el **cas del mètode** si en la definició posem que és final no ens permetrà en subclasses sobreescriure'l, no el podrem modificar.

```java
package paquet.exemplefinal;
public class classeOrigen {
    public final void mostraInfo() {
        System.out.println("mostraInfo");
    }
}

package paquet.exemplefinal;
public class classeFilla extends classeOrigen {
    public void mostraInfo() {
        System.out.println("mostra una altra info");
    }
}
```

En aquest cas donaria un error de compilació ja que intentem sobreescriure un mètode que és definit com a final en la classe pare.

- En el **cas d'un atribut** final un cop inicialitzat no ens permetrà tornar-lo a modificar canviant-li el valor, s'utilitza per definir constants.

```java
public class CanviVariable {
    private final int enter=1;

    public CanviVariable(int enter){
        this.enter = enter;
    }
}


public class CanviVariable2 {

    public static void main(String[] args){
        final int enter = 0;
        enter = 2;
    }
}
```

Els casos anteriors donarien error ja que volem canviar el valor d'una variable que s'ha declarat final i ja té valor. En canvi, el cas següent no ens donaria cap error, ja que quan creem l'objecte donem valor per primer cop a aquesta variable, això sí, no li podrem canviar el valor en l'execució de tot el programa al ser final.

```java
public class CanviVariable {

    private final int enter;

    public CanviVariable(int enter){
        this.enter = enter;
    }
}
```

**Constructors i super**

Quan definim els mètodes constructors de les subclasses, és necessari primer cridar la constructora de la classe pare, això és possible gràcies a `super()` o `super(parametres)`. Quan es crea un fill primer sempre es comença inicialitzant les variables del pare i després s'inicialitzen les del fill. Si no posem cap mètode super, per defecte intentarà buscar super() en el pare, si no existís hi hauria un error de compilació.

```java
public class Persona{
    String dni;
    public Persona(String dni){
        this.dni = dni;
    }
}

public class Alumne extends Persona{
    int matricula;
    public Alumne(String dni, int matricula){
        super(dni);
        this.matricula = matricula;
    }
}

//Error de compilació ja que la constructora Persona() com a tal no existeix
public class Alumne extends Persona{
    int matricula;
    public Alumne(int matricula){
        super();
        this.matricula = matricula;
    }
}
```

**Exemple**

Realitzem un exemple de com seria una herència amb classe pare Producte i classe Filla ProducteDescompte.

```java

public class Producte {

    protected String nom;
    protected double preu;

    public Producte(String nom, double preu) {
        this.nom = nom;
        this.preu = preu;
    }

    public void anunci() {
        System.out.println("Hola sóc el producte " + nom);
    }

    public double valorProducte() {
        return preu;
    }
}

public class ProducteDescompte extends Producte {

    private int descompte;

    public ProducteDescompte(String nom, double preu, int descompte) {
        super(nom, preu);
        this.descompte = descompte;
    }

    @Override
    public void anunci() {
        super.anunci();
        System.out.println( "Tinc un descompte de " + descompte+"%");
    }

    @Override
    public double valorProducte() {
        return preu - (preu*descompte)/100;
    }

    public void rebaixaNouDescompte(int rebaixa){
        this.descompte = this.descompte - rebaixa;
    }

    public void augmentaNouDescompte(int augment){
        this.descompte = this.descompte + augment;
    }
}

public class Programa {

    public static void main(String[] args) {

        Producte p = new Producte("Llapis", 100.0);
        p.anunci();
        System.out.println("El preu del producte és " + p.valorProducte());
        System.out.println();
        ProducteDescompte p1 = new ProducteDescompte("Llapis rebaixat", 100.0, 10);
        p1.anunci();
        System.out.println("El preu d'un nou producte rebaixat és " + p1.valorProducte());
        System.out.println();
        p1.augmentaNouDescompte(10);
        p1.anunci();
        System.out.println("El preu del producte després de modificar la rebaixa és " + p1.valorProducte());
    }

}

```
