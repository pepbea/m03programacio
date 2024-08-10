---
title: Mètodes estàtics
weight: 2
pre: "3.2. "
chapter: false
---

### Mètodes Estàtics 

{{% notice note %}}
Els **mètodes estàtics** són aquells que no depenen d'un objecte i que per tant s'invoquen a partir de la classe.
Els **mètodes que no són estàtics** són aquells que depenen de l'existència d'un objecte i que per tant té sentit que s'invoquin una vegada s'ha creat un objecte.
{{% /notice %}}

Posem un exemple, d'un mètode que és estàtic i que per tant no depèn de la instanciació d'un objecte i d'un mètode que no és estàtic i que per tant necessita d'un objecte per ser executat:

```java
//EXEMPLE ESTÀTIC
//Mètode estàtic, suma de dos nombres
public class Arithmetic{
  public static int sum (int a, int b)
  {
      int s;
      s = a + b;
      return s;
  }
}

//El cridaríem fent ús de la pròpia classe, no és necessari crear un objecte Arithmetic per cridar la suma entre dos nombres.
public class Main{
  public static void main(String[] args){
    int res;
    res = Arithmetic.suma(2,3);
  }
}


//EXEMPLE NO ESTÀTIC
//Classe Persona amb un sol atribut, constructora i mètode saluda que utilitza l'atribut nom.
public class Persona{
  private String nom;

  Persona(String nom){
    this.nom = nom;
  } 

  public void saluda (){
     System.out.println("Hola em dic " + nom)
  }
}

//Per tal de cridar saluda és necessari crear una persona, no té sentit cridar saluda sense haver creat la persona ja que no sabem a partir de qui saludem!
public class Main{
  public static void main(String[] args){
    Persona persona = new Persona("Manolo");
    persona.saluda();
  }
}

```

 Com s'observa en el primer exemple el comportament del mètode suma no varia tant si intanciem com si no instanciem la classe Arithmetic, és una funció que té dos paràmetres d'entrada (que són els operands) i un paràmetre de sortida, per tant sempre té el mateix comportament. Mentre que en el segon exemple el mètode saluda fa ús de l'atribut nom, si no tenim un objecte Persona deixa de tenir sentit aquest mètode per això va lligat al comportament que adopti una determinada persona.


<br>

**RECORDA**

No podrem declarar un mètode com estàtic si aquest:
- Accedeix a atributs de la classe.
- Modifica el contingut d'atributs de la classe.
- En ell hi intervenen mètodes privats de la pròpia classe.

Si el mètode ha de realitzar una tasca independent al contingut de l'objecte i no hi té incidència es pot declarar com `static`. 

En Java existeixen funcionalitats en les quals ens ve de sèrie classes implementades amb mètdoes estàtics, seguint l'exemple anterior és un clar exemple la classe [Math de Java](https://docs.oracle.com/en%2Fjava%2Fjavase%2F22%2Fdocs%2Fapi%2F%2F/java.base/java/lang/Math.html). Si li feu un cop d'ull observareu que tots els seus mètodes són estàtics, és així ja que el propòsit de tots ells és efectuar càlculs independents. En l'exemple següent usarem el mètode max de la classe Math:

```java
public static void main((String[] args) {
  int numero1 = 20;
  int numero2 = 10;
  int numeroMaxim = Math.max(numero1, numero2);
}
```

Observacions:
- La notació per tal d'usar els mètodes estàtics és NomClasse.nomMetode(). 
- Els mètodes estàtics també poden ser privats. Si per exemple hagués declarat suma() com a mètode privat voldria dir que només el podria usar des de dins la pròpia classe Arithmetic, no tindria visibilitat fora d'aquesta.


**Atributs estàtics**

Fins al moment hem treballat amb atributs d'instància, són aquells que poden canviar de valor en cada objecte i que per tant el determinen. Però també tenim atributs estàtics, són aquells que no se'n modifica el valor i que, per tant, comparteixen el mateix valor per tots els objectes. Els atributs estàtics estan sempre en memòria, per això és necessari declarar només aquells que siguin imprescindibles.

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

Un dels usos més habituals de les variables estàtiques són per declarar constants (vist ja en la RA1), per exemple en la classe Math anterior tenim `Math.PI`. En aquests casos cal que vagin acompanyats de la paraula `final`, en Java quan declarem una variable com a final vol dir que un cop inicialitzada no li podem canviar el valor (com passa amb les constants). Si es vol canviar el valor a un atribut declarat com a final el compilador de Java respondrà amb el pertinent error. 

```java
  public static final int MAJOR_EDAT = 18;  
```

