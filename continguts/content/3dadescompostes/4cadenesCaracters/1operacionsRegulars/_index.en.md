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

Com es pot observar en l'exemple anterior `Pattern.compile("\\w+")` defineix el patró de cerca en el qual s'identifiquen totes aquelles seqüències de caràcters que són **W**ords, això  el que fa és buscar seqüències de text dins el text a buscar que coincideixi amb el patró `[a-zA-Z_0-9]+`. 

Un cop definit el *Pattern* el que fem és cridar la funció matcher que s'encarrega d'enllaçar el patró amb el text on estic buscant i el resultat queda en un objecte Matcher que ja puc iterar si és el cas.

En la pròpia pàgina de Pattern de l'API de Java Oracle observareu quins són els caràcters especials i com es poden conformar diferents tipus de patrons
[java.util.regex.Pattern](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/regex/Pattern.html).

