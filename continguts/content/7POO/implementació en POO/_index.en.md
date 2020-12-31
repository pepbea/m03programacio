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
    System.out.println("Hola, sóc " + nom + " i tinc " + anys + "anys");
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
    String edat1 = sc.nextInt();

    System.out.println("Demana el nom de la persona1: ");
    String nomPersona2 = sc.nextLine();
    System.out.println("Demana el nom de la persona1: ");
    String edat2 = sc.nextInt();

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
