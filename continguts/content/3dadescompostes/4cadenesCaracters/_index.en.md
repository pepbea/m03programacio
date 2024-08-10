---
title: Tractament cadena de caràcters
weight: 4
pre: "4. "
---

{{% notice note %}}
Un **String** és una classe que permet treballar amb cadenes de caràcters. La classe String de Java ens dóna moltes funcionalitats que ens permeten realitzar moltes tasques d'una forma senzilla. 
{{% /notice %}}

La funció sobre la classe String la trobareu a:
[Java Oracle Classe String](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html)

#### Immutable

És important destacar que la classe String és **immutable**. Això vol dir que un cop en definim un valor no es pot tornar a modificar. Sembla estrany, ja que si en el codi assignem un nou valor a la mateixa variable observem com es guarda correctament. Bé, el que passa exactament és que String no és una classe primitiva de Java, això vol dir que quan declaro una variable `String` el que faig realment és crear una referència de memòria (es guarda en la pila del meu programa que s'executa), quan a aquesta variable li assigno un valor, aquest és en sí un Objecte String (es guarda en el Heap de la memòria), de forma que si torno a guardar un valor en la mateixa referència de memòria **no li estic modificant el valor a l'objecte original, sinó que assigno la variable String a un altre objecte** (Immutabilitat).

#### Inicialització

La manera de declarar i inicialitzar aquest objecte és com en els tipus primitius. Amb la variable String diem que la variable str i strBuit emmagatzemen un String i a continuació s'hi assigna un valor. En el cas del valor ``""`` assignem un String buit. Per mostrar-ne el contingut, igual que en les classes primitives, fem ús de System.out.println.

```java
String str = "El primer string";
String strBuit = "";
System.out.println(str);
```

De la mateixa manera que qualsevol altre objecte es podria crear un String de la següent manera utilitzant `new`.
```java
String str = new String ("El primer string");
```

#### Funcionalitats interessants

**Longitud** d'un String
```java
System.out.println("longitud " + str.length());
```

**Concatenació** de Strings
```java
String primeraPart = "Hola";
String segonaPart = " ";
String terceraPart = "Mon!";
String total = primeraPart + segonaPart + terceraPart;
System.out.println(total);
```

Conèixer el contingut d'una determinada posició dins l'String. (**charAt**)
```java
str = "El primer programa";
System.out.println("En la posició 4 hi ha: " + str.charAt(4));
System.out.println("En la posició 11 hi ha: " + str.charAt(11));
```

Creació d'una subcadena (**substring**) a partir d'una cadena original. La primera opció crea una subcadena nova des de la posició indicada fins al final del String str. La segona opció crea una subcadena des de la posició inicial fins a la posició final.
```java
str.substring(posicioInicial)
str.substring(posicioInicial, posicioFinal)

str = "El primer programa";
System.out.println("Substring " + str.substring(12)); //Java
System.out.println("Substring " + str.substring(3, 11));  //lenguaje
```

Saber si l' **inici o final d'un String comença o acaba**  amb una determinada subcadena.
```java
str = "El primer programa";
System.out.println("comienza por El      " + str.startsWith("El"));
System.out.println("termina por programa " + str.endsWith("programa"));
```

Conèixer la posició d'un determinat caràcter o seqüència de caràcters dins una cadena. (**indexOf**). Si la funció porta dos arguments, el segon paràmetre indica a partir de quina posició comença la cerca. 
```java
str = "El primer programa";

//Comença a buscar 'x' dins str des de la posició 0
str.indexOf('x')

//Comença a buscar 'x' dins str des de la posició pos
str.indexOf('x', pos)

int pos = str.indexOf('p');
System.out.println("posició de la lletra p " + pos);

//segona ocurrencia de p
pos = str.indexOf('p', pos + 1);

//també permet buscar cadenes de caràcters
int pos = str.indexOf("El");
System.out.println("posició de la subcadena \"EL\" " + pos);

int pos = str.indexOf("pr", 7);
System.out.println("posició de la subcadena \"pr\" a partir de la posició 7: " + pos);


```

Comparació de dos Strings (**compareTo**). Compara lexicogràficament dos cadenes de caràcters, i extreu com a resultat -1 0 1 depenent de quin String estigui per davant, si el primer, el segon o tenen el mateix valor lexicogràfic, per tant 0.
```java
str = "Pep";
System.out.println("Orden alfabético " + str.compareTo("Xavi"));
System.out.println("Orden alfabético " + str.compareTo("Gines"));
System.out.println("Orden alfabético " + str.compareTo("Pep"));
```

Elimina espais (**trim**) a l'inici o final de la cadena de caràcters.
```java
str = "                12             ";
System.out.println("string original               :" + str);
System.out.println("string sin espacios en blanco :" + str.trim());
```

Convertir un Array a String (**toString**).
```java
int[] arrayNumeric = {24, 2, 4, -12};
System.out.println("número --> string " + Arrays.toString(arrayNumeric));
```

Convertir Strings a enters i decimals

```java
INTEGER.PARSEINT(str.TRIM());
DOUBLE.VALUEOF(str).DOUBLEVALUE();

str = "12";
int numeroInt = Integer.parseInt(str.trim());
System.out.println("string --> número " + numeroInt);
str = "12.35 ";
double numeroDouble = Double.valueOf(str).doubleValue();
System.out.println("string --> número " + numeroDouble);
```

Separar String en diferents cadenes (**split**)
```java
//Separar les diferents paraules per espais
str.SPLIT(" "); 

String cadena = "Hola que tal com estas";
String[] vectorSeparat = cadena.split(" ");
for (String a : vectorSeparat) System.out.println(a);
```

**EXEMPLE D'ÚS**: De cada alumne volem obtenir el nom amb el format correcte i el dni.
```java
String alumnes = "" +
        "Nom; Cognoms; DNI\n" +
        "xavi; sanChO; 111111a\n" +
        "pep; beÀ; 222222b\n";

String[] rows = alumnes.split("\n");

for (int i = 1; i < rows.length; i++) {
    String[] dades = rows[i].split(";");

    String nom = dades[0];
    String cognoms = dades[1];

    String nomComplet = nom + " " + cognoms;

    String[] partsNom = nomComplet.split(" ");

    String capitalitzat = "";

    for (String part : partsNom) {
        String senseEspais = part.trim();

        if (!senseEspais.equals("")) {
            String inicial = part.substring(0, 1).toUpperCase();

            String resta = part.substring(1).toLowerCase();

            capitalitzat += inicial + resta + " ";
        }

    }

    System.out.println(capitalitzat);
    String dni = dades[2].trim();

    System.out.println(dni);
}
```
