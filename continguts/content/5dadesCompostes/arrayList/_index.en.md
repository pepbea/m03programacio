---
date: 2016-04-09T16:50:16+02:00
title: ArrayList
weight: 5
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

**Declaració**

En la declaració indicarem de quin tipus és la llista entre <>. Per exemple per declarar un ArrayList d'enters:
```java
  ArrayList<Integer> arrayListEnters = new ArrayList();
```

**Funcionalitats principals**

En el següent exemple es veuen diferents mètodes (tots ells explicats en la declaració de Java Oracle) que permeten actuar a un ArrayList de la mateixa manera que un Array (.add(), .size(), .get()),en ell es genera un arrayList d'enters, s'entren valors i es fa un recorregut per l'estructura:

```java
Scanner teclat = new Scanner(System.in);
ArrayList<Integer> arrayDinamic = new ArrayList<Integer>();
int valor = 1;

while (valor != 0)
{
    System.out.println("Introdueix valor");
    valor = teclat.nextInt();
    if (valor != 0)
        //Amb add() s'assignen nous valors a l'arrayList
        arrayDinamic.add(valor);
}

//.size() fa la mateixa funció que .length en els arrays estàtics
for (int i = 0; i<arrayDinamic.size(); i++)
    //Per tal d'accedir als elements usarem .get(int pos), recordem que la primera posició és 0.
    System.out.println("arrayDinamic.get("+i+") = "+arrayDinamic.get(i));



//altres funcions interessants són isEmpty o remove
if(arrayDinamic.isEmpty()) System.out.println("No existeix cap element dins l'arrayList, està buit");

//Eliminar un element per posició
arrayDinamic.remove(i);

teclat.close();
```

En aquesta pàgina trobareu uns quants exemples més d'ús d'ArrayList: [ArrayList con ejemplos](https://jarroba.com/arraylist-en-java-ejemplos/)





