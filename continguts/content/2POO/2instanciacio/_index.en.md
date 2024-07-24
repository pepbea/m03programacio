---
title: Instanciació d'objectes
weight: 2
pre: "2. "
chapter: false
---

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