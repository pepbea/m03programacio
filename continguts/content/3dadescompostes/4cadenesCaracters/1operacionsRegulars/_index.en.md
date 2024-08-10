---
title: Operacions Regulars
weight: 1
pre: "4.1. "
chapter: false
---

{{% notice note %}}
Una **expressió regular (regex)** és la representació d'un patró alhora de buscar una seqüència de caràcters en un text.
{{% /notice %}}

El patró de cerca pot anar des d'un caràcter, un string fixat o una expressió complexa de diferents caràcters especials.

L'avaluació d'un patró o d'una expressió regex sempre serà d'esquerra a dreta. Pot ser que es trobi una ocurrència com a resultat, que no en trobi cap o que en trobi més d'una.

#### Com aplicar-ho des de Java

Ens podria interessar que:
1. Si **un text complert** s'identifica amb un patró fixat, en aquest cas usarem `Pattern.matches(regex, string);` -> Retorna un booleà.
2. Si **una part del text** compleix el patró, o si hi ha més d'una ocurrència que compleixi amb el patró fixat, en aquest cas usarem `Pattern.compile(regex).matcher(string).find()`

Un exemple de com podríem trobar quines paraules existeixen dins un text:

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class Main {
    public static void main(String[] args) {

        Pattern myPattern = Pattern.compile("\\w+");
        Matcher myMatcher = myPattern.matcher("Hola Mon!");
        
        while (myMatcher.find()) {
            System.out.println("Trobat: " + myMatcher.group() + " a: " + myMatcher.start() + "," + myMatcher.end());
        }
    }
}
```

Com es pot observar en l'exemple anterior `Pattern.compile("\\w+")` defineix el patró de cerca en el qual s'identifiquen totes aquelles seqüències de caràcters que són **W**ords, "\\w+" busca seqüències de caràcters dins el text que coincideixi amb el patró `[a-zA-Z_0-9]+`. 

Un cop definit el *Pattern* el que fem és cridar la funció matcher que s'encarrega d'enllaçar el patró amb el text on estic buscant i el resultat queda en un objecte Matcher que ja puc iterar si és el cas (find/group).

Quan la totalitat del text encaixa amb el patró utilitzaríem la funció `matches` de Pattern:

```java
Pattern.matches(PATRO_DEFINIT, TEXT_A_BUSCAR); //Retorna True/False

Pattern.matches("\\d{5}", "56745"); //TRUE
Pattern.matches("\\d{5}", "56745d"); //FALSE
```

Per veure la diferència entre Pattern.matches() o Pattern.compile().matcher().find(). En el següent exemple, si busquem amb el mateix patró en el mateix text, observem com el primer cas ens retorna TRUE mentre que el segon ens retorna FALSE, ja que el patró encaixa amb una subcadena del text, no en la seva totalitat.

```java
Pattern.compile("HOLA").matcher("HOLA MON!").find()  //True
Pattern.matches("HOLA", "HOLA MON!");  //False
```

{{% notice note %}}
En la pròpia pàgina de la classe Pattern de l'API de Java Oracle observareu quins són els caràcters especials i com es poden conformar diferents tipus de patrons
[java.util.regex.Pattern](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/regex/Pattern.html).
{{% /notice %}}


#### Exemples d'ús

Saber si una data està en el format correcte.
```java
String literalMonthRegexp = "\\d{1,2}/(?i)(gener|febrer|març|abril|maig|juny|juliol|agost|setembre|octubre|novembre|desembre)/\\d{4}";

//TRUE
System.out.println(Pattern.matches(literalMonthRegexp, "15/maig/2024"));
System.out.println(Pattern.matches(literalMonthRegexp, "8/abril/2021"));
System.out.println(Pattern.matches(literalMonthRegexp, "7/juny/2023"));   

//FALSE
System.out.println(Pattern.matches(literalMonthRegexp, "11/abc/2024"));
System.out.println(Pattern.matches(literalMonthRegexp, "11//2024"));
System.out.println(Pattern.matches(literalMonthRegexp, "7/juny/2023joan"));   
```

Validar que un dni contingui 8 nombres i una lletra de DNI.
```java
String dniRegexp = "\\d{8}[A-HJ-NP-TV-Z]";

System.out.println(Pattern.matches(dniRegexp, "56453453C"));  //TRUE

System.out.println(Pattern.matches(dniRegexp, "01234567U")); // FALSE, U no vàlida
System.out.println(Pattern.matches(dniRegexp, "0123567X")); // FALSE no conté 8 dígits
```

Validar el format d'un email
```java
String entrada = "<p>malvarez@iespoblenou.org</p><br>\n";

Pattern limpiar = Pattern
        .compile("([a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\\.[a-zA-Z0-9-]+)*)");
Matcher buscar = limpiar.matcher(entrada);
while (buscar.find())
    System.out.println(buscar.group(1));
```