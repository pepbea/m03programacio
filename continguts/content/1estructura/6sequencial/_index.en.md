---
title: Estructura Seqüencial
weight: 6
pre: "6. "
chapter: false
---

#### Estructura seqüencial

{{% notice note %}}
En **l'estructura seqüencial** permet descomposar un problema en instruccions que s'executaran de la primera a la última seguint un ordre **de forma incondicional**. 
{{% /notice %}}

{{% notice note %}}
L' **assignació** consisteix en donar un valor a una variable. "Guardar" una informació en una variable, que segurament serà tractada i/o consultada més endavant. 
{{% /notice %}}

|Codi| Diagrama de flux|
|---|---|
|Acció1;<br>Acció2;<br>Acció3;<br>Acció4;|![seq](images/seq.png?width=100px)|


### Estructura bàsica 
L'estructura bàsica de qualsevol programa en Java anirà dins una "classe" amb un fitxer .java, amb la següent plantilla:

```java
public class Main {
    public static void main(String[] args) {
    
    
    }
}
```

Java executarà tot el que trobi dins les claus del main anterior. 


### Dades d'entrada

Per tal **d'introduir valors** al nostre programa (inputs), inicialment, farem servir la classe Scanner (Scanner ens permet introduir molts tipus de dades en les variables que ja coneixem). Primerament cal que "importem" Scanner just a l'inici del nostre fitxer, `import java.util.Scanner`, tot seguit i ja dins el nostre bloc de main creem un objecte Scanner, per exemple a l'identificador de la variable li direm sc. Aquest objecte ens permetrà introduir informació pel teclat dels tipus de dades ja coneguts. L'exemple és molt il·lustratiu:

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int enter32bits = sc.nextInt();
        long enter64bits = sc.nextLong();
        float decimal = sc.nextFloat();
        double decimalGran = sc.nextDouble();
        boolean boolea = sc.nextBoolean();
        String cadenaCaracters = sc.next();                //Capta tots els caràcters fins al primer espai.
        String cadenaCaractersFinalLinia = sc.nextLine();  //Guarda tots els caràcters fins a la finalització de línia (Enter).
    }
}

```

Quan s'executa aquest programa, observarem que quan arriba a la línia on hi ha `sc.nextInt()`, el programa es queda parat esperant que l'usuari introdueixi per teclat un valor i pressioni Enter, això passarà amb la resta de valors que s'espera que l'usuari introdueixi per teclat. Tots aquests valors seran assignats a les variables que hem definit: enter32bits, enter64bits...



### Dades de sortida

Per tal d'observar els valors pel terminal (outputs) el que farem serà usar `System.out.print` i si volem un salt de línia `System.out.println`

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("Pots escriure el teu nom per línia de comandes?");

        String nom = sc.nextLine();

        System.out.print("Hola! ");
        System.out.print("El meu nom és " + nom);
    }
}
```
### Comentaris

Els comentaris són útils per mostrar informació adicional del codi, quan aquesta sigui necessària, no és bo abusar-ne. Normalment un codi ben escrit hauria de ser autoexplicatiu. Si s'assignen noms de variables i funcions coherents pel que s'utilitzen no caldria escriure molts comentaris.

Java interpreta com a text explicatiu tots els comentaris i per tant **NO ELS EXECUTA** com si fossin instruccions. Existeixen comentaris per:
- Una fila. En aquest cas utilitzarem  "// Comentari"
- Més d'una fila, el comentari anirà entre "/* Comentari vàries línies */"
- Per realitzar documentacions de codi usant, per exemple Javadoc "/** Documentació */"

```java
public class Main {
    public static void main(String[] args) {

    //Comentari d'una sola línia

    /*
    Comentari
    de 
    més d'una 
    línia
    */

}

/**
 * Aquesta funció retorna la suma entera de dos nombres enters passats per paràmetre
 *
 * @param  operand1  primer operand de l'operació suma
 * @param  operand2  segon operand de l'operació suma
 * @return      retorna un enter que és la suma dels dos
 * @see         suma
 */
 public int suma(int operand1, int operand2) {
    var resultat = operand1 + operand2;
    return resultat;
 }

```



#### Exemples de problemes seqüencials

1. Llegeix dos nombres reals i escriu la seva suma, resta, producte i quocient.

```java  
    float operand1 = sc.nextFloat();
    float operand2 = sc.nextFloat();

    float suma = operand1 + operand2;
    float resta = operand1 - operand2;
    float multiplicacio = operand1 * operand2;
    float divisio = operand1 / operand2;
    float modul = operand1 % operand2;

    System.out.println("Suma:" + suma);
    System.out.println("Resta:" + resta);
    System.out.println("Multiplicacio:" + multiplicacio);
    System.out.println("Divisio:" + divisio);
    System.out.println("Modul:" + modul);

```

2. Llegeix el preu d'un producte, l'IVA (en %) i el descompte (en %) a aplicar. Escriu el preu final del producte.

```java  
    float preu = sc.nextFloat();
    int iva = sc.nextInt();
    int descompte = sc.nextInt();

    float preuAmbIva = preu + preu * iva / 100;
    float preuAmbIvaIDescompte = preuAmbIva - preuAmbIva * descompte / 100;

    System.out.println("Preu final:" + preuAmbIvaIDescompte);
```

3. Calcula l'àrea lateral i el volum d'un cilindre recte, introduint per teclat els valors del radi i l'altura. V =pi⋅r2⋅h    AL=2⋅pi⋅r⋅h

```java     
    float radi = sc.nextFloat();
    float altura = sc.nextFloat();

    double areaLateral = 2 * Math.PI * radi * altura;
    double volum = Math.PI * Math.pow(radi,2) * altura;

    System.out.println("Area lateral:" + areaLateral + " Volum:" + volum);
```

4. Llegeix un nombre enter no negatiu i un altre nombre enter no negatiu que indica la posició de les seves xifres i escriu la xifra que ocupa aquesta posició. Les unitats estan a la posició 1, les desenes a la posició 2, etc.

```java     
    int nombre = sc.nextInt();
    int posicio = sc.nextInt();

    double potencia = Math.pow(10,posicio-1);
    double nombreRetallat = nombre / potencia;
    int nombreBuscat = (int)nombreRetallat % 10;
    
    System.out.println("el dígit " +posicio+ " del nombre " + nombre + " és: "+ nombreBuscat);
```

5. Llegeix un nombre enter de segons i escriu el nombre d’hores, minuts i segons equivalents en format h:m:s.

```java     
    int segonsTotals = sc.nextInt();

    int hores = segonsTotals / 3600;
    int segonsRestants = segonsTotals % 3600;
    int minuts = segonsRestants / 60;
    int segons = segonsRestants % 60;

    System.out.println(hores + ":" + minuts + ":" + segons);
```