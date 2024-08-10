---
title: Estructura de classe i mètodes
weight: 3
pre: "3. "
chapter: false
---

#### Atributs de la instància (propietats de la classe)

Les variables locals es declaren dins un àmbit de visibilitat, per exemple, com ja hem vist, les variables creades dins un while/for estan actives dins aquest àmbit, després desapareixen.

Cada classe té les seves propietats. En la creació de l'objecte aquestes poden prendre uns valors determinats que dónen sentit al propi objecte. Aquests valors estan actius durant la vida d'aquest objecte, això vol dir que quan aquest objecte es destrueix aquests valors deixen d'existir. Cada objecte de cada classe manté una còpia de les propietats amb els seus respectius valors. 

#### Getters & Setters

En la definició de qualsevol classe existeixen uns mètodes particulars que ens ajuden a interactuar amb les propietats de la classe:

- Getters: són mètodes que ens permeten **accedir** al contingut d'una variable d'instància.
- Setters: són mètodes que ens permeten **modificar** el contingut d'una variable d'instància.

Les classes en Java estan estructurades sota el **principi d'encapsulació**. Per això, declarem les propietats de la classe com a privades (podríem haver-les fet públiques) encapsulem (amaguem) les propietats. Així, aquestes sols es poden modificar des dels mètodes setNomVariable (setter) que els declarem públics. Evitem modificacions accidentals des de qualsevol lloc del programa. De la mateixa manera, si volem accedir a un valor d'una propietat d'un objecte existeixen els mètodes getters.

Així doncs la manera de minimitzar errors i a la vegada d'ocultar el tipus de les variables (la qual cosa ens dóna flexibilitat si en un futur existeixen modificacions en l'estructura de dades de la pròpia classe) és **creant les propietats de classe com a privats i implementar els seus mètodes get i set públics**. L'accés des de fora la classe a cada propietat serà a través dels mètodes esmentats. Així per a cada propietat de la classe implementarem un getter i un setter. 

Reprenem l'exemple anterior i afegim dues propietats a Persona: nom i edat, afegim degudament els seus getters & setters i en comprovem el funcionament en el PersonaTest creant dos exemples de Persona diferents.


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
- El getNom i getEdat retornen el valor de la propietat d'un objecte determinat.
- Per la seva banda setNom i setEdat modifiquen el contingut de la propietat pertinent.
- Fixem-nos que saluda() ja no té com a paràmetre d'entrada el nom ja que l'agafa de la pròpia classe. La propietat és privada i per tant no és accessible des de fora la classe (s'accedeix mitjançant el getNom) però sí que ho és desde dins la classe, en saluda().