---
date: 2016-04-09T16:50:16+02:00
title: Diccionari - Hashmap
weight: 3
pre: "5.3. "
---

{{% notice note %}}
**HashMap**: és una estructura de dades que conté elements que obeeixen a la lògica clau-valor (K-V). La clau és única en tota la col·lecció i identifica un element respecte els altres, els valors poden estar duplicats.
{{% /notice %}}

La definició de la classe HashMap **java.util.HashMap** i de totes les seves funcionalitats la trobareu a:
[Java Oracle Classe HashMap](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/HashMap.html)

Utilitza una taula de dispersió per a emmagatzemar la informació de mapa. Les operacions bàsiques (get i put) es faran en temps constant sempre que es dispersin adequadament els elements. El cost de la iteració dependrà del nombre d'entrades de la taula i del nombre d'elements del mapa. No es garanteix que es respecti l'ordre de les claus. Tot hi que se l'identifica com una Collection, un HashMap hereta de Map i no de Collection.

**Declaració**

En la declaració indicarem de quin tipus és la llista en <K, V>. Per exemple per declarar un HashMap on la clau són enters i els valors són Strings:
```java
  HashMap<Integer,String> hm = new HashMap<Integer,String>();
```

**Funcionalitats principals**

En l'exemple s'observa la manipulació d'un HashMap primer per un parell<Integer, String> i després per un parell <Integer,Alumne>:

```java
import java.util.*;
import java.util.stream.Collectors;

public class ExHashmap {
    public static void main(String[] args)
    {
        // HashSet de String
        // Creem el Hashmap
        HashMap<Integer,String> hm = new HashMap<Integer,String>();

        // Afegim elements
        hm.put(45,"Element 9");
        hm.put(23,"Element 2");
        hm.put(12,"Element 7");
        hm.put(87,"Element 4");
        hm.put(97,"Element 5");
        hm.put(34,"Element 6");
        hm.put(56,"Element 3");
        hm.put(32,"Element 8");
        hm.put(98,"Element 1");

        // Afegim elements amb la mateixa clau
        hm.put(98,"Element maxacat");
        hm.put(56,"Element maxacat");
        hm.put(32,"Element maxacat");
        hm.put(34,"Element maxacat");

        // Imprimim hashmap
        System.out.println("\nRealitzem recorregut de tres maneres diferents");
        System.out.println("1. Mitjançant la key");
        for (int key : hm.keySet()) {
            System.out.println(key+" --> "+hm.get(key));
        }

        System.out.println("\n2. Només amb els valors");
        for (Object value : hm.values()) {
            System.out.println((String)value);
        }

        System.out.println("\n3. Amb valor i clau");
        for (Map.Entry<Integer, String> entry : hm.entrySet()) {
            int key = entry.getKey();
            Object value = entry.getValue();
            System.out.println("Per la clau " + key + " tenim el valor " + value);
        }

        System.out.println("\nSi intento eliminar amb el mètode remove(key), si la key no existeix retorna null");
        System.out.println(hm.remove(1));

        System.out.println("\nSi intento eliminar amb el mètode remove(key), si la key existeix retorna el valor");
        System.out.println(hm.remove(98));

        //Ordenació mitjançant TreeMap
        System.out.println("\nOrdenem mitjançant un TreeMap");
        TreeMap<Integer, String> hmOrdenat = new TreeMap<>(hm);
        //TreeMap<Integer, String> hmOrdenat2 = new TreeMap<>();
        //hmOrdenat2.putAll(hm);

        System.out.println("\nMostrem HashMap ordenat per keys");
        for (int key : hmOrdenat.keySet()) {
            System.out.printf("key: %s, value: %s\n", key, hmOrdenat.get(key));
        }

        /*System.out.println("\nMostrem HashMap ordenat per keys");
        Set ref = hmOrdenat.keySet();
        Iterator it = ref.iterator();
        while (it.hasNext()) {
            int key = (int) it.next();
            System.out.println(key + " --> " + hmOrdenat.get(key));
        }*/
        System.out.println("\nMostrem HashMap ordenat per valors");
        final Map<Integer, String> ordenarPerString = hm.entrySet()
                .stream()
                .sorted(Map.Entry.comparingByValue())
                .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue, (e1, e2) -> e1, LinkedHashMap::new));

        for (int key : ordenarPerString.keySet()) {
            System.out.printf("key: %s, value: %s\n", key, ordenarPerString.get(key));
        }

        //Objectes ALUMNE
        // HashMap d' objectes Alumne
        System.out.println("\nHASHMAP ALUMNES");
        HashMap<Integer, Alumne> alumnes = new HashMap<Integer,Alumne>();

        // Afegir element
        alumnes.put(4,new Alumne(20, "Amos", "Ledesma"));
        alumnes.put(3,new Alumne(21, "Roger","Polo"));
        Alumne al = new Alumne(25, "Oriol","Benito");
        alumnes.put(2,al);
        alumnes.put(1,new Alumne(28, "Joaquim","Rocamora"));
        alumnes.put(5,new Alumne(18, "Hector", "Peris"));

        // Imprimim hashmap les altre dues formes d'imprimir també funcionen.
        System.out.println("\nRealitzem recorregut");
        System.out.println("Mostrem HashMap d'alumnes:");
        for (int key : alumnes.keySet()) {
            System.out.println("key: "+ key +" valor: " + alumnes.get(key));
        }

        //ORDENAR MITJANÇANT ARRAYLIST
        System.out.println("\nOrdenar claus i valors per ArrayList");
        List<Integer> keyAlumnes = new ArrayList<>(alumnes.keySet());
        Collections.sort(keyAlumnes);
        System.out.println("Ordenar claus");
        System.out.println(keyAlumnes);

        List<Alumne> alumnesLlista = new ArrayList<>(alumnes.values());
        Collections.sort(alumnesLlista, Alumne.alumnesCompararPerCognom);
        System.out.println("\nOrdenar valors per cognom");
        for(Alumne alumne: alumnesLlista)
        System.out.println(alumne);

        
        // Comprovar si conté un objecte
        System.out.println("\nComprovem si conté un element per key");
        if (alumnes.containsKey(4)) {
            System.out.println("Existeix l'alumne buscat "+alumnes.get(4));
        }
        System.out.println("\nComprovem si conté un element per valor");
        if (alumnes.containsValue(al)) {
            System.out.println("Existeix l'alumne buscat "+alumnes.get(1));
        }

        //Eliminem i recorregut
        System.out.println("\nEliminem l'element amb key: 1");
        alumnes.remove(1);
        System.out.println(alumnes);
    }
}
```