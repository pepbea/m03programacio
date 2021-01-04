---
date: 2016-04-09T16:50:16+02:00
title: Herència
weight: 1
---

{{% notice note %}}
L'herència permet a una classe nova crear-se a partir d'una classe existent. La nova classe (subclasse) "hereta" els atributs i mètodes de la classe primària, i a més a més, té la possibilitat d'incorporar nous atributs i mètodes específics a la subclasse.
{{% /notice %}}

Aquesta particularitat permet crear una estructura jeràrquica de classes cada vegada més especialitzada. L'herència es basa en la reutilització de classes on es crea una classe nova incorporant atributs i mètodes de la classe pare. Els mètodes heretats poden ser sobreescrits i adoptar un comportament nou o amplicant-ne la seva funcionalitat. Aquesta reutilització permet estalviar molt de temps i adoptar components creats i ja testats.

Conceptes:

- *Superclasse:* Classe primària o existent en l'herència.
- *Subclasse:* classe nova i resultant d'aplicar herència a una altra classe.
- *Especialització:* Procés que permet estendre d'una classe pare a una classe filla, ampliant atributs i mètodes.
- *Generalització:* Procés de navegar de les classes filles a la classe pare. En la classe pare trobarem els atributs i mètodes comuns a totes les subclasses.

*java.lang.Object*

Una subclasse pot ser a la vegada superclasse d'altres classes i crear així un àrbre jeràrquic de classes. Com ja sabem, en Java totes les classes hereten d'una classe mare, la classe arrel de totes és java.lang.Object. Hi ha un conjunt de mètodes que tenen TOTES les classes de Java, inclús les que programeu vosaltres, aquí teniu la descripció de [Java Oracle referent a la classe Object](https://docs.oracle.com/javase/7/docs/api/java/lang/Object.html). 

*Herència simple*

Java permet l'herència simple: qualsevol classe només té una classe pare, no permet l'herència múltiple com sí permeten altres llenguatges de programació com el C++. Això ens planteja el problema que a vegades pels requisits de la nostra aplicació és necessari simular l'herència múltiple fent ús d'interfícies. Per a més informació: [problema del diamant](https://www.geeksforgeeks.org/java-and-multiple-inheritance/)

*Relació "és un" vs "conté un"*

L'herència és una relació d'extensió d'una classe més específica respecte una classe genèrica, això ens porta a que la classe filla **ÉS UNA** classe pare, però amb les funcionalitats ampliades/exteses/modificades. A vegades quan es programa existeix el dubte de confondre aquesta relació amb una relació de composició **CONTÉ UN**, que erròniament entenguem com a subclasse "una part"  de la classe principal. 