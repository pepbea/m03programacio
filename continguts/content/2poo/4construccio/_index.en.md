---
title: Construcció destrucció d'objectes
weight: 4
pre: "4. "
chapter: false
---

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
- La constructora de Persona té dos paràmetres d'entrada que corresponen amb les dues propietats de la classe.
- Per diferenciar dues variables que es diuen igual (atribut de classe i paràmetre d'entrada) utilitzem el this. El this ens ajuda a diferenciar qualsevol atribut/mètode de dins la pròpia classe. Com s'observa en la constructora de Persona hi ha l'atribut de la pròpia instància `this.nom` que prèn per valor el paràmetre passat com argument `nom`.
- En la classe test observem que ara no fem ús dels setters dels atributs, ja que a l'instanciar l'objecte amb la constructora ja inicialitzem els atributs.


**Més d'un constructor**

Es podria donar el cas que fos necessari la implementació de més d'un constructor en una classe, això és possible sempre que els tipus dels paràmetres d'entrada no coincideixin, el compilador de Java diferencia els constructors dins la mateixa classe amb el llistat dels paràmetres d'entrada. Per exemple continuant amb l'exemple anterior redefinim la classe Persona amb 3 constructors:

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

Això és un dels poders que otorga la programació orientada a objectes i en concret el polimorfisme que permet tenir tres constructores que es diuen igual, i que per tant, l'objectiu final de cadascuna d'elles és la instanciació de Persona, però en canvi el "com ho fan", el comportament intern, és diferent ja que tenen diferent nombre d'arguments.

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

#### Destrucció d'objectes

Un objecte es manté viu sempre que existeixi una variable que l'estigui referenciant. Destruïrem un objecte, per tant, deixarem de tenir-hi accés, quan **no existeixi cap variable que apunti a l'objecte**. Una vegada un objecte deixa de ser-nos útil i per tant ocupa memòria innecessàriament és el moment de desrefenciar aquest objecte de totes les variables que l'apuntin **assignant el valor null a aquestes variables**. Quan posem valor null a una variable *desreferenciem* l'objecte on apuntava aquesta variable.

Les variables es guarden a un espai de memòria que s'anomena Stack, mentre que els objectes es guarden a un altre espai que s'anomena Heap. La variable guarda la direcció de memòria d'on es troba aquest objecte dins el heap, quan assignem valor null a una variable fem que aquesta variable deixi de guardar la direcció de memòria de l'objecte dins el heap. Quan això passa, en Java existeix el Garbage Collector, és un aplicatiu que rastreja contínuament la memòria de Java i quan troba objectes que no tenen cap referència en cap variable **alliberen** aquesta memòria i fan que torni a estar disponible per a l'ús de l'aplicatiu.

Exemple1: alliberem memòria un cop l'objecte ja no ens és útil:

``` java
Persona persona = new Persona();
...
persona = null;
```

Exemple2: en el següent exemple per tal d'eliminar l'objecte de persona1, és necessari desreferenciar totes aquelles variables que apuntin a l'objecte:
``` java
Persona persona1 = new Persona("Pedro", 25);
Persona persona2 = new Persona();
Persona persona3 = new Persona("Ramon");
Persona persona4 = new Persona("Alberto", 30);
Persona persona5 = new Persona("Pep", 25);
...
persona2 = persona1;
persona3 = persona1;
persona4 = persona5;
...
persona1 = null;
persona2 = null;
persona3 = null;
```

Quin és l'objecte que es manté actiu en el cas anterior? Persona4! Fixeu-vos que en fer persona2 = persona1; o persona3 = persona1; o persona4 = persona5; tant l'objecte de persona2, com l'objecte de persona3, com l'objecte persona4 han quedat desreferenciats i per tant el Garbage Collector ja els pot eliminar quan en tingui l'ocasió.

Per altra banda, més endavant decidim que persona1 ja no ens és útil, però l'objecte que inicialment hem creat en persona1 també guarda una referència en persona2 i en persona3 (persona2 = persona1; i persona3 = persona1;), de forma que si vull destruir aquest objecte i alliberar-ne la memòria que serà necessari que assigni valor null a les variables persona1 persona2 i persona3. D'aquesta manera elimino totes les referències de variables a aquest objecte i per tant el Garbage Collector ja el pot eliminar de la memòria Heap.

