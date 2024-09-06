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

Des de Java 8 amb la introducció de les expressions lambda i de les [API_Streams](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/stream/package-summary.html), Java permet el processament de fluxos que permet l'encadenament d'operacions en un conjunt de dades.

Aquesta API permet integrar el paradigma funcional a les funcionalitats típiques que realitzem en les col·leccions, com són:
* Filtrar
* Transformar
* Reduir
* Agrupar 
* Ordenar 

{{% notice note %}}
**Fluxos - Streams**. Els fluxos d'elements permeten el processament en paral·lel o seqüencial dels elements d'una col·lecció. En les col·leccions de java per crear un flux en una estructura de dades d'una col·lecció tenim la funció *.stream()*, també podem crear streams a partir d'arrays o a partir dels valors de la seqüència.
{{% /notice %}}

```java
List<String> noms = Arrays.asList("Pep", "Alberto", "Susana", "Maria");
Stream<String> flux = noms.stream();

String[] nomsArray = new String[]{"Pep", "Alberto", "Susana", "Maria"};
Stream<String> flux = Arrays.stream(nomsArray);

Stream<String> flux = Stream.of("Pep", "Alberto", "Susana", "Maria");
```

#### Operacions

En l'API de Streams existeixen dos tipus de funcions, *les Intermitges i les Terminals*. Les operacions que s'apliquen als Streams no modifiquen la font de les dades, promouen la immutabilitat respecte les estructures originals.

L'execució de les diferents funcions contingudes en un Stream aplica el que s'anomena com a `Lazyness`: les operacions s'executen al final i el més tard possible. **Una funció terminal activa les funcions intermitges del flux de dades.** Normalment un Stream es crea, es composa de diferents funcions  intermitges i finalment una funció terminal, no hi poden haver dues funcions terminals.

Molta de l'operativitat de les funcions agregades segueix el que es denomina com a **Filter-Map-Reduce**: Funcionalitat de sel·leccionar dades en base a una condició (filter), transformar les dades (map), combinar aquestes dades per obtenir un resultat (reduce).


#### Operacions Intermitges

Les operacions intermitges retornen un nou Stream, es poden encadenar diferents funcions intermitges. (Recordeu que per ser activades necessiten una operació terminal). Algunes funcions intermitges són:

* map()
* filter()
* distinct()
* sorted()
* limit()
* peek()
* skip()


**MAP()**
La funció .map() ens ajuda a transformar totes les dades d'una col·lecció, per a fer-ho utilitzarem una funció lambda. Quan tractem de dades numèriques també podem usar mapToInt o mapToDouble.

Per exemple, suposem la classe Persona amb un atribut que sigui l'edat. Ens agradaria sumar les edats d'una col·lecció de persones:
```java
int total = lista.stream()
                 .mapToInt(Persona::getEdat)
                 .sum();

System.out.println(total);
```

Un altre exemple podria ser obtenir els quadrats dels 10 primers nombres, ho farem usant la funció lambda `n -> n*n`
```java
List<Integer> nombres = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

List<Integer> quadrats = nombres.stream()
                                .map(n -> n * n)
                                .collect(Collectors.toList());
```


**FILTER()**
L'operació .filter() ens serveix per obtenir un nou Stream amb aquells elements que han passat una condició, per definir aquesta condició utilitzarem Predicats que normalment es definiran com expressions lambda. Si el Predicat s'avalua a `true` aquest element formarà part del nou Stream, en cas contrari, serà rebutjat.

Aquest és un exemple senzill que mostra com filtrar aquells elements parells:
```java
List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Integer> streamNumerosPars = numeros.stream()
                                           .filter(numero -> numero % 2 == 0);

streamNumerosPars.forEach(System.out::println);
```

Permet combinar diferents filtres en una mateixa seqüència Stream:
```java
List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Integer> streamNumerosParsMenorsQue5 = numeros.stream()
                                           .filter(numero -> numero % 2 == 0);
                                           .filter(numero -> numero < 5);
streamNumerosParsMenorsQue5.forEach(System.out::println);
```

Ens permet també treballar amb objectes, per exemple si volguéssim filtrar aquelles persones majors d'edat:

```java
Stream<Persona> streamPersonesMajorsEdat = persones.stream()
                                        .filter(persona -> persona.getEdad() >= 18);
streamPersonesMajorsEdat.forEach(System.out::println);
```

Observarem un exemple de filtrar un String d'un array d'Strings des de dos visions molt diferents. Comencem fent ús dels Streams.

```java
List<String> colors = Arrays.asList("blau", "vermell", "groc");
List<String> colorBlau = colorCars.stream()               
        .filter(color -> "blau".equals(color))     
        .collect(Collectors.toList());             
```

Aquest mateix exemple si el volguéssim fer utilitzant bucles veuríem:
```java
public class AbansStreams {
    public static void main(String[] args) {
        List<String> colors = Arrays.asList("blau", "vermell", "groc");
        List<String> colorsFiltre = getColorBlue(colors);
        for (String color : colorsFiltre) {
            System.out.println(color);    
        }
    }
    private static List<String> getColorBlue(List<String> colors) {
        List<String> colorsFiltrats = new ArrayList<>();
        for (String color : colors) {
            if ("blue".equals(color)) { 
                colorsFiltrats.add(color);
            }
        }
        return colorsFiltrats;
    }
}          
```
Observeu el canvi significatiu en quan a simplicitat i legibilitat de codi. Fixeu-vos també com en el primer exemple s'explica **QUÈ FA EL CODI** més propi d'un sistema de programació funcional (`llenguatge declaratiu`), mentre que el segon exemple es descriu **COM HO FA EL CODI**, més propi d'un `llenguatge imperatiu`.


#### Operacions Terminals

**Són funcions que NO RETORNEN UN STREAM, sinó que RETORNEN UN VALOR PRIMITIU, COL·LECCIÓ O OBJECTE** Les operacions terminals NO PODEN SER encadenades (les operacions intermitges SÍ). Algunes de les operacions terminals són:

* forEach()
* toArray()
* reduce()
* collect()
* min(), max(), count()
* anyMatch(), allMatch(), noneMatch() 
* findFirst(), findAny()

**FOREACH()**
Ens permet iterar tots els elements d'un Stream.

```java
public static void main(String[] args) {
    List<String> names = Arrays.asList("Pep", "Alberto", "Gines");
    names.stream().forEach(System.out::println);
}
```

**REDUCE()**
Executa una operació sobre els elements d'un Stream per tal de produir un resultat final. Per exemple la concatenació de Strings:

```java
List <String> nombres = Arrays.asList("Pep", "Alberto", "Gines");
String reduce = nombres
    .stream()
    .reduce(String::concat)
    .ifPresent(System.out::println);
```

Un altre exemple on fent ús de reduce extraiem el nom més llarga:
```java

List<String> noms = Arrays.asList("Pep", "Alberto", "Gines", "Carles", "Ramon Maria");

Optional<String> nomMesLlarg = words.stream()
    .reduce((nom1, nom2) -> nom1.length() > nom2.length() ? nom1 : nom2);

nomMesLlarg.ifPresent(System.out::println); 
```

**COLLECT()**
Són estructures modificables que reben els elements d'un Stream i construeix el resultat que necessitem, per exemple es poden dipositar en Sets, Maps, o Lists. Per a tal fet  ja existeixen uns collectors predefinits:
* Collector.toList()
* Collectors.toSet()
* Collectors.toMap()

Si volem saber quines paraules d'una llista contenen la paraula "DAM":
```java
public List<String> getDamWords(Stream<String> words) {
  List<String> damWords = words
      .filter(word -> word.contains("DAM"))
      .collect(Collectors.toList());
  return damWords;
}
```

#### Per acabar

Una de les avantatges dels Streams respecte a l'execució seqüencial que ens ofereixen les col·leccions és que en operacions que requereixen d'una gran capacitat de còmput permet realitzar l'execució del càlcul en paral·lel a diferents parts de la col·lecció al mateix temps (particiona la col·lecció per tal de realitzar les operacions en paral·lel), reduint així el temps de còmput global i fent més eficient l'aplicació. S'utilitza en aquest cas la classe `ParallelStream`, a 2n DAM ho veureu més extensament en el mòdul de Serveis i Processos Concurrents.

#### Alguns exemples

1. Suma els elements parells d'un llistat:

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

int sumOfEvens = numbers.stream()
    .filter(n -> n % 2 == 0)
    .mapToInt(Integer::intValue)
    .sum();

System.out.println(sumOfEvens); 

```

2. Compta el nombre de paraules del llistat que la longitud sigui superior a 4.

```java
List<String> words = Arrays.asList("Apple", "Banana", "Avocado", "Kiwi");

long count = words.stream()
    .filter(w -> w.length() > 4)
    .count();

System.out.println(count); 
```

3. Busca la mitjana dels nombres superiors a 5.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 6, 7, 8);

OptionalDouble average = numbers.stream()
    .filter(n -> n > 5)
    .mapToInt(Integer::intValue)
    .average();

average.ifPresent(System.out::println);
```

Tenint en compte que tenim una classe Person amb els atributs (name, age i country):

4. Suma les edats de totes les persones d'un determinat país.
```java
List<Person> people = Arrays.asList(
    new Person("Alice", 30, "USA"),
    new Person("Bob", 25, "Canada"),
    new Person("Charlie", 35, "USA")
);

int sumOfAgesFromUSA = people.stream()
    .filter(p -> p.getCountry().equals("USA"))
    .mapToInt(Person::getAge)
    .sum();

System.out.println(sumOfAgesFromUSA);
```

5. Troba a la persona més jove d'un determinat país.
```java
List<Person> people = Arrays.asList(
    new Person("Alice", 30, "USA"),
    new Person("Bob", 25, "USA"),
    new Person("Charlie", 35, "Canada")
);

Person youngestInUSA = people.stream()
    .filter(p -> p.getCountry().equals("USA"))
    .reduce((p1, p2) -> p1.getAge() < p2.getAge() ? p1 : p2)
    .orElse(null);

System.out.println(youngestInUSA); 
```
6. Compta el nombre de persones d'un determinat país.
```java
List<Person> people = Arrays.asList(
    new Person("Alice", 30, "USA"),
    new Person("Bob", 25, "USA"),
    new Person("Charlie", 35, "Canada")
);

long countFromUSA = people.stream()
    .filter(p -> p.getCountry().equals("USA"))
    .count();
```

