---
title: Estructures estàtiques i dinàmiques
weight: 1
pre: "1. "
chapter: false
---

{{% notice note %}}
Les estructures de dades són una eina que ens ofereix Java per guardar i organitzar dades de forma eficient, de manera que ens permeti manipular aquestes dades d'una manera òptima respecte a temps i memòria. Les estructures de dades s'utilitzen, principalment, pe reduir la complexitat del codi, sobretot en quan a temps d'execució.
{{% /notice %}}

En Java diferenciem entre les estructures de dades estàtiques i dinàmiques.

**Estructures de dades Estàtiques**
Les estructures de dades estàtiques permeten reservar en memòria un espai fix on es guardarà la informació abans d'utilitzar-lo. Sí que permet modificar els valors que guardem dins una estructura estàtica però no el tamany que és fix des de l'inici. Exemples d'estructures estàtiques en java hi ha els arrays, les matrius, les variables, les cadenes de caràcters (String),etc.

**Estructures de dades Dinàmiques** 
Les estructures dinàmiques defineixen inicialment amb quina estructura de dades treballaré i es va assignant memòria dinàmica a mesura que manipulem aquesta estructura, reservant nova memòria quan afegim elements i alliberant memòria quan en traiem. Exemples d'estructures dinàmiques en Java tenim totes les classes que deriven de Collections i que permeten definir les estructures típiques dinàmiques: llistes, conjunts, diccionaris, etc.

{{% notice note %}}
Les estructures dinàmiques de dades permeten d'una forma senzilla crear les principals estructures de dades molt útils en problemes algorítmics: llistes, arbres, grafs, cues, piles, etc.
{{% /notice %}}

Tot seguit pel que fa a estructures estàtiques analitzarem arrays unidimensionals (comunment dit array), arrays bidimensionals (matriu) i les cadenes de caràcters (Strings). Pel que fa a les estructures dinàmiques explicarem l'estructura que té Java de classificar totes les classes dins la interfície Collections i com **existeix un polimorfisme paramètric i tipus (Generics)** que permet definir l'estructura d'una estructura dinàmica sense necessitat d'especificar l'objecte que les conté. Treballarem amb un tipus de llista ArrayList, un tipus de conjunt HashSet i un tipus de diccionari HashMap.

