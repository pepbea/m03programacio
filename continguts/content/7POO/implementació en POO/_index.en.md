---
title: Implementació bàsica de POO
weight: 2
---


#### Definicions

| | |
|---|---|
|Classe<br><br><br><br><br>|**Una classe és la definició d'un objecte real.**<br><br>És l'element que descriu els components d'un objecte de manera general. En ell hi queden especificats quines característiques té l'objecte (atributs) i quines accions pot realitzar (mètodes). És la plantilla que ens servirà per crear objectes.|
|Objecte<br><br><br><br>|**Un objecte és una instància d'una classe.** <br><br>Diem que hem creat o instanciat un objecte quan donem valors i fem servir els components definits a la classe.|
|Atribut<br><br><br>|**Un atribut és una característica concreta d'un objecte.** <br><br>Es defineix com les variables del programes estructurats, és a dir, definint tipus de dades i nom.|
|Mètode<br><br><br>|**Els mètodes defineixen quines funcionalitats o accions pot realitzar la classe.** <br><br>Reflecteixen les operacions que es poden fer sobre els atributs. |

#### Exemple

Un exemple podria ser una classe jugadorFutbol que tingués:

- *atributs:* nom, edat, pes, posició, nacionalitat, etc. 
- *mètodes:* marcaGols, esLesiona, protestaArbitre, canviaPosicio, etc.

I amb aquesta classe jugadorFutbol definida podríem tenir diferents jugadors, per tant hi instanciaríem diferents objectes:

- Leo Messi, 33 anys, 65kg, davanter, argentí.
- Andres Iniesta, 36 anys, 67kg, centrecampista, espanyol.

***

#### Intanciem la primera classe

Definirem la classe Persona i un mètode que ens faci saludar aquesta persona mostrant un missatge per pantalla. 

```java
package exemple1.versio1;

public class Persona {

  public void saluda() { 
    System.out.println("Hola, sóc una persona");
  }   
}
```
Observacions:
- A la línia 1 tenim la declaració del package. Per conveni, el nom dels packages s'ha d'escriure en minúscules.
- A la línia 3 tenim la declaració de la classe. La paraula reservada public serveix per especificar l’àmbit (o accés o visibilitat) de la classe. De moment, totes les classes seran públiques. Fixeu-vos que la primera lletra és majúscula i la resta del nom de la classe en minúscula.
- A la línia 5 tenim la declaració del mètode. És un mètode públic això ens indica que té visibilitat en altres classes i per tant pot ser cridat des d'elles. També s'observa que la signatura del mètode no porta la paraula static, això voldrà dir que si es vol cridar aquest mètode necessitarem abans crear una instància de Persona.

Recordem que la JVM busca en la classe que executem un mètode main com a punt d'inici de l'execució, en la classe Persona no hi és, si proveu d'executar-lo el compilador de Java retorna un error conforme no ha trobat un mètode main. Cal doncs que definim aquest mètode main ja sigui a la pròpia classe Persona o una altra classe. En l'exemple següent s'ha generat una classe nova per testejar Persona capaç de crear-ne una instància i cridar al mètode saluda.

```java
package exemple1.versio1;

public class PersonaTest {

  public static void main(String[] args) { 
    Persona persona = new Persona();
    persona.saluda();
  }   
}
```

Observacions:
- A diferència del mètode saluda, el mètode main de PersonaTest és static, això vol dir que no necessita de la instància de la classe PersonaTest per ser cridat.
- En la línia 6 es crea un objecte nou de la classe Persona, aquest objecte és instanciat en una variable que s'anomena persona. El tipus de persona és Persona que ara mateix no té cap atribut i només conté un mètode capaç de saludar. El mètode Persona() que es crida quan s'instancia l'objecte s'anomena constructor i el veurem més endavant.
- A continuació, com que ja tenim un objecte instanciat de Persona, ja podem cridar tots aquells mètodes no-statics que tingui aquesta persona, com per exemple saluda. 

#### Crida amb paràmetres

Efectuem un petit canvi a l'activitat anterior i definim el mètode saluda amb un paràmetre d'entrada que simbolitzi el nom de la persona i que demanarem per teclat en PersonaTest. Les dues classes quedarien de la següent manera:

```java
package exemple1.versio2;

public class Persona {

  public void saluda(String nom) { 
    System.out.println("Hola, sóc " + nom);
  }   
}
```

```java
package exemple1.versio2;
import java.util.Scanner;

public class PersonaTest {

  public static void main(String[] args) { 
    Scanner sc = new Scanner(System.in);
    System.out.println("Demana el nom de la persona que saluda: ");
    String nomPersona = sc.nextLine();
    Persona persona = new Persona();
    persona.saluda(nomPersona);
  }   
}
```
Sobre les classes utilitzades en PersonaTest:
- Usem Scanner, per això l'importem, ja que sinó no el tindríem visible. 
- També estem cridant String i System, les dues pertanyents al paquet java.lang. Java ja les ha incorporades implícitament per això les podem usar sense declarar-ne l'import.
- Finalment estem creant objectes de la classe Persona. Com que PersonaTest i Persona es troben en el mateix directori, que correspon al mateix package, ja és visible i no cal importar-la tampoc.

#### Variables d'instància (atributs de classe)

Com ja hem vist en la UF2 les variables locals es declaren dins un àmbit de visibilitat, ja sigui dins un mètode o d'una determinada estructura de control (while/for), estan actives dins aquest àmbit, després desapareixen.

Dins de cada classe hi ha les anomenades variables d'instància o atributs de la classe. Aquests poden ser instanciats en la creació de l'objecte i estan actius durant la vida d'aquest objecte. Cada objecte de la classe manté una còpia d'aquests camps amb els seus respectius valors. 


#### Getters & Setters

En la definició de qualsevol classe existeixen uns mètodes particulars que ens ajuden a interactuar amb els atributs dins la classe:

- Getters: són mètodes que ens permeten **accedir** al contingut d'una variable d'instància.
- Setters: són mètodes que ens permeten **modificar** el contingut d'una variable d'instància.

Les classes en Java estan estructurades sota el **principi d'encapsulació**. Declarant les variables d'instància com a privades (podríem haver-les fet públiques) encapsulem (amaguem) la variable. Així, aquesta variable sols es pot modificar des del
nostre mètode setNomVariable (setter). Evitem modificacions accidentals des de qualsevol lloc del programa.

Així doncs la manera de minimitzar errors i a la vegada d'ocultar el tipus de les variables (la qual cosa ens dóna flexibilitat si en un futur existeixen modificacions en l'estructura de dades de la pròpia classe) és **creant els atributs de classe com a privats i implementar els seus mètodes get i set públics**. L'accés des de fora la classe a aquesta variable serà a través dels mètodes. Així per a cada atribut de classe implementarem un getter i un setter. 

Reprenem l'exemple anterior i afegim dues variables de classe a Persona: nom i edat, afegim degudament els seus getters & setters i en comprovem el funcionament en el PersonaTest creant dos exemples de Persona diferents.


```java
package exemple1.versio2;

public class Persona {

  private String nom;
  private int edat;

  public String getNom(){
      return nom;
  }

  public int getEdat(){
      return edat;
  }

  public void setNom(String nom){
      this.nom = nom;
  }

  public void setEdat(int edatNova){
      edat = edatNova;
  }

  public void saluda() { 
        System.out.println("Hola, sóc " + nom + " i tinc " + edat + " anys");
  }   
}
```

```java
package exemple1.versio2;
import java.util.Scanner;

public class PersonaTest {

  public static void main(String[] args) { 
    
    Scanner sc = new Scanner(System.in);

    System.out.println("Demana el nom de la persona1: ");
    String nomPersona1 = sc.nextLine();
    System.out.println("Demana el nom de la persona1: ");
    int edat1 = sc.nextInt();sc.nextLine();

    System.out.println("Demana el nom de la persona2: ");
    String nomPersona2 = sc.nextLine();
    System.out.println("Demana el nom de la persona2: ");
    int edat2 = sc.nextInt();

    sc.close();

    Persona persona1 = new Persona();
    Persona persona2 = new Persona();

    persona1.setNom(nomPersona1);
    persona1.setEdat(edat1);
    persona2.setNom(nomPersona2);
    persona2.setEdat(edat2);

    System.out.println("El nom de la persona1 es: "+persona1.getNom()+" i l'edat es: "+persona1.getEdat());
    System.out.println("El nom de la persona2 es: "+persona2.getNom()+" i l'edat es: "+persona2.getEdat());

    persona1.saluda();
    persona2.saluda();
  }   
}
```


Observacions:
- El getNom i getEdat retornen el valor de la variable d'instància d'un objecte determinat.
- Per la seva banda setNom i SetEdat modifiquen el contingut de la variable d'instància pertinent.
- Fixem-nos que saluda() ja no té com a paràmetre d'entrada el nom ja que l'agafa de la pròpia classe. L'atribut de classe és privat i per tant no és accessible des de fora la classe (s'accedeix mitjançant el getNom) però sí que ho és desde dins la pròpia classe, en saluda().

#### Constructors

{{% notice note %}}
Totes les classes han de tenir un constructor que es fa servir per a instanciar objectes d'aquesta classe. En el constructor s'acostuma a donar valor als atributs de classe.

El constructor ha de tenir el mateix nom que la classe i no s'ha de posar tipus de retorn (ni void ni res!)
{{% /notice %}}

Si en una classe no s'especifica cap constructor, el compilador proporciona un constructor per defecte sense paràmetres. Per exemple:

```java
public class ClasseProva {

    /* És el mateix posar aquest constructor que no posar-lo.
     * ClasseProva (){
     *
     * }
     */
}

public class ClasseProvaTest {

  public static void main(String[] args){
      ClasseProva cp = new ClasseProva();
  }

}
```

Encara que no l'haguem definit en ClasseProva, per tal de crear objectes de tipus ClasseProva, **SI NO EXISTEIX CAP MÉS CONSTRUCTOR**, Java ens proporciona el constructor per defecte (aquell constructor que no conté cap paràmetre ni cap operació dins el constructor). Ara bé, quan ClasseProva tingui definit almenys un constructor, desapareix ClasseProva per defecte, a no sé que també estigui explícitament definit en la classe ClasseProva.

Els constructors són mètodes especials que sobretot **NO retornen** cap valor. Serveixen per indicar a Java que estem creant un objecte d'aquella classe. Sí que es pot proporcionar paràmetres d'entrada que ens ajudin a instanciar els atributs de classe d'aquell objecte. Si ens fixem en l'exemple anterior de Persona, podríem redefinir-lo de la següent manera:


```java
public class Persona {

  private String nom;
  private int edat;

  Persona (String nom, int edat){
      this.nom = nom;
      this.edat = edat;
  }

  public String getNom(){
      return nom;
  }

  public int getEdat(){
      return edat;
  }

  public void setNom(String nom){
      this.nom = nom;
  }

  public void setEdat(int edatNova){
      edat = edatNova;
  }

  public void saluda() { 
        System.out.println("Hola, sóc " + nom + " i tinc " + edat + " anys");
  }   
}
```

```java
import java.util.Scanner;

public class PersonaTest {

  public static void main(String[] args) { 
    
    Scanner sc = new Scanner(System.in);

    System.out.println("Demana el nom de la persona1: ");
    String nomPersona1 = sc.nextLine();
    System.out.println("Demana el nom de la persona1: ");
    int edat1 = sc.nextInt();sc.nextLine();

    System.out.println("Demana el nom de la persona2: ");
    String nomPersona2 = sc.nextLine();
    System.out.println("Demana el nom de la persona2: ");
    int edat2 = sc.nextInt();

    sc.close();

    Persona persona1 = new Persona(nomPersona1, edat1);
    Persona persona2 = new Persona(nomPersona2, edat2);

    System.out.println("El nom de la persona1 es: "+persona1.getNom()+" i l'edat es: "+persona1.getEdat());
    System.out.println("El nom de la persona2 es: "+persona2.getNom()+" i l'edat es: "+persona2.getEdat());

    persona1.saluda();
    persona2.saluda();
  }   
}
```

Observacions:
- La constructora de Persona té dos paràmetres d'entrada que corresponen amb els dos atributs de la classe.
- Per diferenciar dues variables que es diuen igual (atribut de classe i paràmetre d'entrada) utilitzem el this. El this ens ajuda a diferenciar qualsevol atribut/mètode de dins la pròpia classe.
- En la classe test observem que ara no fem ús dels setters dels atributs, ja que a l'instanciar l'objecte amb la constructora ja els inicialitzem els atributs.


**Més d'un constructor**

Es podria donar el cas que fos necessari la implementació de més d'un constructor en una classe, això és possible sempre que els tipus dels paràmetres d'entrada no coincideixin del tot, el compilador de Java diferencia els constructors dins la mateixa classe amb el llistat dels paràmetres d'entrada. Per exemple continuant amb l'exemple anterior redefinim la classe Persona amb 3 constructors:

```java

//Constructor per crear una persona amb nom
public Persona(String nomPersona) {
  nom = nomPersona;
  edat = 0; //li poso un valor per defecte
}

//Constructor per crear una persona sense res
public Persona() {
}

//Constructor per crear un persona amb nom i edat
public Persona(String nomPersona, int edatPersona) {
  nom = nomPersona;
  edat = edatPersona;
}
```  

En el programa principal podríem crear ara objectes Persona de tres maneres diferents:

```java
public static void main(String[] args) {
    Persona persona1 = new Persona("Jordi");
    persona1.setEdat(45);
    persona1.saluda();
    Persona alumne2 = new Persona("Maria", 18);
    persona2.saluda();
    Persona persona3 = new Persona();
    persona3.saluda();
}
```

#### This

{{% notice note %}}
Quan som dins d'un constructor o un mètode, this és una referència a l'objecte actual. Amb this pots fer referència a qualsevol atribut o mètode de l'objecte actual. Sobretot és necessari quan podria prestar confusió quan dos atributs o dos mètodes s'anomenen igual.
{{% /notice %}}

```java
  public String getNom(){
      return this.nom;
  }

  public String setEdat(){
      return this.edat;
  }

  public void setNom(String nom){
      this.nom = nom;
  }

  public void setEdat(int edatNova){
      edat = edatNova;
  }
   
}
```

Observacions:
- En el mètode setNom és necessari l'ús del this ja que ens diferencia l'atribut de classe del paràmetre de la funció.
- En el mètode setEdat, no l'hem posat ja que no presta a confusió les dues variables, tot hi així es podria haver posat a `this.edat` per remarcar que estem parlant de l'atribut de classe.
- En els getters l'hem deixat com a bona praxis, però si no hi hagués el this tampoc hi hauria confusió i java ho interpretaria correctament.

En l'exemple següent utilitzem el this com a crida a un constructor dins la mateixa classe:

```java
public Persona(String nom) {
  this(nom, 18); //crido al 3r constructor
}

public Persona() {
  this("Anonymous"); //crido al 1r constructor
}

public Persona(String nom, int edat) {
  this.setNom(nom);
  this.setEdat(edat);
}
```

#### Mètodes i variables Estàtics i No Estàtics

**Mètodes estàtics**

Ja hem vist a la UF2 la diferència entre una variable o mètode estàtic i no estàtic. Fins al moment amb l'exemple Persona hem treballat la definició d'una classe que per ser utilitzada és necessari instanciar-ne un objecte, és així ja que és necessari guardar en memòria la informació d'aquesta persona, d'aquesta manera, els mètodes de la classe interactuen amb aquests atributs, és un clar exemple d'una classe no estàtica. És necessari la creació d'un objecte Persona per utilitzar els seus mètodes getters & setters o saluda. Això no treu que podria haver-hi hagut algun mètode que sí fos estàtic, o sigui, el seu comportament no varia tant si intanciem com si no instanciem una Persona, un exemple seria:

```java
public static String informa(){
    System.out.println("Soc un metode de la classe Persona i el meu objectiu es nomes informar d'aixo");
}
```

Per fer ús d'aquest mètode `informa()` no és necessari crear un objecte Persona.

Així doncs no podrem declarar un mètode com estàtic si aquest:
- Accedeix a atributs de la classe.
- Modifica el contingut d'atributs de la classe.
- En ell hi intervenen mètodes privats de la pròpia classe.

Si el mètode ha de realitzar una tasca independent al contingut de l'objecte i no hi té incidència es pot declarar com `static`. 

L'exemple anterior ens podria servir per persona. Normalment s'usen els mètodes estàtics per realitzar càlculs o recorre llistats predeterminats. Un exemple és la classe [Math de Java](https://docs.oracle.com/javase/8/docs/api/java/lang/Math.html). Si li feu un cop d'ull observareu que tots els seus mètodes són statics, és així ja que el propòsit de tots ells és efectuar càlculs independents. En l'exemple següent usarem el mètode anterior `informa()` i el mètode max de la classe Math:

```java
public static void main((String[] args) {
  int numero1 = 20;
  int numero2 = 10;
  int numeroMaxim = Math.max(numero1, numero2);
  Persona.informa();
}
```

Observacions:
- La notació per tal d'usar els mètodes estàtics és NomClasse.nomMetode(). 
- Els mètodes estàtics també poden ser privats. Si per exemple hagués declarat informa() voldria dir que només el podria usar des de dins la pròpia classe Persona, no tindria visibilitat fora d'aquesta.

Es poden referenciar mètodes estàtics desde dins de mètodes no estàtics, un exemple en són els mètodes de la classe Math que els podem usar allà on siguin requerits, però no al revés. No podria declarar el mètode saluda() de la classe Persona com a estàtic ja que ESTIC USANT ATRIBUTS de la classe. Si el declaro com a estàtic podria passar que utilitzés el mètode saluda() abans de crear un objecte Persona, el mètode va a buscar les variables nom i edat que no reconeix i el compilador de Java donaria error.

```java
  public void saluda() { 
        System.out.println("Hola, sóc " + nom + " i tinc " + edat + " anys");
  } 
```

**Atributs estàtics**

Fins al moment hem treballat amb atributs d'instància, són aquells que poden canviar de valor en cada objecte i que per tant el determinen. Però també tenim atributs estàtics, són aquells que no se'n modifica el valor i que, per tant, tenen el mateix valor per tots els objectes. Els atributs estàtics estan sempre en memòria, per això és necessari declarar només aquells que siguin imprescindibles.

Per a utilitzar-los posarem la paraula `static` abans del tipus de la variable. Per exemple MAJOR_EDAT:

```java
public class Persona {
 
  public static int MAJOR_EDAT = 18;  
  private String nom;
  private int edat;

  Persona (String nom, int edat){
      this.nom = nom;
      this.edat = edat;
  }

  public String getNom(){
      return nom;
  }
  
  ...

```

Igual que amb els mètodes, si la variable estàtica és pública i es vol accedir a ella des d'una altra classe cal que siguem la nomenclatura NomClasse.NomAtribut. Per exemple per accedir a l'anteior atribut estàtic fora de Persona hauríem de posar `Persona.MAJOR_EDAT`. 

Un dels usos més habituals de les variables estàtiques són per declarar constants, per exemple en la classe Math anterior tenim `Math.PI`. En aquests casos cal que vagin acompanyats de la paraula `final`, en Java quan declarem una variable com a final vol dir que un cop inicialitzada no li podem canviar el valor (com passa amb les constants). Si es vol canviar el valor a un atribut declarat com a final el compilador de Java contestarà amb un error. 

```java
  public static final int MAJOR_EDAT = 18;  
```

