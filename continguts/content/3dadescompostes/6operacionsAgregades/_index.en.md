---
date: 2016-04-09T16:50:16+02:00
title: Operacions agregades
weight: 6
pre: "6. "
chapter: false
---

{{% notice note %}}
Les **operacions agregades** en Java neix de l'oportunitat de processar operacions típiques en col·leccions d'una manera funcional i concisa.
{{% /notice %}}

Des de Java 8 amb la introducció de [Streams-API](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/stream/package-summary.html), Java permet el processament de fluxos i expressions lambda que permet l'encadenament d'operacions en una col·lecció.

Aquesta API permet integrar el paradigma funcional a les funcionalitats típiques que realitzem en les col·leccions, com són:
* Filtrar
* Transformar
* Reduir
* Agrupar 
* Ordenar 

{{% notice note %}}
**Fluxos - Streams**. Els fluxos d'elements permeten el processament en paral·lel o seqüencial dels elements d'una col·lecció, en les col·leccions de java per crear un flux en una estructura de dades d'una col·lecció tenim la funció *.stream()*.
{{% /notice %}}

```java
List<String> noms = Arrays.asList("Pep", "Alberto", "Susana", "Maria");
Stream<String> flux = noms.stream();
```
