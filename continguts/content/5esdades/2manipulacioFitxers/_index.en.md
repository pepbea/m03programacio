---
title: Manipulació de fitxers
weight: 2
pre: "2. "
---

En Java, la manipulació de fitxers és un aspecte essencial de la programació, ja que sovint necessitem llegir, escriure i processar dades emmagatzemades en fitxers. Hi ha diferents tipus de fitxers (com ara fitxers de text i binaris), i també diferents maneres d’accedir-hi (seqüencial i aleatori)

En els següents apartats abordarem la manipulació de fitxers de caràcters, de fitxers binaris i veurem altres aspectes sobre la gestió de fitxers com el RandomAccessFile que ens permet un accés aleatori als fitxers. També veurem classes que treballen amb objectes i per tant veurem el procés de serialització i deserialització.


Les comunicacions entre diferents aplicacions i dispositius es vehiculen a través de flux de dades d'entrada/sortida.


#### Flux de dades

{{% notice note %}}
Un **flux de dades** és un conjunt seqüencial de bytes, com per exemple un fitxer, un dispositiu USB extern, una memòria, una API, etc. que normalment necessita gestionar l'entrada/sortida de dades.
{{% /notice %}}

Un flux és una entitat lògica de tot allò que produeix o consumeix informació. Java, com a llenguatge d'alt nivell i multiplataforma que és, s'ocupa de saber a qui cal demanar la informació en base a les especificacions que li indiquem. Serà el flux de dades el que hagi de comunicar-se amb el sistema operatiu i "saber" a on anar a buscar la informació. La nostra aplicació serà independent del sistema operatiu on s'apliqui i del dipositiu on estigui.

En Java, totes les classes que treballarem a partir d'ara estan incloses en l'especificació de [java.io](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/package-summary.html). Els fluxos de Java es poden classificar en fluxos d'entrada (`InputStreams`) o fluxos de sortida (`OutputStreams`). Els fluxos obeeixen al tipus de dades que tracten:

**1. Flux de caràcters (text pla)**
Aquests flux tracten caràcter, elements de 16 bits, s'utilitzen per treballar amb text entendible en el llenguatge  humà i existent dins algun sistema de codificació determinat: ASCI, ISO8859-1, etc. Normalment es treballarà amb la gestió de fitxers de text en aquests tipus de flux. 

En quan a les classes de Java que dónen cobertura hi ha `Reader i Writer`, aquestes classes gestionen fluxos de caràcters Unicode. Aquestes classes i les que hereden d'elles ajuden en la gestió de caràcters a nivell invidivual o col·lectiu (per exemple en la lectura d'un caràcter o la lectura d'una línia de text)

**2. Flux de bytes (8bits)**

En aquest cas, les classes que treballen en bytes entenen que la informació emmagatzemada es tracta a partir de bytes, la màquina identifica fitxers binaris, com per exemple: imatges, arxius executables, etc. Les classes abstractes que Java li dóna cobertura són `InputStream i OutputStream`. Les subclasses d'aquesta classe són les que implementaran funcions com read() write() que ajuden en el maneig de fitxers binaris.

**Wrappers**
Cal destacar que en la lectura/escriptura d'un flux de dades, hi ha classes que s'embolcallen dins d'altres classes per millorar-ne l'eficiència. Per exemple en un flux de caràcters existeix la classe Reader o la classe FileReader que ens permet llegir un text provinent d'un fitxer caràcter a caràcter, el fet *"d'embolcallar"* aquesta classe dins un BufferedReader li permet llegir línies de text directament. De forma que en cada accés de lectura, enlloc de llegir un sol caràcter, llegeix tota la línia, amb la millora d'eficiència que suposa accedir moltes menys vegades per llegir el mateix text.

#### Entrada i sortida estàndard

Java té accés a l'entrada/sortida estàndard a través de la classe System. En concret:

**1. Stdin.System.in** és un objecte de tipus InputStream, y està definit a la clase System com un flux d'entrada estàndard. Per defecte és el teclat, però pot redirigir-se a qualsevol altre dispositiu d'entrada.

**2. Stdout.System.out** implementa stdout com una instància de la classe PrintStream. Normalment s'utilitzen els mètodes print() y println().

**3. Stderr.System.err** és un objecte de tipus PrintStream. És un flux de sortida definit a la classe System i representa la sortida d' error estàndard. Per defecte, és el monitor, encara que es pot redireccionar a qualsevol altre dispositiu de sortida.

#### Procés d'utilització d'un fitxer en Java

Depenent de si llegeixo un document de text o un document binari utilitzaré unes classes o altres. Els passos que segur necessitaràs fer per realitzar qualsevol tractament del fitxer són els següents:

1. __*Importar els paquets necessaris*__ per treballar amb fitxers (java.io o java.nio).
2. __*Crear un objecte File*__: Per obrir el fitxer primer creem un objecte File que ens indica la posició d'aquest fitxer dins el sistema d'arxius. 
3. __*Obrir el fitxer*__: A continuació i depenent del tipus de dades que es volen llegir (text o binari) obrirem el fitxer amb una classe determinada o una altra.
4. __*Llegir o escriure dades*__: Tot seguit utilitzarem els mètodes proporcionats per les classes amb les que hem obert el fitxer per duu a terme el nostre propòsit de Lectura/Escriptura.
5. __*Tancar el fitxer*__: Després de llegir o escriure, és important tancar el fitxer per alliberar recursos i evitar possibles pèrdues de dades.


#### Excepcions en la manipulació de fitxers

És important gestionar les excepcions en els processos de E/S en el tractament de fitxers, cal controlar:

- Fitxers inexistents `FileNotFoundException`
○ Fallades d'E/S `IOException`
○ Incoherències de tipus quan es fa servir Scanner `InputMismatchException`