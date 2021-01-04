---
title: Desenvolupament de POO
weight: 3
---

#### Variables referenciades

Totes les variables que no són primitives en Java passen a estar referenciades, igual com ja hem vist que passa amb els arrays o els Strings. En el cas que declarem les nostres pròpies classes i les instanciem passa el mateix. Retornant a l'exemple de Persona de l'activitat anterior, quan declarem una `Persona p`, estem declarant una referència a un objecte de tipus Persona, però fins que no la construïm amb el `new Persona()` aquesta referència p apunta a un valor null. La màquina virtual de Java té un procés anomenat garbage collector que periòdicament analitza quines són les variables desreferenciades (que apunten a null) i les elimina de la memòria. Així doncs un cop passa el garbage collector pel següent codi troba una variable p a null i l'elimina:

```java
//Creem la referència a un objecte de tipus Persona, de moment no està creat encara
Persona p;

//Creem i reservem en memòria espai suficient per guardar els atributs d'aquest objecte
p = new Persona();

//Efectuem modificacions a l'objecte
p.setEdat(5);
p.setNom("Joaquim");

//Fem que p es desreferenciï de l'objecte instanciat. Quan passi garbage collector eliminarà tots els punters desreferenciats com aquest.
p = null;
```

En la UF2 anterior hem observat el pas per valor i el pas per referència. Com ja hem vist quan passem com a paràmetre a una funció una variable de tipus primitiu s'efectua una còpia d'aquesta variable i no s'actua en l' original, mentre que **quan el paràmetre no es primitiu es passa com a referència, i per tant SÍ que estem enviant la posició de memòria on es troba la variable**, ho hem vist amb els arrays i ara veurem que passa el mateix quan passem una referència d'un objecte d'una classe que hem creat nosaltres (NO és de tipus primitiu). Anem a observar l'exemple següent:

```java
public static void main(String[] args) {
    Persona p = new Persona("Leo", 5);
    System.out.println("Abans d'entrar al canvi sense modificació:" + p);
    canviSenseModificarObjecte(p);
    System.out.println("Després de sortir de la funció del canvi sense modificacio:" +p);
    canviModificantObjecte(p);
    System.out.println("Després de sortir de la funció del canvi amb modificacio:" +p);

}

private static void canviSenseModificarObjecte(Persona p) {
    System.out.println("'p' dins de canviSenseModificarObjecte abans de canviar l'objecte de Persona p: " + p);
    p = new Persona();
    p.setNom("Victor");
    p.setEdat(33);
    System.out.println("'p' dins de canviSenseModificarObjecte després de canvia l'objecte de Persona p: " + p);
}
private static void canviModificantObjecte(Persona p) {
    System.out.println("'p' dins de canviModificantObjecte abans de modificar-lo: " + p);
    p.setNom("Pere");
    p.setEdat(47);
    System.out.println("'p' dins de canviSenseModificarObjecte després de canvia l'objecte de Persona p: " + p);
}
```

Resultat
```
Abans d'entrar al canvi sense modificació:Persona{nom='Leo', edat=5}
'p' dins de canviSenseModificarObjecte abans de canviar l'objecte de Persona p: Persona{nom='Leo', edat=5}
'p' dins de canviSenseModificarObjecte després de canvia l'objecte de Persona p: Persona{nom='Victor', edat=33}
Després de sortir de la funció del canvi sense modificacio:Persona{nom='Leo', edat=5}
'p' dins de canviModificantObjecte abans de modificar-lo: Persona{nom='Leo', edat=5}
'p' dins de canviSenseModificarObjecte després de canvia l'objecte de Persona p: Persona{nom='Pere', edat=47}
Després de sortir de la funció del canvi amb modificacio:Persona{nom='Pere', edat=47}
```

Observacions:
- Veiem que imprimim directament p i se n'observen els valors dels atributs. Per defecte totes les classes tenen una funció `public String toString()` que quan es crida la referència de l'objecte n'imprimeix els seus valors. Més endavant veurem com modificar-ho.
- Com s'observa en l'exemple quan es surt del primer mètode com que els canvis d'objecte es produeixen a l'interior del mètode, al sortir del mètode la referència p apunta on originàriament apuntava (es passa per referència) de forma que perdem els canvis que s'hagin pogut produir dins. En el segon mètode com que s'efectuen els canvis justament en la direcció p original, al sortir del mètode observem com els canvis s'han mantingut en l'objecte p Persona.

#### Exemples d'associació entre classes

#### Exemple 1: Classe Triangle

Creem una classe Triangle.

```java
public class Triangle {
	
	private int side1;
	private int side2;
	private int side3;
	
	/**
	 * Constructor per defecte.
	 */
	public Triangle(){
		side1 = 3;
		side2 = 4;
		side3 = 5;	
	}

	/**
	 * Constructor que rep la mida dels tres costats.
	 * @param nouSide1 Costat 1
	 * @param nouSide2 Costat 2
	 * @param nouSide3 Costat 3
	 */
	public Triangle(int nouSide1, int nouSide2, int nouSide3){
		side1 = nouSide1;
		side2 = nouSide2;
		side3 = nouSide3;	
	}
	
	/**
	 * Calcula el perímetre del triangle.
	 * @return Perímetre del triangle
	 */
	public int perimetre(){
		
		return side1+side2+side3;
	}
	
	/**
	 * Calcula l'àrea del triangle.
	 * @return Àrea del triangle
	 */
	public double area(){
		double s = (side1+side2+side3)/2;
		double a = s*(s-side1)*(s-side2)*(s-side3);
		double area = Math.sqrt(a);
		return area;
	}
	
	/**
	 * Prova de la classe.
	 * @param args
	 */
	public static void main(String[] args){
		Triangle triangle = new Triangle(10,14,15);
		System.out.println("Àrea del triangle: " + triangle.area());
		System.out.println("Perímetre del triangle: " + triangle.perimetre());
	}
	
}

```

#### Exemple 2: Comptador d'un dígit

Observem una possible implementació d'un comptador d'un sol dígit de 0-9.

```java
public class Comptador 
{
	private int numComptador;
	
	/**
	 * Definim la constructora
	 */
	public  Comptador(){
		numComptador = 0;
	}
	
	/**
	 * Definim el getter de numCumptador
	 * @return el valor del comptador
	 */
	public int getNumComptador(){
		return numComptador;
	}
	
	/**
	 * Definim el setter de numComptador
	 * @param a
	 */
	public void setNumComptador(int a){
		numComptador=a;
	}
	
	/**
	 * Incrementa el comptador
	 */
	public void incrementaComptador(){
		if (numComptador==9)numComptador=0;
		else numComptador++;	
	}
	
	/**
	 * Decrementa el comptador
	 */
	public void decrementaComptador() 
	{
		if (numComptador==0)numComptador=9;
		else numComptador--;
	}

    public static void main(String[] args) {
		Scanner in = new Scanner (System.in);
		Comptador c = new Comptador();
		System.out.println("\n EXERCICI COMPTADOR");
		System.out.println("\n ---------------------");

		System.out.println("Valor Inicial: "+c.getNumComptador());
		System.out.println("Incrementem 15 vegades el comptador");
		for (int h=0; h<15; h++){
	        c.incrementaComptador();
			System.out.println(c.getNumComptador());
		}
		System.out.println("Decrementem 15 vegades el valor del comptador");
		for (int h=0; h<15; h++){
			c.decrementaComptador();
			System.out.println(c.getNumComptador());
		}
    }
    

}
```

#### Exemple 3: Comptador de dos dígits (usant l'anterior)

Ara volem un comptador de dos dígits però usant dos comptadors d'un sol dígit (exemple anterior)
```java
public class Comptador2 
{
	Comptador desenes; 
    Comptador unitats;
    
    /**
     * Constructora de Comptador de dos dígits usant la classe Comptador
     */
	public Comptador2(){
		desenes = new Comptador();
		unitats = new Comptador();
	    desenes.setNumComptador(0);
	    unitats.setNumComptador(0);
	}
	
	/**
	 * Mètode getter del comptador
	 */
	public String getNumComptador(){
		return desenes.getNumComptador()+""+unitats.getNumComptador();
	}
	
	/**
	 * Mètode setter del comptador
	 * @param desenes
	 * @param unitats
	 */
	public void setNumComptador(int desenes, int unitats){
		this.desenes.setNumComptador(desenes);
		this.unitats.setNumComptador(unitats);
	}
	
	/**
	 * Incrementa el comptador
	 */
	public void incrementaComptador(){
		if(desenes.getNumComptador()==9 && unitats.getNumComptador()==9){
			desenes.setNumComptador(0);
			unitats.setNumComptador(0);
		}else if(unitats.getNumComptador()==9){
			desenes.incrementaComptador();
			unitats.setNumComptador(0);
		}else{
			unitats.incrementaComptador();
		}
	}
	
	/**
	 * Decrementa el comptador
	 */
	public void decrementaComptador(){
		if(desenes.getNumComptador()==0 && unitats.getNumComptador()==0){
			desenes.setNumComptador(9);
			unitats.setNumComptador(9);
		}else if(unitats.getNumComptador()==0){
			desenes.decrementaComptador();
			unitats.setNumComptador(9);
		}else{
			unitats.decrementaComptador();
		}
	}

    public static void main(String[] args) 
	{
		Comptador2 c2 = new Comptador2();
		System.out.println("\n\n EXERCICI COMPTADOR 2");
		System.out.println("\n -------------------------");
		System.out.println("Ara enlloc de tenir un comptador, tenim unitats i desenes (2 instàncies de la classe comptador)");
		System.out.print("Valor inicial: " + c2.getNumComptador());
		System.out.println("Incrementem valors fins a 101 i veiem què passa");
		for (int h=0; h<101; h++){
	        c2.incrementaComptador();
			c2.getNumComptador();
			System.out.println(c2.getNumComptador());
		}
		System.out.println("Decrementem els valors fins a -102 i veiem què passa");
		for (int h=0; h<102; h++){
			c2.decrementaComptador();
			c2.getNumComptador();
			System.out.println(c2.getNumComptador());
		}
    }
}
```

#### Exemple 4: Classe amb alumnes

Exemple de com usar una col·lecció d'objectes, en aquest cas tenim una classe Alumne i una classe Classe que serà un conjunt d'alumnes. Durant l'exemple veurem diferents conceptes:
1. Alumne
2. Test amb JUnit Alumne
3. Classe
4. Programa principal

Comencem amb la definició de la classe Alumne, a més a més:
- Mètodes Override
- Mètodes de còpia d'un objecte
- Comparator

```java
import java.util.Comparator;
public class Alumne implements Cloneable{

    private int edat=18;
    private String nom;
    private String cognoms;

    //CONSTRUCTORES
    public Alumne(){
        this(18,"","");
    }

    public Alumne(String nom, String cognoms){
        this.nom = nom;
        this.cognoms = cognoms;
    }

    public Alumne(int edat, String nom, String cognoms){
        this.edat = edat;
        this.nom = nom;
        this.cognoms = cognoms;
    }

    //CÒPIA OBJECTE
    public Alumne (Alumne a){
        this.edat = a.getEdat();
        this.nom = a.getNom();
        this.cognoms = a.getCognoms();
    }

    //GETTERS
    public int getEdat() {
        return edat;
    }

    public String getNom() {
        return nom;
    }

    public String getCognoms() {
        return cognoms;
    }

    //SETTERS
    public void setEdat(int edat) {
        this.edat = edat;
    }

    public void setNom(String nouNom) {
        nom = nouNom;
    }

    public void setCognoms(String cognoms) {
        this.cognoms = cognoms;
    }

    //MÈTODES SOBREESCRITS
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Alumne)) return false;

        Alumne alumne = (Alumne) o;

        if (getEdat() != alumne.getEdat()) return false;
        if (!getNom().equals(alumne.getNom())) return false;
        return getCognoms().equals(alumne.getCognoms());
    }

    @Override
    public int hashCode() {
        int result = getEdat();
        result = 31 * result + getNom().hashCode();
        result = 31 * result + getCognoms().hashCode();
        return result;
    }

    @Override
    public String toString() {
        return "Alumne{" +
                "edat=" + edat +
                ", nom='" + nom + '\'' +
                ", cognoms='" + cognoms + '\'' +
                '}';
    }


    //DEFINIM COMPARATORS PER A ORDENAR
    /*Comparator per Nom*/
    public static Comparator<Alumne> alumnesCompararPerNom = new Comparator<Alumne>() {
        public int compare(Alumne a1, Alumne a2) {
            String alumneNom1 = a1.getNom().toUpperCase();
            String alumneNom2 = a2.getNom().toUpperCase();

            //ordre ascendent
            return alumneNom1.compareTo(alumneNom2);

            //ordre descendent
            //return alumneNom2.compareTo(alumneNom1);
        }};


    /*Comparator per Cognoms*/
    public static Comparator<Alumne> alumnesCompararPerCognom = new Comparator<Alumne>() {
        public int compare(Alumne a1, Alumne a2) {
            String alumneCognom1 = a1.getCognoms().toUpperCase();
            String alumneCognom2 = a2.getCognoms().toUpperCase();

            //ordre ascendent
            return alumneCognom1.compareTo(alumneCognom2);

            //ordre descendent
            //return alumneCognom2.compareTo(alumneCognom1);
        }};


    /*Comparator per Nom*/
    public static Comparator<Alumne> alumnesCompararPerEdat = new Comparator<Alumne>() {
        public int compare(Alumne a1, Alumne a2) {
            int alumneEdat1 = a1.getEdat();
            int alumneEdat2 = a2.getEdat();

            //ordre ascendent
            if (alumneEdat1>=alumneEdat2) return 1;
            else return -1;

            //ordre descendent
            //if (alumneEdat1>=alumneEdat2) return -1;
            //else return 1;
        }};

    //ALTRES MÈTODES
    public void saluda() {
        System.out.println("Hola, sóc un alumne i em dic " + nom);
    }
}
```

Tot seguit continuem amb una classe Test que ens ajudi a testejar la classe Alumne:

```java
import org.junit.Test;
import static org.junit.Assert.*;
public class AlumneTest {

    @Test
    public void getEdat() throws Exception {
        Alumne a = new Alumne();
        assertEquals(18, a.getEdat());


        Alumne a2 = new Alumne(26, "","");
        assertEquals(26, a2.getEdat());

    }

    @Test
    public void getNom() throws Exception {
        Alumne a = new Alumne();
        assertEquals("", a.getNom());


        Alumne a2 = new Alumne("Ramon","");
        assertEquals("Ramon", a2.getNom());
    }

    @Test
    public void getCognoms() throws Exception {
        Alumne a = new Alumne();
        assertEquals("", a.getCognoms());


        Alumne a2 = new Alumne("","Torres");
        assertEquals("Torres", a2.getCognoms());
    }

    @Test
    public void setEdat() throws Exception {
        Alumne a = new Alumne();
        a.setEdat(20);
        assertEquals(20, a.getEdat());
    }

    @Test
    public void setNom() throws Exception {
        Alumne a = new Alumne();
        a.setNom("Miquel");
        assertEquals("Miquel", a.getNom());
    }

    @Test
    public void setCognoms() throws Exception {
        Alumne a = new Alumne();
        a.setCognoms("Torres");
        assertEquals("Torres", a.getCognoms());
    }

    @Test
    public void testClone() throws Exception {
        Alumne a = new Alumne();
        Alumne clon = (Alumne)a.clone();
        assertEquals(a,clon);

        Alumne a2 = new Alumne(30, "Mireia", "Ramirez");
        Alumne copia = new Alumne(a2);
        assertEquals(a2,copia);
    }

    @Test
    public void equals() throws Exception {
        Alumne a = new Alumne(20,"Joan","Rius");
        Alumne b = new Alumne (20,"Joan","Rius");
        assertEquals(a,b);
        assertNotNull(a);
        a = null;
        assertNull(a);
    }

    @Test
    public void testToString() throws Exception {
        Alumne a = new Alumne();
        assertEquals("Alumne{edat=18, nom='', cognoms=''}", a.toString());

        Alumne a2 = new Alumne(28,"Maria","Romero");
        assertEquals("Alumne{edat=28, nom='Maria', cognoms='Romero'}", a2.toString());
    }

```

Ara definim la classe Classe (com serà una classe amb alumnes)

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Comparator;
public class Classe implements Cloneable{

    private String grup;
    private String aula;
    private ArrayList<Alumne> alumnes = new ArrayList<>();

    //CONSTRUCTORES
    public Classe(){


    }

    public Classe(String grup, String aula, ArrayList<Alumne> grupAlumne){
        this.grup = grup;
        this.aula = aula;
        this.alumnes = grupAlumne;
    }

    //CÒPIA OBJECTE
    public Classe (Classe classe){
        this.grup = classe.getGrup();
        this.aula = classe.getAula();
        this.alumnes = classe.getAlumnes();
    }

    //GETTERS
    public String getGrup() {
        return grup;
    }


    public String getAula() {
        return aula;
    }

    public ArrayList<Alumne> getAlumnes() {
        return alumnes;
    }

    public Alumne getAlumne(int posicio) {
        return alumnes.get(posicio);
    }


    //SETTERS
    public void setGrup(String grup) {
        this.grup = grup;
    }

    public void setAula(String aula) {
        this.aula = aula;
    }

    public void setAlumnes(ArrayList<Alumne> alumnes) {
        this.alumnes = alumnes;
    }


    //Mètodes típics de llistes
    public void afegirAlumne(Alumne a){
        alumnes.add(a);
    }

    public boolean esBuit(){
        return alumnes.size()==0;
    }

    public boolean existeixAlumne(Alumne a){
        return alumnes.contains(a);
    }

    public int posicioAlumne(Alumne a){
        return alumnes.indexOf(a);
    }

    public void eliminarAlumne(Alumne a){
        alumnes.remove(a);
    }

    //MÈTODES SOBREESCRITS
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;

        Classe classe = (Classe) o;

        if (!grup.equals(classe.grup)) return false;
        if (!aula.equals(classe.aula)) return false;
        return alumnes.equals(classe.alumnes);
    }

    @Override
    public int hashCode() {
        int result = grup.hashCode();
        result = 31 * result + aula.hashCode();
        result = 31 * result + alumnes.hashCode();
        return result;
    }

    @Override
    public String toString() {
        return "Classe{" +
                "grup='" + grup + '\'' +
                ", aula='" + aula + '\'' +
                ", alumnes=" + alumnes +
                '}';
    }

}

```

Finalment anem a crear el programa principal.

```java
import java.util.Scanner;

public class AlumneClasseMain {

    public static void main(String args[]){

        //Anem a crear una classe de 5 estudiants
        Classe classe = new Classe();

        Scanner sc = new Scanner(System.in);
        System.out.println("Introdueix el nom del grup");
        String grup = sc.nextLine();
        classe.setGrup(grup);
        System.out.println();
        System.out.println("Introdueix el nom de l'aula");
        String aula = sc.nextLine();
        classe.setAula(aula);
        System.out.println();

        System.out.println("Introduim 5 alumnes");
        Alumne a = new Alumne(20, "Amos", "Ledesma");
        classe.afegirAlumne(a);
        a = new Alumne(21, "Roger","Polo");
        classe.afegirAlumne(a);
        a = new Alumne(25, "Oriol","Benito");
        classe.afegirAlumne(a);
        a = new Alumne(28, "Joaquim","Rocamora");
        classe.afegirAlumne(a);
        a = new Alumne(18, "Hector", "Peris");
        classe.afegirAlumne(a);
        System.out.println();

        System.out.println("Imprimim la classe:" + classe);
        System.out.println();

        System.out.println("L'aula està buida? " + classe.esBuit());
        System.out.println();

        System.out.println("Si l'alumne 'a' existeix imprimeix-lo i diga'n la seva posició ");
        if(classe.existeixAlumne(a)){
            System.out.println("L'alumne 'a' és :" + a);
            System.out.println("L'alumne 'a' es troba a la posició :" + classe.posicioAlumne(a));
            System.out.println("Eliminem aquest alumne :");
            classe.eliminarAlumne(a);
        }
        System.out.println();

        System.out.println("Modifiquem informació de l'alumne 3 i a partir d'ara es dirà Pere Benitez i té 18 anys.");
        classe.getAlumne(3).setNom("Pere");
        classe.getAlumne(3).setCognoms("Benitez");
        classe.getAlumne(3).setEdat(18);
        System.out.println();
        System.out.println();

        System.out.println("Imprimim l'alumne 3" + classe.getAlumne(3));
    }
}

```
