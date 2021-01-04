---
date: 2016-04-09T16:50:16+02:00
title: ArrayList
weight: 1
---

{{% notice note %}}
**Arrays unidimensional**: és una estructura de dades que conté una col·lecció de dades del mateix tipus i és dinàmica. 
{{% /notice %}}

La definició de la classe ArrayList **java.util.ArrayList** i de totes les seves funcionalitats la trobareu a:
[Java Oracle Classe ArrayList](https://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html)


**Propietats**
- Un arrayList funciona de forma similar a un array estàtic, conté elements del mateix tipus, poden ser repetits i aquests elements estan ordenats.
- A diferència d'un array estàtic, en els ArrayList no és necessari definir el tamany de l'array en la seva creació.
- Es tracta d'una llista d'elements en els que podrem iterar-los, afegir-ne, modificar-los o eliminar-los.


Les operacions d'afegir un element al final de l'array (add), i d'establir o obtenir l'element en una determinada posició (get/set) tenen un cost temporal constant. Les insercions i esborrats tenen un cost lineal O(n), on n és el nombre d'elements de l'array.

Hem de destacar que la implementació d' ArrayList no està sincronitzada, és a dir, si múltiples fils accedeixen a un mateix ArrayList concurrentment podríem tenir problemes en la consistència de les dades. Per tant, ho haurem de tenir en compte quan fem servir aquest tipus de dades que hem de controlar la concurrència d'accés, una altra opció és utilitzar la classe Vector, similar a ArrayList i que sí permet la sincronització.


**Declaració**

En la declaració indicarem de quin tipus és la llista entre <>. Per exemple per declarar un ArrayList d'enters:
```java
  ArrayList<Integer> arrayListEnters = new ArrayList();
```

**Exemple**

En el següent exemple es veuen diferents mètodes (tots ells explicats en la declaració de Java Oracle) que permeten actuar a un ArrayList de la mateixa manera que un Array (.add(), .size(), .get()), l'exemple és primer per un enter i després per una col·lecció d'objectes Alumne:

```java
import java.util.ArrayList;
import java.util.Collections;

public class ExempleArrayList {
    public static void main(String[] args)
    {
        
	/*
	 * ARRAYLIST AMB ENTERS
	 */

        System.out.println("ARRAYLIST ENTERS");
        ArrayList<Integer> aL = new ArrayList<Integer>();

        // Afegir elements
        aL.add(23);
        aL.add(12);
        aL.add(46);
        aL.add(2);

        // Recorregut
        System.out.println("Mostrem els elements tal qual s'han introduït, ArrayList és una llista d'elements:");
        for (int i=0; i<aL.size(); i++){
            System.out.print(aL.get(i) + " ");
        }
        System.out.println();
        System.out.println();

        // Comprovar si conté un objecte i obtenir la posició
        System.out.println("Comprovem si conté element 46 i diem la posició on es troba:");
        if (aL.contains(46)) {
            System.out.println("Existeix i es troba a la posició: " + aL.indexOf(46));
        }
        System.out.println();

        //Ordenem i recorregut
        Collections.sort(aL);
        System.out.println("Mostrem els elements ORDENATS:");
        for (int i=0; i<aL.size(); i++){
            System.out.print(aL.get(i) + " ");
        }
        System.out.println();
        System.out.println();

        //Eliminem i recorregut
        System.out.println("Eliminem l'element amb index 1:");
        aL.remove(1);
        for (int i=0; i<aL.size(); i++){
            System.out.print(aL.get(i) + " ");
        }
        System.out.println();


        
	/*
	 * ARRAYLIST AMB OBJECTES ALUMNE
	 */


        System.out.println("ARRAYLIST ALUMNES");
        ArrayList<Alumne> alumnes = new ArrayList<Alumne>();

        // Afegir elements
        System.out.println("Mostrem els elements tal qual s'han introduït:");
        alumnes.add(new Alumne(20, "Amos", "Ledesma"));
        alumnes.add(new Alumne(21, "Roger","Polo"));
        Alumne al = new Alumne(25, "Oriol","Benito");
        alumnes.add(al);
        alumnes.add(new Alumne(28, "Joaquim","Rocamora"));
        alumnes.add(new Alumne(18, "Hector", "Peris"));

        // Recorregut
        for (int i=0; i<alumnes.size(); i++){
            System.out.println(alumnes.get(i));
        }
        System.out.println();
        System.out.println();

        // Comprovar si conté un objecte i obtenir la posició
        System.out.println("Comprovem si conté un element Alumne \"al\" i diem la posició on es troba:");
        if (alumnes.contains(al)) {
            System.out.println("Existeix i es troba a la posició: " + alumnes.indexOf(al));
        }
        System.out.println();
        System.out.println();

        //ORDENACIÓ D'OBJECTES
        //Ordenem per edat i mostrem en recorregut
        Collections.sort(alumnes, Alumne.alumnesCompararPerEdat);
        System.out.println("Mostrem els elements ORDENATS:");
        for (int i=0; i<alumnes.size(); i++){
            System.out.println(alumnes.get(i) + " ");
        }
        System.out.println();
        System.out.println();

        //Ordenem per nom i mostrem en recorregut
        Collections.sort(alumnes, Alumne.alumnesCompararPerNom);
        System.out.println("Mostrem els elements ORDENATS:");
        for (int i=0; i<alumnes.size(); i++){
            System.out.println(alumnes.get(i) + " ");
        }
        System.out.println();
        System.out.println();

        //Ordenem per cognoms i mostrem en recorregut
        Collections.sort(alumnes, Alumne.alumnesCompararPerCognom);
        System.out.println("Mostrem els elements ORDENATS:");
        for (int i=0; i<alumnes.size(); i++){
            System.out.println(alumnes.get(i) + " ");
        }
        System.out.println();
        System.out.println();

        //Eliminem i recorregut
        System.out.println("Eliminem l'element amb index 1:");
        alumnes.remove(1);

        System.out.println();
        for (Alumne alumne : alumnes){
            System.out.println(alumne);
        }

    }
}
```

En aquesta pàgina trobareu uns quants exemples més d'ús d'ArrayList: [ArrayList con ejemplos](https://jarroba.com/arraylist-en-java-ejemplos/)





