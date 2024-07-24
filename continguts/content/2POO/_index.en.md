---
title: AEA2. Introducció a la POO
weight: 2

chapter: false
---

Com hem observat, a mesura que tenim problemes més complexes és necessari fer ús de tècniques que ens ajudin a programar d'una forma més senzilla, d'aquesta manera hem passat de la programació estructurada a la programació modular. Continuant en aquest procés ara toca fer el salt per conèixer la programació orientada a objectes (POO). Com ja hem vist dins el món de la programació hi ha una sèrie de paradigmes que repassem tot seguit.

{{% notice note %}}
Un **paradigma** és una forma de representar i manipular el coneixement. Representa un enfocament particular o filosofia per a la construcció del programari. 
{{% /notice %}}


#### 1. Paradigma de Programació orientada a objectes

{{% notice note %}}
Es fonamenta en la manera en que els éssers humans percebem i entenem els objectes del nostre món
{{% /notice %}}

__Exemple:__

Joan
![persona1](./images/persona1.jpg?width=500px)

Maria
![persona2](./images/persona2.jpg?width=500px)

Que tenen en comú el Joan i la Maria? **Els dos són persones**. 

Mitjançant un procés de generalització sabem que els dos __objectes__ Joan i Maria pertanyen a la mateixa __classe__ persona.

Mitjançant aquesta **abstracció** identifiquem molts *exemples* de la mateixa *plantilla*. Així doncs sabem que tots aquests exemples tenen les característiques comunes d'una plantilla persona.

![persona3](./images/persones3.jpg?width=500px)

Aprofundim ara en els nostres exemples de Persona: Joan i Maria.

|||
|---|---|
|![persona1](./images/persona1.jpg?width=400px)| *Atributs*<br>- Nom<br>- Estatura<br>- Pes<br>- Color cabell<br>- Color ulls<br>- Edat<br>- Sexe<br>- Té un nas<br>*Mètodes*<br>- Somriu<br>- Parla<br>- Dorm<br>- Pensa<br>- Menja|
|![persona2](./images/persona2.jpg?width=400px)| *Atributs*<br>- Nom<br>- Estatura<br>- Pes<br>- Color cabell<br>- Color ulls<br>- Edat<br>- Sexe<br>- Té un nas<br>*Mètodes*<br>- Somriu<br>- Parla<br>- Dorm<br>- Pensa<br>- Menja|

Com podem observar tant en Joan com la Maria tenen una sèrie de *característiques comunes* (atributs) i un *comportament comú* (mètodes) ja que els dos es poden classificar dins la mateixa categoria de persones.

La POO consisteix en fer servir aquesta manera natural de pensar en objectes com a mecanisme per a organitzar millor el nostre codi i poder desenvolupar, mantenir i ampliar aplicacions de software amb un alt grau de complexitat.
