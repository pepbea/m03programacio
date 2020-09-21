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

Una altra forma de declarar una matriu és amb els valors directament igual com ja havíem vist en l'array unidimensional. Per exemple, la següent matriu conté 3 files i 2 columnes:

```java
int[][] matriu = {13,25},{34,78},{0,-3}};
```

S'observen 3 files i cadascuna conté els valors entre {}, les files entre sí estan separades per una coma.


#### Longitud

Al igual que els vectors les matrius també poden fer ús de l'atribut length. El que passa que si provem d'imprimir ``matriu.length`` observarem que mostra el total de files que conté la matriu. Java organitza la informació com un vector de vectors, així que si volem saber el length d'una columna cal que fem el següent ``matriu[i].length``.

#### Funcionalitat


| Funcionalitat | Sintaxi | Exemples |
| --- | --- | --- | 
| Declaració d'un array 2D | tipus[][] nom; | int[][] matriu1; <br>double[][] matriu2;| 
| Creació d'un array de n files i m columnes | nom = new tipus[n][m]; |  matriu1 = new int [3][2]; <br> matriu2 = new double[5][5];| 
| Declaració d'un array 2D inicialitzat | tipus[][] nom ={{elem01,...,elem0n},{elem11,...,elem1n},...,{elemm1,...,elemmn}} | int[][] matriu1={{13,25},{34,78},{0,-3}};| 
| Accés a l'element de la fila i i columna j | nom[i][j] |  int a = matriu1[1][0];<br>double m = matriu2[5][8];| 


#### Recorregut
Per fer un recorregut d'un array bidimensional o matriu utilitzarem 2 bucles anidats. Això
ens permetrà tenir dos índexos, un per les files i un per les columnes. Per exemple:

```java
int rows = 10;
int cols = 10;
int[][] myArray = new int[rows][cols];
for (int i = 0; i < rows; i++){
    for (int j = 0; j < cols; j++){
        myArray[i][j] = 0;
    }
}
```

#### Cerca
De la mateixa manera que treballàvem la cerca d'un element dins un vector, en les matrius funciona igual, només que ara toca realitzar la cerca en dos bucles anidats. En aquest cas, quan es troba l'element (si es troba) cal sortir dels dos bucles. 

En el següent exemple busquem el 0 dins una matriu de nombres aleatoris:

```java
boolean trobat=false;
int matriu[][] = new int[10][12];

//Introduim valors aleatoris
for (int i = 0; i < matriu.length; i++){
    for(int j = 0; j < matriu[i].length; j++){
        matriu[i][j] = (int) (Math.random() * 100);
    }
}

for (int i = 0; i < matriu.length && !trobat; i++){
    for(int j = 0; j < matriu[i].length && !trobat; j++){
        if( matriu[i][j]==0) trobat=true;
    }
}
String resposta = (trobat)? "S'ha trobat l'element" : "NO s'ha trobat l'element";
System.out.println(resposta);  
```

##### Exemple

Busquem l'element màxim i mínim d'una matriu:
```java
int max = Integer.MIN_VALUE;
int min = Integer.MAX_VALUE;

//RECORREM FILES
for(int i=0; i<matriu.length;i++) {

    //RECORREM COLUMNES
    for (int j = 0; j < matriu[i].length; j++) {

        //BUSQUEM ELEMENT MES GRAN i MES PETIT
        if(matriu[i][j] > max) max = matriu[i][j];
        if(matriu[i][j] < min) min = matriu[i][j];

    }
}
System.out.println("");
System.out.println("MAX: "+max);
System.out.println("MIN: "+min);
```