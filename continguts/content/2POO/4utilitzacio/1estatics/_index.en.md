---
title: Mètodes estàtics
weight: 1
pre: "4.1. "
chapter: false
---

### 5. Mètodes Estàtics o no estàtics

{{% notice note %}}
Els **mètodes no estàtics** (o mètodes) són aquells que depenen d'un objecte i que per tant s'invoquen a partir de la instanciació d'un objecte.
{{% /notice %}}

Posem un exemple, imaginem aquest mètode de la classe Conversor:

```java
public double m2km (double m)
{
 double km;
 km = m / 1000;
 return km;
}
```

Per cridar aquesta mètode des d'un altre mètode faríem:
```java
Conversor conv = new Conversor();
double kilometers;
kilometers = conv.m2km(325012);
```
{{% notice note %}}
Els **mètodes estàtics** són aquells que no depenen d'un objecte i que per tant s'invoquen a partir de la classe.
{{% /notice %}}

Posem un exemple, imaginem aquest mètode de la classe Arithmetic:
```java
public static int sum (int a, int b)
{
    int s;
    s = a + b;
    return s;
}
```

Per cridar aquesta mètode des d'un altre mètode:
```java
int res;
res = Arithmetic.suma(2,3);
``


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

