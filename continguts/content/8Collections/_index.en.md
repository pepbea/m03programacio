---
date: 2016-04-09T16:50:16+02:00
title: Col·leccions
weight: 8
pre: "<b>8. </b>"
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

### Collections

{{% notice note %}}
Les **Collections** representen grups d'objectes, anomenats elements. Podem trobar diversos tipus de col·leccions, segons si els seus elements estan ordenats, o si permetem repetició d'elements o no. 
{{% /notice %}}

La informació de Java Oracle corresponen a la Collection la trobareu [aquí](https://docs.oracle.com/javase/8/docs/api/?java/util/Collection.html).

Com observareu de l'enllaç anterior una Collection és una interfície de la qual heradaran totes les estructures de dades que veurem a continuació. En aquesta interfície hi trobareu un conjunt de mètodes que totes les estructures tenen implementades: add(), size(), isEmpty(), etc. Aquests operadors són **polimòrfics** això vol dir que amb la mateixa denominació efectuen la mateixa funcionalitat però per estructures de dades diferents. Ex: el mateix mètode add() ens serveix per afegir un element a un HashSet a un ArrayList o a un LinkedList. 

Sempre que tinguem un tipus de dades que contingui una col·lecció implementarà totes les funcions comunes a ella i les podrem utilitzar. En aquesta interfície trobem una sèrie de mètodes que ens serviran per accedir als elements de qualsevol col·lecció de dades, sigui del tipus que sigui. 

Aquests mètodes generals són:

|Mètode|Funcionalitat|
|---|---|
|boolean **add(Object o)**|Afegir un element en la col·lecció|
|void **clear()**|Elimina tots els elements de la col·lecció|
|boolean **contains(Object o)**|Comprova si existeix l'element en la col·lecció|
|boolean **isEmpty()**|Comprova si la col·lecció està buida|
|boolean **remove(Object o)**|Elimina un element de la col·lecció|
|int **size()**|Retorna la quantitat d'elements que té la col·lecció|
|Object[] **toArray()**|Retorna els conjunt d'elements dins un array|

![arbre](images/collection.jpg?width=800px)


|Classe|Elements repetits|Elements ordenats| Comentaris|
|---|---|---|---|
|ArrayList|Sí, els permet| Elements ordenats per ordre d'inserció|És non-synchronized, si es vol synchronized: Vector|
|HashSet|No, no els permet| No existeix un ordre | Internament utilitza una taula de hash per guardar els elements|
|HashMap|Les claus són úniques, els valors poden estar duplicats| No existeix un ordre | Guarda valors basat en claus (diccionari)|

*Nota: Tot hi que HashMap no hereta de Collections (ho fa de Maps), el tractarem com un element més d'anàlisi ja que les seves propietats són molt idònies per determinats tipus de problema.*

*Quan utilitzar aquestes estructures en Java?*
1. Si no voleu tenir valors duplicats a la base de dades, *HashSet* hauria de ser la vostra primera opció, ja que totes les seves classes no permeten duplicats.
2. Si es necessiten operacions de cerca freqüents basades en els valors de l'índex, Llista (*ArrayList*) és una opció millor.
3. Si cal mantenir l’ordre d’inserció, també la *llista* és la interfície de col·lecció preferida.
4. Si el requisit és tenir les assignacions de claus i valors a la base de dades, llavors *HashMap* és la vostra millor aposta.


Collection i Maps són interfícies molt genèriques i analitzarem de forma pràctica les següents classes heredades d'aquestes amb exemples:

- [ArrayList]({{%relref "8Collections/1arrayList/_index.en.md" %}}): Array dinàmic per guardar objectes i elements.
- [HashSet]({{%relref "8Collections/2hashset/_index.en.md" %}}): Conjunt d'elements únics i que no tenen un ordre establert.
- [HashMap]({{%relref "8Collections/3hashmap/_index.en.md" %}}): Conjunt d'elements clau-valor (K-V).