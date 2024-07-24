---
date: 2016-04-09T16:50:16+02:00
title: Genericitat
weight: 4
pre: "5.4. "
chapter: false
---

### Tipus Genèrics

*Són Tipus Parametritzat*. Permet indicar per paràmetre el tipus de dades sobre els que s'opera en classes, interfícies o mètodes.

Els tipus genèrics permeten escriure codi que resulta més segur i més fàcil de llegir. Els tipus genèrics són especialment útils amb les classes heredades de la interfície Collections.

**Els tipus genèrics permeten reutilitzar objectes de diferents tipus. El tipus genèric comporta l'abstracció de les operacions que es poden fer a conjunts diferents de dades.**

Quan parlem d'operacions que es poden fer a un determinat conjunt de dades, gairebé sempre hi tindrem:
+ Afegir elements.
+ Inserir elements.
+ Esborrar elements.
+ Actualitzar elements.
+ Obtenir un element.
+ Iterar pels elements.

Independentment del tipus dels elements que formen la llista dels elements, el tipus genèric ens permet aplicar una classe a un objecte concret ja sigui String, File, o objectes de classe com Llibre, Cotxe... 

Utilitzar un tipus genèric a l'hora de crear una col·lecció permet:
+ Crear estructures generalistes i reutilitzables independent de l'Objecte/dada que s'apliqui.
+ El codi on es passa un paràmetre com a genèric treballarà automàticament amb el tipus de dades que hem passat. Per exemple QuickSort treballa de la mateixa manera independentment del tipus de dades amb els que operi: String, Integers...
+ Treballar automàticament amb el tipus de dades passades al vostre paràmetre de tipus <T> normalment Type, tot hi que també pot haver E o V.
+ Controlar en temps de compilació ja que tots els elements són del tipus genèric.



Exemple de classe genèrica:

```java

public class Cotxe {
    private String marca;

    public Cotxe(String marca) {
        super();
        this.marca = marca;
    }
    
    public String getMarca() {
        return marca;
    }
 
    public void setMarca(String marca) {
        this.marca = marca;
    }
}


import java.util.ArrayList;
import java.util.Iterator;
public class Conjunt <T> implements Iterable <T> {
    private ArrayList <T> llista = new ArrayList <T> ();
    private int tamany;
    
    public Conjunt(int tamany) {
        super();
        this.tamany = tamany;
    }
    
    public void add(T objecte) {
        if (llista.size() >= tope) {
            llista.add(objecte);
        } else {
            throw new RuntimeException("no caben mas");
        }
    }
 
    public Iterator <T> iterator() {
        return llista.iterator();
    }
}


public class Principal {
    public static void main(String[] args) {
        Conjunt <Cotxe> conjuntCotxes = new Conjunt <Cotxe> ();
        Cotxe c = new Cotxe("Audio");
        Cotxe c1 = new Cotxe("Merceditas");
        Cotxe c2 = new Cotxe("Seaton");
        conjuntCotxes.add(c);
        conjuntCotxes.add(c1);
        conjuntCotxes.add(c2);
        for (Cotxe cotxe: conjuntCotxes) {
            System.out.println(cotxe.getMarca());
        }
    }
}

```

Si ara canviem l'objecte Cotxe per l'objecte Llibre, podem utilitzar la classe genèrica Conjunt igual ja que és independent del tipus de dades que la usi al ser genèrica.

```java

public class Llibre {
    private String titol;

    public Llibre(String titol) {
        super();
        this.titol = titol;
    }
    
    public String getTitol() {
        return titol;
    }
 
    public void setTitol(String titol) {
        this.titol = titol;
    }
}

public class Principal {
    public static void main(String[] args) {
        Conjunt <Llibre> conjuntLlibres = new Conjunt <Llibre> ();
        Llibre c = new Llibre("Aventures del Poblenou");
        Llibre c1 = new Llibre("Superherois de DAM");
        Llibre c2 = new Llibre("La vida a l'institut Poblenou");
        conjuntLlibres.add(c);
        conjuntLlibres.add(c1);
        conjuntLlibres.add(c2);
        for (Llibre llibre: conjuntLlibres) {
            System.out.println(llibre.getTitol());
        }
    }
}

```
