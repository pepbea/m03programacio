---
title: Definicions i exemples
weight: 2
pre: "1. "
chapter: false
---

Com hem observat, a mesura que tenim problemes més complexes és necessari fer ús de tècniques que ens ajudin a programar d'una forma més senzilla, d'aquesta manera hem passat de la programació estructurada a la programació funcional on hem ordenat i estructurat el codi en blocs d'instruccions coherents. Continuant en aquest procés ara toca fer el salt per conèixer la programació orientada a objectes (POO). 


#### 1. Paradigma de Programació orientada a objectes

{{% notice note %}}
Es fonamenta en la manera en que els éssers humans percebem i entenem els objectes del nostre món
{{% /notice %}}

__Exemple:__

| Joan | Maria |
| --- | --- |
| ![persona1](../images/persona1.jpg?width=230px) | ![persona2](../images/persona2.jpg?width=400px) |

Que tenen en comú el Joan i la Maria? **Els dos són persones**. 

Mitjançant un procés de generalització sabem que els dos __objectes__ Joan i Maria pertanyen a la mateixa __classe__ persona.

Mitjançant aquesta **abstracció** identifiquem molts *exemples* de la mateixa *plantilla*. Així doncs sabem que tots aquests exemples tenen les característiques comunes d'una plantilla persona.

![persona3](../images/persones3.jpg?width=500px)

Aprofundim ara en els nostres exemples de Persona: Joan i Maria.

|||
|---|---|
|![persona1](../images/persona1.jpg?width=230px)| *Atributs*<br>- Nom<br>- Estatura<br>- Pes<br>- Color cabell<br>- Color ulls<br>- Edat<br>- Sexe<br>- Té un nas<br>*Mètodes*<br>- Somriu<br>- Parla<br>- Dorm<br>- Pensa<br>- Menja|
|![persona2](../images/persona2.jpg?width=400px)| *Atributs*<br>- Nom<br>- Estatura<br>- Pes<br>- Color cabell<br>- Color ulls<br>- Edat<br>- Sexe<br>- Té un nas<br>*Mètodes*<br>- Somriu<br>- Parla<br>- Dorm<br>- Pensa<br>- Menja|

Com podem observar tant en Joan com la Maria tenen una sèrie de *característiques comunes* (atributs) i un *comportament comú* (mètodes) ja que els dos es poden classificar dins la mateixa categoria de persones.

La POO consisteix en fer servir aquesta manera natural de pensar en objectes com a mecanisme per a organitzar millor el nostre codi i poder desenvolupar, mantenir i ampliar aplicacions de software amb un alt grau de complexitat.

#### 2. Definicions

| | |
|---|---|
|Classe<br><br><br><br><br>|**Una classe és la definició d'un objecte real.**<br><br>És l'element que descriu els components d'un objecte de manera general. En ell hi queden especificats quines característiques té l'objecte (*atributs*) i quines accions pot realitzar (*mètodes*). És la plantilla que ens servirà per crear objectes.|
|Objecte<br><br><br><br>|**Un objecte és una instància d'una classe.** <br><br>Diem que hem creat o instanciat un objecte quan donem valors i fem servir els mètodes definits a la classe.|
|Atribut<br><br><br>|**Un atribut és una característica concreta d'un objecte.** <br><br>Es defineix com les variables del programes estructurats, és a dir, definint tipus de dades i identificador (nom).|
|Mètode<br><br><br>|**Els mètodes defineixen quines funcionalitats pot realitzar els objectes d'una classe.** <br><br>Reflecteixen les operacions que es poden fer sobre els atributs. |

##### Exemple

Un exemple podria ser una classe jugadorFutbol que tingués:

- *atributs:* nom, edat, pes, posició, nacionalitat, etc. 
- *mètodes:* marcaGols, esLesiona, protestaArbitre, canviaPosicio, etc.

I amb aquesta classe jugadorFutbol definida podríem tenir diferents jugadors, per tant hi instanciaríem diferents objectes:

- Leo Messi, 37 anys, 65kg, davanter, argentí.
- Andres Iniesta, 40 anys, 67kg, centrecampista, espanyol.

#### 3. Característiques generals de POO

##### Abstracció

{{% notice note %}}
Es tracta de centrar-se en **“el què fa”** més que no en el **“com ho fa”**.
{{% /notice %}}

Com hem vist en l'exemple anterior, sabem que dos objectes diferents com el Joan i la Maria tenen unes característiques i un comportament comú, d'aquí hem deduït per abstracció que formen part del mateix conjunt Persones. Així doncs l'abstracció ens permet aïllar aquella part que ens interessa del conjunt. Ex:
- No és necessari saber de mecànica de bicicletes per aprendre a anar en bicicleta.
- No és necessari conèixer què fan exactament les funcions del kernel de linux per usar-les.
- No ens cal conèixer en profunditat com funciona el rentaplats per usar-lo.
Tots els exemples anteriors són casos en els que fem ús d'un instrument sense coneixer-lo a fons.

Quan definiu les classes podeu crear funcions privades que utilitzeu pel funcionament del vostre programa però que NO seran accessibles des del programa principal.

![car1](../images/car1.png)

![car2](../images/car2.png)

L'abstracció permet que qualsevol objecte el poguem **reutilitzar** en qualsevol situació. Per exemple, l'objecte cotxe vist anteriorment el podem fer servir en una aplicació de carreres però també per a una altra de mobilitat sostenible. El que tenen en comú és que identifiquem el mateix objecte en ambdues aplicacions(característiques i comportament).

##### Encapsulament

{{% notice note %}}
Es refereix a l'ocultació d'informació de forma que les dades internes d'un objecte són ocultes al món exterior, tal sols sabem què podem fer amb ell.
{{% /notice %}}
 
Per exemple, quan escrivim per pantalla amb el mètode “sc.nextInt()”, sols sabem que ens retorna un enter però no sabem com és la implementació d'aquest mètode per dins, ni tampoc coneixem les seves variables internes.

##### Modularitat

{{% notice note %}}
es refereix a la forma en que els elements es POO es troben organitzats en mòduls (paquets en Java) facilitant l'encapsulació i abstracció de la informació.
{{% /notice %}}


![paquets](../images/paquets.gif)

##### Jerarquia

{{% notice note %}}
S'ordenen els objectes de forma que s'estableixen relacions entre ells. Serveix per especificar aquelles característiques d'un objecte necessàries per la nostra aplicació.
{{% /notice %}}

La jerarquia s'estableix mitjançant herència. Per exemple, podem definir objectes vehicle (amb matrícula, cavalls, etc..) i també objectes camions que hereten les característiques de vehicle i n'afegeixen d'altres (pes màxim, etc...).

##### Polimorfisme

{{% notice note %}}
Defineix la possibilitat de tenir mètodes i classes amb la mateixa identificació però que tenen un comportament diferent segons l'objecte que la faci servir.
{{% /notice %}}

Un bon exemple de polimorfisme és l'operador +. Si l'apliquem a dos enters ens retorna la suma d'aquests, mentre que si l'apliquem a dos strings ens els concatena, per tant, donat el mateix operador, el comportament és diferent, és un element sobrecarregat i que adopta diferent funció depenent dels tipus que el rodegen. En POO passa el mateix, podem tenir un mètode que faci una funció diferent depenent de quin objecte l'implementa. 

