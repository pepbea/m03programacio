---
date: 2016-04-09T16:50:16+02:00
title: Conjunt - HashSet
weight: 2
pre: "5.2. "
---

{{% notice note %}}
**HashSet**: és un conjunt d'elements en els quals no hi trobem cap element repetit (Set) i que no existeix un ordre en l'inserció de nous elements. 
{{% /notice %}}

La definició de la classe ArrayList **java.util.HashSet** i de totes les seves funcionalitats la trobareu a:
[Java Oracle Classe HashSet](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/HashSet.html)

Considerem que un element està repetit si tenim dos objectes o1 i o2 iguals, comparant-los mitjançant l'operador o1.equals(o2). D'aquesta manera, si l'objecte a inserir en el conjunt estigués repetit, no ens deixaria inserir-lo i el mètode add retornaria false. Un conjunt pot contenir com a màxim un element null.

Els objectes s'emmagatzemen en una taula de dispersió (hash). El cost de les operacions bàsiques (inserció, esborrat, recerca) es realitzen en temps constant sempre que els elements s'hagin dispersat de forma adequada. La iteració a través dels seus elements és més costosa, ja que necessitarà recórrer totes les entrades de la taula de dispersió, el que farà que el cost estigui en funció tant del nombre d'elements inserits en el conjunt com de el nombre d'entrades de la taula. L'ordre d'iteració pot ser diferent de l'ordre en què es van inserir els elements.

**Declaració**

En la declaració indicarem de quin tipus són els elements del Set <>. Per exemple per declarar un HashSet d'enters:
```java
  HashSet<Integer> conjuntEnters = new HashSet();
```

**Funcionalitats principals**

En l'exemple s'observa la manipulació d'un HashSet primer per enters i després per un set d'objectes Alumne:

```java
import java.util.*;

public class ExHashSet {
    public static void main(String[] args)
    {
        // HashSet de String
        // Creem el HashSet
        HashSet<String> hS = new HashSet<String>();

        // Afegim elements
        hS.add("Element 9");
        hS.add("Element 2");
        hS.add("Element 7");
        hS.add("Element 4");
        hS.add("Element 5");
        hS.add("Element 6");
        hS.add("Element 3");
        hS.add("Element 8");
        hS.add("Element 1");

        // Intentem afegir Elements repetits
        hS.add("Element 2");
        hS.add("Element 2");
        hS.add("Element 2");
        hS.add("Element 2");

        if (!hS.add("Element 2"))
            System.out.println("Element 2 nomes s'afegeix una sola vegada");
        System.out.println();

        // Recorregut usant la classe Iterator
        System.out.println("Realitzem un recorregut mitjançant iterator");
        Iterator<String> it = hS.iterator();
        while (it.hasNext())
            System.out.println((String)it.next());
        System.out.println();

        // Eliminar un element
        if (!hS.remove("Element 25"))
            System.out.println("Si intento esborrar un objecte que no existeix em retorna false!!!");
        System.out.println();

        System.out.println("Esborrem un element existent: Element 3, i mostrem com queda el HashSet");
        hS.remove("Element 3");
        System.out.println(hS);
        System.out.println();
        System.out.println();

        //Ordenació mitjançant TreeSet
        System.out.println("Ordenem mitjançant un TreeSet");
        TreeSet myTreeSet = new TreeSet();
        myTreeSet.addAll(hS);
        System.out.println(myTreeSet);

        //Objectes ALUMNE
        // ArrayList d' objectes Alumne
        System.out.println("\nHASHSET ALUMNES");
        HashSet<Alumne> alumnes = new HashSet<Alumne>();

        // Afegir elements
        System.out.println("Mostrem els alumnes");
        alumnes.add(new Alumne(20, "Amos", "Ledesma"));
        alumnes.add(new Alumne(21, "Roger","Polo"));
        Alumne al = new Alumne(25, "Oriol","Benito");
        alumnes.add(al);
        alumnes.add(new Alumne(28, "Joaquim","Rocamora"));
        alumnes.add(new Alumne(18, "Hector", "Peris"));

        // Recorregut usant la classe Iterator
        System.out.println("\nRealitzem un recorregut mitjançant iterator");
        Iterator its = alumnes.iterator();
        while (its.hasNext())
            System.out.println(its.next());

        //ORDENAR HASHSET USANT TREESET
        System.out.println("\nOrdenem mitjançant un TreeSet per NOM");
        TreeSet treeNom = new TreeSet(Alumne.alumnesCompararPerNom);
        treeNom.addAll(alumnes);
        its = treeNom.iterator();
        while (its.hasNext())
            System.out.println(its.next());

        System.out.println("\nOrdenem mitjançant un TreeSet per COGNOM");
        TreeSet treeCognom = new TreeSet(Alumne.alumnesCompararPerCognom);
        treeCognom.addAll(alumnes);
        its = treeCognom.iterator();
        while (its.hasNext())
            System.out.println(its.next());

        System.out.println("\nOrdenem mitjançant un TreeSet per EDAT");
        TreeSet treeEdat = new TreeSet(Alumne.alumnesCompararPerEdat);
        treeEdat.addAll(alumnes);
        its = treeEdat.iterator();
        while (its.hasNext())
            System.out.println(its.next());

        // Comprovar si conté un objecte
        System.out.println("\nComprovem si conté un element Alumne \"al\"");
        if (alumnes.contains(al)) {
            System.out.println("Existeix l'alumne buscat"+al);
        }

        //Eliminem i recorregut
        System.out.println("\nEliminem l'element 'al'");
        alumnes.remove(al);
        System.out.println(alumnes);
    }
}
```











