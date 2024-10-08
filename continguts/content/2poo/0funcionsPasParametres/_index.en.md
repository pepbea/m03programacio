---
title: Funcions i pas de paràmetres
weight: 1
pre: "0. "
chapter: false
---

El paradigma de programació utilitzat fins ara ha estat el de la programació estructurada, consistent en tractar de desenvolupar programes més fiables i fàcils de mantenir mitjançant la utilització exclusiva de 3 estructures de control: la seqüencial, l'alternativa i la iterativa.

Quan els programes comencen a créixer i es tornen difícils de resoldre en conjunt per la seva complexitat, és necessari optar per particionar el codi en porcions petites i estructurades que poden ser abordades més fàcilment per separat. Es tracta del principi de **"divideix i guanyaràs"**.

La **programació funcional** consisteix en aplicar aquesta tècnica de divideix i venceràs per separar un programa en parts més senzilles, anomenades **funcions**. És el pas previ a treballar amb la Programació Orientada a Objectes (POO).


#### Funció

{{% notice note %}}
**Una funció** es defineix com un conjunt d’instruccions que desenvolupen una tasca concreta i que pot ser (o no) necessària en diferents llocs del programa. Una funció té un conjunt d'instruccions que la defineixen i pot ser "executada" en diferents parts del nostre programa, cada vegada que es "crida" la mateixa.
{{% /notice %}}

Les funcions **poden necessitar o no dades externes** que es passen com a paràmetres d'entrada i **poden retornar o no** un resultat a qui l'hagi cridat com a paràmetre de sortida.

El llenguatge Java segueix el paradigma de l'orientació a objectes, i per tant tot s'estructura a partir de  classes. En aquest context les funcions s'implementen dins una estructura d'una classe i cada funció s'anomena **mètode** d'aquesta classe.

Quan codifiquem un mètode tindrem els següents elements:
* **Signatura** o capçalera del mètode: Està composta per:
    - El _nom_ del mètode.
    - Els *arguments* del mètode: ens informen de quins paràmetres obtenim per tal de poder usar dins el mètode. Si el llenguatge de programació usa tipus de dades, com Java, també ens especificarà de quin tipus de dades és cadascun d'aquests arguments.
    - *Tipus* de dada que retorna el mètode: només s'especificarà si la funció retorna un paràmetre, sinó en el cas de Java, si no retorna cap paràmetre el tipus serà void.

* **Cos del mètode**: Defineix el bloc d'instruccions que executarà el mètode. Dins del cos del mètode hi haurà el retorn del mètode on es posarà quina dada es retorna (si és que es retorna alguna dada). 

Quan parlem de **la crida** a un mètode, ens referim a fer ús d'aquest mètode des d'un altre mètode (ja sigui des de la mateixa classe o no).


#### Exemple de funció que retorna un valor i funció que no retorna un valor

Si per exemple tenim la següent funció:

```java 
public static int sumaFuncioRetornaValor(int a, int b){
    int resultat;
    resultat = a + b;
    return resultat;
}

```

- La *signatura* és: ``public static int sumaFuncioRetornaValor(int a, int b)``
- El *nom* ``sumaFuncioRetornaValor``
- Els *arguments*: ``(int a, int b)``
- *Tipus* de dades que retorna ``int``
- El *cos* són les tres instruccions de dins la funció.


Com podem comprovar l'anterior mètode es una funció ja que retorna un enter. Si volguéssim canviar aquesta funció per una altra que no retorni cap valor ho faríem de la següent manera:

```java 
public static void sumaFuncioNoRetornaValor(int a, int b){
    int resultat;
    resultat = a + b;
    System.out.println(resultat);
}
```

Fixeu-vos que hem canviat int -> void i ara ja no retornem res, sinó que ho escrivim per pantalla.

Si volem efectuar la *crida* dins el main del nostre programa faríem el següent per una funció i per una acció:

```java
public static void main(String args[]){
    int res = sumaFuncioRetornaValor(2,3);
    System.out.println(res);

    sumaFuncioNoRetornaValor(2,3);
}
```

### Pas per valor o per referència

Arguments o paràmetres
Els **paràmetres formals** són les dades que apareixen a la signatura de la funció.

Els **paràmetres actuals** són les dades transferides en la crida d'una funció.


Transferència per valor o per referència:
1. En la **transferència per valor**, el valor del paràmetre actual es **copia** en una altra posició de memòria, a la qual es pot accedir pel nom del paràmetre formal. Aquesta NO ÉS la variable inicial, n'és una còpia del seu valor en una altra posició de memòria.

2. En la **transferència per referència**, el subprograma rep **l’adreça de memòria** en què es troba el paràmetre actual, a la qual es pot accedir llavors pel nom del paràmetre formal. Per això en manipular una variable passada per referència es modifica l'original ja que actua sobre la MATEIXA posició de memòria.

{{% notice note %}}
**A Java, les dades primitives i els Strings es passen per valor i les compostes (com els arrays o altres objectes) es passen per referència.**
{{% /notice %}}

####  Exemple: Pas per valor o per referència
Pas de paràmetres per valor o per referència. En aquest exemple es veu la diferència de passar un valor o de passar la referència on es troba aquest valor.
```java
public class Parametres {

	// Paràmetres passats per valor perquè són de tipus simple
	public static void intercanvi(int a, int b)
	{
		System.out.println("Dins del mètode intercanvi:");
		System.out.println("a = " + a);
		System.out.println("b = " + b);

		int temp = a;
		a = b;
		b = temp;

		System.out.println("a = " + a);
		System.out.println("b = " + b);
	}
	
	// Paràmetres passats per referència perquè és de tipus compost (un objecte)
	public static void intercanviArray(int[] v)
	{
		System.out.println("Dins del mètode intercanviArray:");
		System.out.println("v[0] = " + v[0]);
		System.out.println("v[1] = " + v[1]);

		int temp = v[0];
		v[0] = v[1];
		v[1] = temp;

		System.out.println("v[0] = " + v[0]);
		System.out.println("v[1] = " + v[1]);
	}
	
	// Main()
	public static void main(String[] args) {
		//
		// Exemple de pas de paràmetres per valor
		//
		System.out.println("PER VALOR");
		int x = 5;
		int y = 10;
		
		System.out.println("x = " + x);
		System.out.println("y = " + y);
		System.out.println("Cridem intercanvi(x, y)");
		
		intercanvi(x, y);

		System.out.println("Tornem del mètode intercanvi(x, y)");
		System.out.println("x = " + x);
		System.out.println("y = " + y);
		System.out.println();

		
		//
		// Exemple de pas de paràmetres per referència
		//
		System.out.println("PER REFERÈNCIA");
		int[] array = {25, 50};

		System.out.println("array[0] = " + array[0]);
		System.out.println("array[1] = " + array[1]);
		System.out.println("Cridem intercanviArray(array)");
		
		intercanviArray(array);

		System.out.println("Tornem del mètode intercanviArray(array)");
		System.out.println("array[0] = " + array[0]);
		System.out.println("array[1] = " + array[1]);
		System.out.println();

		
		//
		//Un altre exemple de pas per valor
		//
		System.out.println("PER VALOR");
		System.out.println("array[0] = " + array[0]);
		System.out.println("array[1] = " + array[1]);
		System.out.println("Cridem intercanvi(array[0], array[1])");
		
		intercanvi(array[0], array[1]);

		System.out.println("Tornem del mètode intercanvi(array[0], array[1])");
		System.out.println("array[0] = " + array[0]);
		System.out.println("array[1] = " + array[1]);
	}

}
```

*Observació:* les cadenes (tipus String) són objectes, però són immutables, per tant **no**
poden canviar el seu valor

### Exemples

**Exemple1: Funció suma senzilla**
Realitzem la suma de dos nombres dins una funció i en retornem el resultat al programa principal:
```java
public class Suma
{
	public static void main(String[] args)
	{
		int res;
		int num = 25;
		
		// Exemples d'ús d'un mètode
		res = suma(2, 3);
		System.out.println("suma = " + res);

		res = suma(num, 10);
		System.out.println("suma = " + res);

		res = suma(res, num);
		System.out.println("suma = " + res);
	}
	
	// Mètode que fa la suma de dos nombres enters
	public static int suma (int a, int b)
	{
		int s;
		s = a + b;
		return s;
	}
}
```

<br>

**Exemple2: Paràmetres del programa**

```java
public class ProvaArgs
{
	/**
	 * Imprimeix per pantalla tots els paràmetres passats en l'execució del programa
	 * @param args Paràmetres al executar el programa
	 */
	public static void main(String[] args)
	{
		for (int i=0; i<args.length; i++)
		{
			System.out.println("Paràmetre " + i + " = " + args[i]);
		}
	}
}
```