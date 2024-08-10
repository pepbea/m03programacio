---
title: StringBuilder
weight: 1
pre: "4.2. "
chapter: false
---

Com s'ha comentat anteriorment la classe String és una classe **immutable**, això des del punt de vista de l'eficiència a l'hora d'operar i manipular les cadenes de caràcters es planteja com un gran problema. Cada cop que manipulem una referència de String el que acaba succeïnt és que es crea una nova instància de String en la memòria Heap, no es modifica l'anterior, sinó que estem creant objectes nous per a cada modificació que realitzem, la qual cosa és mooolt costós en temps i en memòria.

Per això existeix les classes **StringBuilder**, i **StringBuffer**. Són classes que sí són **mutables**, per tant Sí permeten la modificació d'una cadena de caràcters **sense perdre eficència**, ja que no creen noves instàncies sinó que manipulen l'objecte actual.

La diferència entre StringBuilder i StringBuffer està en que **StringBuffer té els mètodes sincronitzats i, degut a això, és una mica més ineficient**. A mesura que desenvolupeu codi us adonareu que diferents programes (fils d'execució, threads) interactuaran de forma síncrona, per tal d'evitar problemes de sincronització de recursos compartits us serà necessari usar eines que evitin aquest problema, com per exemple StringBuffer, de moment, i donat que els mètodes són  els mateixos, utilitzarem StringBuilder. 

Com ja vam veure en l'AEA anterior, els objectes String es guarden en el **Constant String Pool**, que és un repositori de valors de Strings. La utilitat d'aquest Pool és que si creem altres Strings amb el mateix valor, no es crea un objecte nou en el Heap sinó que es "reutilitza" el valor que ja tenim en el Pool (recordem que String és immutable). Tant StringBuilder com StringBuffer emmagatzemen directament els objectes en el Heap.

#### Inicialització

Per tal d'inicialitzar un StringBuilder usarem aquestes tres formes, depenent de cada cas:

```java
//Construeix un StringBuilder buit i amb una capacitat de 16 caràcters
StringBuilder s = new StringBuilder();

//Construeix un StringBuilder buit i amb una capacitat de 25 caràcters
StringBuilder s = new StringBuilder(25);

//Construeix un StringBuilder en base a l'String passat com a paràmetre
StringBuilder s = new StringBuilder("Hola Món!");
```

#### Funcionalitats més habituals

El conjunt de funcionalitats complert el trobareu a Oracle a l'apartat de [StringBuilder](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/StringBuilder.html).


Passo a detallar aquelles funcionalitats més significatives, moltes funcionalitats són les mateixes que la classe String (charAt, indexOf, substring...):

**append**. Aquesta serà la funcionalitat més utilitzada, serveix per concatenar al final del StringBuilder una cadena de text determinada

```java
for(int i = 0; i < 1000; i++)
    stringBuilder.append(i);
```

**length()**. Caràcters amb informació útil en StringBuilder.
```java
    stringBuilder.length();
```

**capacity()**. Inicialment StringBuilder reserva una capacitat (espai per allotjar-hi caràcters). Si la informació que manipulem supera aquesta capacitat el que fa StringBuilder és crear una nova instància amb la capacitat necessària per encabir la informació sol·licitada. 
```java
    stringBuilder.capacity();
```

**toString()**. Converteix un StringBuilder a un String. Si volem mostrar el valor d'un StringBuilder serà necessari fer aquesta conversió per imprimir-lo per línia de comandes.
```java
    System.out.println(stringBuilder.toString());
```



#### Criteris per utilitzar String o StringBuilder/StringBuffer

1. Si el valor que assignem a les variables String no ha de variar (o varia poques vegades) utilitzarem la classe String.
2. Si el valor que assignem a les variables String varia un gran nombre de vegades i estem en un únic fil d'execució s'utilitzarà StringBuilder ja que és més eficient.
3. Si el valor que assignem a les variables String varia un gran nombre de vegades i estem en multitasca s'utilitzarà StringBuffer ja que és thread safe i per tant ens assegura un bon ús compartit de les dades entre els diferents fils d'execució.


#### Exemple d'ús i comparativa de temps

Posem per cas el següent exemple: "Donada una cadena, crea una altra cadena igual a la primera sense espais en blanc."
Es recomana provar el codi amb tamanys de text d'entrada MOOOLT diferents, d'aquesta forma permet apreciar les diferències alhora de manipular un String o un StringBuilder.

```java
//Opcio1: fent ús de replace()
System.out.println("Introdueix una cadena: ");
String cadena = sc.nextLine();

long startTime = System.currentTimeMillis();
System.out.println(cadena.replace(" ", ""));
long finalTime = System.currentTimeMillis();

System.out.println("AMB REPLACE");
System.out.println("Temps en trobar solucio: "+(finalTime-startTime));
System.out.println();

//Opcio2 sense fer ús de replace()
String paraules[] = cadena.split(" ");
String solucio = "";

startTime = System.currentTimeMillis();
for(String paraula : paraules){
    //solucio = solucio + paraula
    solucio += paraula;
}
finalTime = System.currentTimeMillis();

System.out.println(solucio);
System.out.println("STRING");
System.out.println("Temps en trobar solucio: "+(finalTime-startTime));
System.out.println();


//Opcio3 amb StringBuilder
String paraulesBuilder[] = cadena.split(" ");
StringBuilder solucioBuilder = new StringBuilder();

startTime = System.currentTimeMillis();
for(String paraula : paraules){
    solucioBuilder.append(paraula);
}
finalTime = System.currentTimeMillis();

System.out.println(solucioBuilder.toString());
System.out.println("STRINGBUILDER");
System.out.println("Temps en trobar solucio: "+(System.currentTimeMillis()-startTime));
```
