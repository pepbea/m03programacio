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
1. Si **un text complert** s'identifica amb un patró fixat, en aquest cas usarem `Pattern.matches(regex, string)` -> Retorna un booleà.

```java
Pattern.matches(PATRO_DEFINIT, TEXT_A_BUSCAR); //Retorna True/False

Pattern.matches("\\d{5}", "56745"); //TRUE
Pattern.matches("\\d{5}", "56745d"); //FALSE
```

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

##### Diferència entre Pattern.matches() i Pattern.compile().matcher().find()

Per veure la diferència entre Pattern.matches() o Pattern.compile().matcher().find() obsrvarem el següent exemple. Si busquem amb el mateix patró en el mateix text, observem com enel primer cas ens retorna FALSE mentre que el segon ens retorna TRUE, ja que el patró encaixa amb una subcadena del text, no en la seva totalitat.

```java
Pattern.matches("HOLA", "HOLA MON!");  //False
Pattern.compile("HOLA").matcher("HOLA MON!").find()  //True
```

{{% notice note %}}
En la pròpia pàgina de la classe Pattern de l'API de Java Oracle observareu quins són els caràcters especials i com es poden conformar diferents tipus de patrons
[java.util.regex.Pattern](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/regex/Pattern.html). Requereix de molta pràctica i molts exemples per dominar-ho.
{{% /notice %}}

[Tutorial de Regex de Java Oracle](https://docs.oracle.com/javase/tutorial/essential/regex/)


#### Exemples d'ús

1. Saber si una data està en el format correcte.
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

2. Validar que un dni contingui 8 nombres i una lletra de DNI.
```java
String dniRegexp = "\\d{8}[A-HJ-NP-TV-Z]";

System.out.println(Pattern.matches(dniRegexp, "56453453C"));  //TRUE

System.out.println(Pattern.matches(dniRegexp, "01234567U")); // FALSE, U no vàlida
System.out.println(Pattern.matches(dniRegexp, "0123567X")); // FALSE no conté 8 dígits
```

3. Validar el format d'un email
```java
String entrada = "<p>malvarez@iespoblenou.org</p><br>\n";

Pattern netejar = Pattern
        .compile("([a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\\.[a-zA-Z0-9-]+)*)");
Matcher buscar = limpiar.matcher(entrada);
while (buscar.find())
    System.out.println(buscar.group(1));
```

4. Validar un nombre de telèfon fix, com per ex: 932-234-235.
```java
String patroTelefon = "\d{3}-\d{3}-\d{3}";

//TRUE
System.out.println(Pattern.matches(patroTelefon, "932-234-235"));
System.out.println(Pattern.matches(patroTelefon, "666-666-666"));

//FALSE
System.out.println(Pattern.matches(patroTelefon, "932-aaa-235"));
System.out.println(Pattern.matches(patroTelefon, "32-34-25"));
```

5. Validar una IP.
```java
String patroIp = "\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}";

//TRUE
System.out.println(Pattern.matches(patroIp, "192.168.1.1"));
System.out.println(Pattern.matches(patroIp, "192.168.1.111"));

//FALSE
System.out.println(Pattern.matches(patroIp, "4444.3.2.3"));
System.out.println(Pattern.matches(patroIp, "123.123.123"));
```

6. Validar una IP dins un rang determinat. Per exemple entre 192.168.1.1 i 192.168.1.255
```java
String patroIpPrivada = "^192\.168\.1\.(\d|[1-9]\d|1\d\d|2([0-4]\d|5[0-5]))$";

//TRUE
System.out.println(Pattern.matches(patroIpPrivada, "192.168.1.1"));
System.out.println(Pattern.matches(patroIpPrivada, "192.168.1.111"));

//FALSE
System.out.println(Pattern.matches(patroIpPrivada, "192.168.2.1"));
System.out.println(Pattern.matches(patroIpPrivada, "192.168.1.256"));
```

7. Quantes vegades apareix la paraula completa DAM en un text (sense que sigui subcadena d'una altra paraula).
```java
final String PATRO_DAM = "\\bDAM\\b";

Pattern myPattern = Pattern.compile(PATRO_DAM);
Matcher myMatcher = myPattern.matcher("Estic cursant DAM i m'agrada molt DAM, espero poder aprovar DAM.");
var count = 0;

while (myMatcher.find()) count++;

System.out.println("La paraula 'DAM' apareix " + count + " vegades en el text.");
```

8. Validar si una contrassenya conté de 8 a 16 caràcters alfanúmerics 
```java
String patroPassword = "^[a-zA-Z0-9]{8,16}$";

//TRUE
System.out.println(Pattern.matches(patroPassword, "poblenou"));
System.out.println(Pattern.matches(patroPassword, "1N5T1TUTPOBL3N01"));

//FALSE
System.out.println(Pattern.matches(patroPassword, "poblenou_"));
System.out.println(Pattern.matches(patroPassword, "InstitutPoblenouBarcelona"));
```

9. Comprovar si una cadena conté un caràcter especial
```java
String patroPassword = "[^a-zA-Z0-9]";

//TRUE
System.out.println(Pattern.matches(patroPassword, "Hola$ComEstas"));
System.out.println(Pattern.matches(patroPassword, "AquestTextConteCaracterEspecial*#"));

//FALSE
System.out.println(Pattern.matches(patroPassword, "HolaComEstas"));
System.out.println(Pattern.matches(patroPassword, "AquestTextNoConteCaracterEspecial012345789"));
```

10. Trobar els hashtags en un text de xarxes socials
```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class Main {
    public static void main(String[] args) {

        Pattern myPattern = Pattern.compile("#\\w+");
        Matcher myMatcher = myPattern.matcher("#DAMMola #InstitutPoblenou #INSPoblenou #ExpressionsRegulars");
        
        while (myMatcher.find()) {
            System.out.println("Trobat: " + myMatcher.group() + " a: " + myMatcher.start() + "," + myMatcher.end());
        }
    }
}
```

