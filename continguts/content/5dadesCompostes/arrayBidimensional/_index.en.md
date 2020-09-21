---
date: 2016-04-09T16:50:16+02:00
title: Arrays Bidimensionals
weight: 2
---

{{% notice note %}}
**Arrays bidimensional**: és una estructura d'array de dues dimensions. També s'entén com un vector de vectors. Es coneix amb el nom de matriu. És una col·lecció d'elements del mateix tipus disposats en dues dimensions.
{{% /notice %}}

En aquest cas al tenir dues dimensions en forma de taula, la primera dimensió ens indica les files i la segona les columnes. 

#### Declaració

A l'igual que amb els arrays unidimensionals existeix la part de **declarar una referència** a la matriu i tot seguit quan cridem el ``new`` reservem en memòria l'espai on allotjar la informació. 

En l'exemple següent creem una matriu d'enters que l'anomenem ``balances`` de 11 x 6 posicions guardem en memòria 66 enters de forma consecutiva i ordenats per files i columnes. 

Per tal d'accedir a un element cal indicar ara dos índexs, un per les files i un per les columnes, si per exemple volgués accedir a l'element situat a la 4 fila i 5a columna ho faríem amb ``balances[3][4]``

```java
int[][] balances = new int[11][6];
int valor = balances[3][4];
```

![matriu](../images/matriu.png?width=500px)