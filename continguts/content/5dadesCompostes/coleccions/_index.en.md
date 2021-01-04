---
date: 2016-04-09T16:50:16+02:00
title: Col·leccions
weight: 5
---

{{% notice note %}}
Les **Collections** representen grups d'objectes, anomenats elements. Podem trobar diversos tipus de col·leccions, segons si els seus elements estan ordenats, o si permetem repetició d'elements o no. 
{{% /notice %}}

La informació de Java Oracle corresponen a les Collections la trobareu [aquí](https://docs.oracle.com/javase/8/docs/api/?java/util/Collections.html).

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

![arbre](../images/collection.jpg?width=700px)


|Classe|Elements repetits|Elements ordenats| Comentaris|
|---|---|---|---|
|ArrayList|Sí, els permet| Elements ordenats per ordre d'inserció|És non-synchronized, si es vol synchronized: Vector|
|HashSet|No, no els permet| No existeix un ordre | Internament utilitza una taula de hash per guardar els elements|
|HashMap|Les claus són úniques, els valors poden estar duplicats| No existeix un ordre | Guarda valors basat en claus (diccionari)|

*Nota: Tot hi que HashMap no hereta de Collections (ho fa de Maps), el tractarem com un element més d'anàlisi ja que les seves propietats són molt idònies per determinats tipus de problema.*

*Quan utilitzar-los en Java?*
1. Si no voleu tenir valors duplicats a la base de dades, *HashSet* hauria de ser la vostra primera opció, ja que totes les seves classes no permeten duplicats.
2. Si es necessiten operacions de cerca freqüents basades en els valors de l'índex, Llista (*ArrayList*) és una opció millor.
3. Si cal mantenir l’ordre d’inserció, també la *llista* és la interfície de col·lecció preferida.
4. Si el requisit és tenir les assignacions de claus i valors a la base de dades, llavors *HashMap* és la vostra millor aposta.


Collections i Maps són interfícies molt genèriques i analitzarem de forma pràctica les següents classes heredades d'aquestes amb exemples:

- [ArrayList]({{%relref "5dadesCompostes/coleccions/1arrayList/_index.en.md" %}}): Array dinàmic per guardar objectes i elements.
- [HashSet]({{%relref "5dadesCompostes/coleccions/2hashset/_index.en.md" %}}): Conjunt d'elements únics i que no tenen un ordre establert.
- [HashMap]({{%relref "5dadesCompostes/coleccions/3hashmap/_index.en.md" %}}): Conjunt d'elements clau-valor (K-V).