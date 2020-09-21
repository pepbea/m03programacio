---
title: Tractament cadena de caràcters
weight: 3
---

{{% notice note %}}
Un **String** és una classe que permet treballar amb cadenes de caràcters. La classe String de Java ens dóna moltes funcionalitats que ens permeten realitzar moltes tasques d'una forma senzilla.
{{% /notice %}}

La funció sobre la classe String la trobareu a:
[Java Oracle Classe String](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html)

##### Inicialització

La manera de declarar i inicialitzar aquest objecte és com en els tipus primitius. Amb la variable String diem que la variable str i strBuit emmagatzemen un String i a continuació s'hi assigna un valor. En el cas del valor ``""`` assignem un String buit.

```java
String str = "El primer string";
String strBuit = "";
```

##### Funcionalitats interessants

```java
/*
longitud del string
STR.LENGTH()
*/
System.out.println("longitud " + str.length());

/*
Caràcter en la posició pos de str.
STR.CHARAT(int)
*/
str = "El primer programa";
System.out.println("En la posició 4 hi ha: " + str.charAt(4));
System.out.println("En la posició 11 hi ha: " + str.charAt(11));

/*
Comença o acaba l'string en...
STARTSWITH OR ENDSWITH
*/
str = "El primer programa";
System.out.println("comienza por El      " + str.startsWith("El"));
System.out.println("termina por programa " + str.endsWith("programa"));

/*
Posició d'un caràcter dins un string
STR.INDEXOF('x')

Ocurrència a partir d'un cert caràcter
STR.INDEXOF('x', pos)
*/
int pos = str.indexOf('p');
System.out.println("posición de la letra p " + pos);

//segona ocurrencia de p
pos = str.indexOf('p', pos + 1);


/*
Comparació entre dos strings
STR.COMPARETO(STRING2)
*/
str = "Pep";

System.out.println("Orden alfabético " + str.compareTo("Xavi"));
System.out.println("Orden alfabético " + str.compareTo("Gines"));
System.out.println("Orden alfabético " + str.compareTo("Pep"));

/*
Substring amb UNA variable posicioInicial indica a a partir de quin caràcter volem recollir el substring fins al final.
STR.SUBSTRING(posicioInicial)

Substring amb Dues variables determinen quin substring obtindrem entre les dues posicions
STR.SUBSTRING(posicioInicial, posicioFinal)
*/
str = "El lenguaje Java";
System.out.println("Substring " + str.substring(12)); //Java
System.out.println("Substring " + str.substring(3, 11));  //lenguaje

/*
Eliminar espais en blanc
STR.TRIM()
*/
str = "                12             ";
System.out.println("string original               :" + str);
System.out.println("string sin espacios en blanco :" + str.trim());

/*
Convertir array a String
ARRAYS.TOSTRING(array)
*/
int[] arrayNumeric = {24, 2, 4, -12};
System.out.println("número --> string " + Arrays.toString(arrayNumeric));

/*
Convertir strings a enters i decimals
INTEGER.PARSEINT(str.TRIM());
DOUBLE.VALUEOF(str).DOUBLEVALUE();
*/
str = "12";
int numeroInt = Integer.parseInt(str.trim());
System.out.println("string --> número " + numeroInt);
str = "12.35 ";
double numeroDouble = Double.valueOf(str).doubleValue();
System.out.println("string --> número " + numeroDouble);

/*
Separar String en diferents cadenes
str.SPLIT(" "); --> Separa les diferents paraules per espais
*/
String cadena = "Hola que tal com estas";
String[] vectorSeparat = cadena.split(" ");
for (String a : vectorSeparat) System.out.println(a);

/*
EXEMPLE D'ÚS: De cada alumne volem obtenir el nom amb el format correcte i el dni.
*/
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
