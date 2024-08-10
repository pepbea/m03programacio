---
date: 2016-04-09T16:50:16+02:00
title: Arrays Unidimensionals
weight: 2
pre: "2. "
---

{{% notice note %}}
**Arrays unidimensional**: és una estructura de dades que conté un conjunt de dades del mateix tipus. 
{{% /notice %}}

La biblioteca de classes de Java inclou una classe auxiliar que s'anomena **java.util.Arrays** i conté funcions molt útils per utilitzar amb arrays:
[Java Oracle Classe Arrays](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/Arrays.html)


**Propietats**
- Els arrays s'utilitzen com a contenedors per guardar dades relacionades (enlloc de declarar variables per separat per cada un dels elements de l'array).
- Totes les dades incluïdes a l'array són del mateix tipus. Es poden crear arrays d'enters (int, long), de reals(float, double), però en un mateix array no es poden mesclar dades de tipus diferents.
- En els arrays estàtics el tamany s'estableix quan es crea l'array (amb l'operador new, igual que qualsevol altre objecte).
- Al ser un conjunt d'elements ordenats, a cada element de l'array s'hi accedirà a través de la posició que ocupa dins el conjunt.

### Exemple

Per exemple podríem necessitar les edats d'una classe per efectuar-ne un tractament especial. Fins ara el que podíem fer és declarar tantes variables enteres com alumnes hi hagi per tal de guardar-ne l'edat:

```java
int edatAlumne1 = 29;
int edatAlumne2 = 26;
int edatAlumne3 = 18;
...
int edatAlumne30 = 28;

```

Com podeu observar, si escaléssim el problema anterior i enlloc de 30 necessitéssim les edats dels 700 estudiants de l'institut, la declaració de variables seria una feina feixuga i amb un alt índex d'equivocar-nos, a més no permetria mantenir i modificar el programa de forma àgil. Per això hi ha les estructures de dades d'un mateix tipus. Una manera de guardar 700 edats dins una mateixa estructura seria aquesta:

```java
//Declarem una posició de memòria on hi ha una referència a un array
int[] edatsAlumnes;

//Aquest array és estàtic, per això abans d'usar-lo ens reservem en memòria el nombre d'enters que necessitem
edatsAlumnes = new int[700];

//Omplim les edats dels alumnes
for(int i = 0; i < edatsAlumnes.length; i++)
  edatsAlumnes[i] = sc.nextInt();
```

#### Declaració array

En les línies anteriors hem observat que per crear un objecte array, és necessari fer servir la paraula reservada ``new``, amb això el que fem és reservar en memòria l'espai necessari per allotjar la informació. En el següent exemple creem un array estàtic que l'anomeno ``arrayEstatic`` de 12 posicions.

```java
int[] arrayEstatic = new int[12];

//També es podria fer de la següent manera:
int arrayEstatic[] = new int[12];
```

Fixeu-vos que en el primer exemple he fet la declaració i la reserva d'espais dels enters en instruccions separades, en canvi en aquest últim exemple ho he fet tot junt en una única línia.

Per accedir a la posició enèssima de l'array ho puc fer de la següent manera ``arrayEstatic[n]``.

{{% notice note %}}
Els **Indexs** d'un array comencen en la **posició 0**, no en la 1. L'últim element de l'array es troba a la posició **llargària de l'array - 1**.
Així doncs en l'exemple anterior el primer enter de l'arrayEstatic es troba en la posició ``arrayEstatic[0]`` mentre que l'últim en la posició ``arrayEstatic[11]``. Hem de tenir en compte que l'**índex** no pot ser un valor negatiu, i que per exemple podria ser un càlcul numèric o fent ús de variables ``arrayEstatic[i + 1]``
{{% /notice %}}

![array](../images/array.gif?width=500px)

És important entendre que un cop declaro un arrayEstatic, es reserva en memòria espai per guardar el ``tipus de dades * Tamany de l'array``. En l'exemple anterior es demana al programa que ens reservi espai per a 12 enters consecutius. Aquests enters per defecte s'inicialitzen a 0 (si fossin booleans a false).

```java
int index = 4;
int array[index + 1]++;
```

En aquest exemple s'observa com inicialitzem un índex a 4, s'accedeix a l'element amb índex 5 de l'array, és la posició 6 (recordeu que el 0 és la primera posició de l'array) i en l'enter de la posició 6 n'augmentem el valor en una unitat.

#### Longitud
Al ser una estructura estàtica la **longitud** de l'array no es pot variar i es defineix quan es crea (amb el new). Per tal d'obtenir el seu valor en Java utilitzarem la propietat `length` de la classe Arrays:
```java
System.out.println("La longitud de l'array és " + array.length);
```
#### Una altra inicialització
Una altra manera d'inicialitzar un array és directament definint els seus elements:

```java
int[] array2 = {10, 20, 54, -2, 76 };
```

Si a aquest array2 imprimissim el seu valor de array2.length el resultat seria 5. De forma que s'hauria declarat i reservat la memòria directament.

#### Recorregut i manipulació d'arrays
Normalment ens trobarem amb problemes on cal accedir a arrays i efectuar-ne un tractament determinat. Per exemple, ens podríem trobar el següent problema:

> Com ho faríem per guardar en un array els 10 primers números parells?

```java
//declaració i creació de l'array					
int[] llista = new int[10];

//modificació el valor dels elements de l'array
for(int i=0; i<llista.length; i++) {
    llista[i] = i*2;
}	

//Imprimim els valors 0 2 4 6 8 10 12 14 16 18
for(int i=0; i<llista.length; i++) { System.out.print(llista[i] + " "); }
```

Es pot observar com mitjançant l'índex ``i`` s'accedeix a tots els elements de l'array i se'n va modificant el seu valor.

#### Ordenació arrays
Una altra funcionalitat corrent és l'ordenació d' arrays. En Java existeix una funció que ordena els elements d'un array, més endavant l'estudiarem amb deteniment.
```java
Arrays.sort(vector);
```

Existeixen molts algorismes diferents capaços d'ordenar els elements d'un array, tots ells tenen la seva lògica i obeeixen a casuïstiques diferents, i per tant també tenen costos de còmput diferent. En la següent web podrem observar simulacions de diferents algorismes en un llenguatge de pseudocodi i com evoluciona cada array fins a la seva ordenació:
[Visualgo](https://visualgo.net/es/sorting?slide=1)


#### Cerca d'un element dins l'array
La cerca d'un element dins un array és un problema típic. No és el mateix tenir l'array ordenat que l'array desordenat:
1. Si l'array està desordenat farem un recorregut buscant l'element, si no el troba s'arriba al final de l'array, si el troba sortim de l'array abans de la seva finalització.
2. Si l'array està ordenat, a diferència de l'anterior, no cal que busquem fins al final de l'array, un cop "em passi" de l'element que estic buscant ja no cal que continuï, és una manera d'optimitzar la cerca.


Cerca en array desordenat:
```java
double[] array = {2, 5.5, 9.1, 1, 2.9, 8, 5.5, 55.4, 2.6, 5.45, 7};

//Definim variable booleana per saber si s'ha trobat el valor
var trobat = false;

//Índex
var i = 0;

//Realitzem el recorregut, mentre no s’arriba al final i no es trobi un 1
while ((i < array.length) && (!trobat)) {
  if (array[i] == 8) {
    trobat = true;
  }
  i = i + 1;
}

//S’ha trobat?
System.out.println ( trobat ? "S'ha trobat l'element" : "NO s'ha trobat l'element");  
```

Una altra manera de fer el mateix problema però utilitzant la instrucció de salt `break` enlloc d'un booleà.

``` java
double[] array = {2, 5.5, 9.1, 1, 2.9, 8, 5.5, 55.4, 2.6, 5.45, 7};

//Índex
var i = 0;

//Realitzem el recorregut, mentre no s’arriba al final i no es trobi un 1
while ((i < array.length)) {
    if (array[i] == 8) {
        break;
    }
    i = i + 1;
}

//S’ha trobat?
System.out.println( i < array.length ? "S'ha trobat l'element" : "NO s'ha trobat l'element");
```


Cerca en array ordenat:
```java
double[] array = {2, 5.5, 8, 9.1, 10.4, 12.9, 18, 25.5, 55.4};

//Definim variable booleana per saber si s'ha trobat el valor
boolean trobat = false;

//Definim variable booleana per saber si ens hem passat ja de l'element
boolean passat=false;

//Índex
int i = 0;

//Realitzem el recorregut, mentre no s’arriba al final i no es trobi un 1
while ((i < array.length) && (!trobat) && (!passat)) {
  if (array[i] == 8) {
    trobat = true;
  }

  if (array[i] > 8) {
    passat = true;
  }
  i = i + 1;
}

//S’ha trobat?
String resposta = (trobat)? "S'ha trobat l'element" : "NO s'ha trobat l'element";
System.out.println(resposta);  
```

#### Bucle for millorat per arrays
Per tal d'efectuar el recorregut en un array java ens permet aquesta expressió reduïda de bucles for `foreach`. Per exemple, els bucles següents són equivalents:

```java
for(int i=0; i<array.length; i++) {
    int valor = array[i];
    System.out.println(valor);
}
for(int valor: array) {
    System.out.println(valor);
}
```

La versió adaptada del bucle for es pot fer servir amb qualsevol tipus d'array (String, int, boolean, etc.).

#### Altres mètodes útils de la classe java.util.Arrays

```java
Arrays.sort(array); // Ordena els elements
Arrays.equals(array1, array2); // Comprova si els dos arrays són iguals
Arrays.fill(array, val) //Omple el vector v amb el valor "val"
Arrays.toString(array)  // Retorna una cadena que representa el contingut del vector
Arrays.binarySearch(array, k) // Busca el valor k dins del vector array (que prèviament ha estat ordenat) 
```



#### Exemples
1. Exemple de diferents maneres per omplir de valors un array i imprimir-lo per línia de comandes:

```java
 //Crear Array
int primerArray[] = new int[7];

//Omplir de valors amb for i després amb while
for(int i=0; i < primerArray.length; i++){
    primerArray[i] = sc.nextInt();
}

var i=0;
while(i < primerArray.length){
    primerArray[i] = sc.nextInt();
    i++;
}

//Mostrar valors amb toString amb bucle for i bucle for millorat
Arrays.toString(primerArray);

for( i=0; i < primerArray.length; i++){
    System.out.println(primerArray[i]);
}

for( int valor : primerArray){
    System.out.println(valor);
}

//Ús de la funció fill de la classe Arrays que consisteix en omplir totes les posicions d'un array amb el mateix valor
Arrays.fill(primerArray,7);

for(i=0; i < primerArray.length; i++){
    primerArray[i] = 7;
}
```

2. Còpia d'arrays
```java
int[] llista = {1,2,3,4};
//llista i llistaCopia apunten al mateix array ja que són referències
int[] llistaCopia = llista; 

//Fent ús de clone. En aquest cas llista i llistaCopia SON DOS ARRAYS IGUALS I INDEPENDENTS
llistaCopia = llista.clone(); 

//còpia manual dels elements
int[] llistaCopia = new int[4]; 
for(i=0; i < llista.length; i++){
    llistaCopia[i] = llista[i];
}

System.out.println("Contingut de l'array 'llista'");
for(int valor : llista) System.out.println(valor);

System.out.println("Contingut de l'array 'llistaCopia'");
for(int valor : llistaCopia) System.out.println(valor);
```

3. Cerca d'un element dins un array (exemple del màxim)
```java
primerArray = new int[]{-1, -2, -3, -4};
var max = 0;
for(i=0; i < primerArray.length; i++){

    if(max<primerArray[i]) max = primerArray[i];
}
```

4. Sumar els elements d'un array valor a valor i guardar-lo en un altre array
```java
int vector1[] = new int[10];
int vector2[] = new int[10];

//falta introduir els valors en vector1 i vector2

int suma[] = new int[10];
for( i=0; i<suma.length;i++){
    suma[i] = vector1[i] + vector2[i];
}
```

5. Cerca dicotòmica 
```java
//Tamany vector
System.out.println("De quants elements vols el vector?");
var llargada = sc.nextInt();

//Creem i posem elements aleatoris entre 0 i 100 dins el vector i l'ordenem
int [] vector = new int[llargada];

for(int i=0; i<llargada;i++) 
  vector[i] = (int)(Math.random()*100);

Arrays.sort(vector);

//Imprimim vector
System.out.println(Arrays.toString(vector));

//Quin element vols buscar?
System.out.println("Quin element vols buscar?");
var nombreBuscat = sc.nextInt();

//inicialitzem index inferior i superior i declarem element central
var elementCentral;
var inferior=0;
var superior=llargada-1;

//inicialment no s'ha trobat l'element
var trobat = false;
var iteracions = 0;

//mentre element inferior no rebassi el superior continuem explorant
while(inferior<=superior && !trobat){

    //Augmentem nombre iteracions
    iteracions++;

    //busquem quin és l'element central
    elementCentral=(superior+inferior)/2;

    //Imprimim l'estat actual
    System.out.println(STR."Iteracio: \{iteracions} Inferior: \{inferior}   Superior: \{superior}   Element Central: \{vector[elementCentral]}  A buscar: \{nombreBuscat}");
    for(int i=inferior; i <= superior; i++) 
      System.out.print(vector[i]+" ");
    
    System.out.println("");
    System.out.println("");
     
    //Si el trobem posem trobat a true per sortir del bucle i anunciem que l'hem trobat
    if(vector[elementCentral]==nombreBuscat){
        trobat=true;
        System.out.println("L'element \{nombreBuscat} està dins l'array");
    }
    //Sinó actualitzem index, caldrà actualitzar o bé el superior en cas que el nombre buscat sigui inferior a l'actual, o bé l'inferior en cas contrari.
    else if(nombreBuscat < vector[elementCentral] ){
        superior=elementCentral-1;
    }
    else {
        inferior=elementCentral+1;
    }
}

//Si no el trobem ho anunciem
if(!trobat)System.out.println("L'element no es troba en el vector");



/**
*  Comparem amb...
*  CERCA LINEAL
*
**/
inferior=0;
superior=llargada-1;

//inicialment no s'ha trobat l'element
trobat = false;
iteracions = 0;

//mentre element inferior no rebassi el superior continuem explorant
while(inferior<=superior && !trobat) {

  //Augmentem nombre iteracions
  iteracions++;

  //Imprimim l'estat actual
  System.out.println(STR."Iteracio: \{iteracions} Inferior: \{inferior}   Superior: \{superior}   Element Central: \{vector[elementCentral]}  A buscar: \{nombreBuscat}");
  for (int i = inferior; i <= superior; i++) System.out.print(vector[i] + " ");
  System.out.println("");
  System.out.println("");

  //Si el trobem posem trobat a true per sortir del bucle i anunciem que l'hem trobat
  if (vector[inferior] == nombreBuscat) {
      trobat = true;
      System.out.println("L'element \{nombreBuscat} està dins l'array");
  }

  //Miro el següent element
  inferior++;

}

//Si no el trobem ho anunciem
if(!trobat)System.out.println("L'element no es troba en el vector");
```




