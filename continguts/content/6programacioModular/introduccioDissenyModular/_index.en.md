---
date: 2016-04-09T16:50:16+02:00
title: Introducció Disseny Modular
weight: 1
---

El paradigma de programació utilitzat fins ara ha estat el de la programació estructurada, consistent en tractar de desenvolupar programes més fiables i fàcils de mantenir mitjançant la utilització exclusiva de 3 estructures de control: la seqüencial, l'alternativa i la iterativa.

Quan els programes comencen a créixer i es tornen difícils de resoldre en conjunt per la seva gran envergadura, la programació estructurada **afavoreix la divisió del problema en parts més petites** que poden ser abordades més fàcilment per separat. Es tracta del principi de **"divideix i guanyaràs"**.

La programació funcional, en el marc conceptual què estem tractant, consisteix justament en aplicar aquesta tècnica de divideix i venceràs per separar un programa en parts més senzilles, anomenades **funcions**.

{{% notice note %}}
**Programació funcional:** dividir un programa en funcions específiques dins del mateix arxiu. <br> **Programació modular:** consisteix a agrupar en arxius separats un conjunt de funcions més genèriques i que guardin alguna relació entre elles amb la finalitat que puguin ser reutilitzades entre programes.
{{% /notice %}}


### 1. Subprogrames i mòduls
El concepte de **subprograma** s’utilitza normalment per identificar un conjunt d’instruccions que conjuntament desenvolupen una tasca concreta i que pot ser (o no) necessària en diferents llocs del programa.
El concepte de **mòdul** es destina normalment a identificar grans apartats d’una aplicació


### 2. Accions, funcions i mètodes

Els subprogrames es classifiquen en:

1. **Acció** és un conjunt d’instruccions amb un objectiu comú, que pot necessitar o no dades externes per a la seva execució i que **NO retorna** cap resultat a qui l'ha cridat.

2. **Funció** és un conjunt d’instruccions amb un objectiu comú, que pot necessitar o no dades externes per a la seva execució i que **Retorna** un resultat a qui l’ha cridat.

El llenguatge Java és orientat a objectes, i per tant tot s'encapsula dins de classes. En aquest context les accions i funcions s'implementen amb una estructura definida dins d'una classe i anomenada **mètode**.

Quan codifiquem un mètode tindrem els següents elements:
* *Signatura* o capçalera del mètode: Està composta per:
    - El *nom* del mètode.
    - Els *arguments* del mètode: ens informen de quins paràmetres obtenim per tal de poder usar dins el mètode. Si el llenguatge de programació usa tipus de dades, com Java, també ens especificarà de quin tipus de dades és cadascun d'aquests arguments.
    - *Tipus* de dada que retorna el mètode: només s'especificarà si el llenguatge de programació usa tipus de dades, com Java.

* *Cos del mètode*: Defineix l'algoritme que executarà el mètode. Dins del cos del mètode hi haurà el retorn del mètode on es posarà quina dada es retorna (si és que es retorna alguna dada). 

Quan parlem de **la crida** a un mètode, ens referim a fer ús d'aquesta mètode des d'un altre mètode (ja sigui des de la mateixa classe o no). 

#### Exemple de funció i acció

Si per exemple tenim la següent funció:

```java 
public static int sumaFuncio(int a, int b){
    int resultat;
    resultat = a + b;
    return resultat;
}

```

- La *signatura* és: ``public static int sumaFuncio(int a, int b)``
- El *nom* ``suma``
- Els *arguments*: ``(int a, int b)``
- *Tipus* de dades que retorna ``int``
- El *cos* són les tres instruccions de dins la funció.


Com podem comprovar l'anterior mètode es una funció ja que retorna un enter. Si volguéssim canviar aquesta funció per una acció (subprograma que no retorna cap valor) ho faríem de la següent manera:

```java 
public static void sumaAccio(int a, int b){
    int resultat;
    resultat = a + b;
    System.out.println(resultat);
}
```

Fixeu-vos que hem canviat int -> void i ara ja no retornem res, sinó que ho escrivim per pantalla.

Si volem efectuar la *crida* dins el main del nostre programa faríem el següent per una funció i per una acció:

```java
public static void main(String args[]){
    int res = sumaFuncio(2,3);
    System.out.println(res);

    sumaAccio(2,3);
}
```

### 3. Accessibilitat de les variables

Les **variables globals** són les variables tals que el seu àmbit de validesa i disponibilitat és total, és a dir, es poden utilitzar, actualitzant-les o no, des del programa principal i des de tots els subprogrames. No és aconsellable l'ús de variables globals. Les definim just després de la declaració de la classe, per ex:

```java 
public class Main{
public static int variableGlobal;
...
```

Una **variable local** és aquella que està declarada dins d’un subprograma. L’àmbit d’ús de les variables locals és el subprograma en què s’han definit. L’àmbit d’existència d’una variable és la part de la classe en què la variable pot ser
referenciada o s’hi pot accedir pel seu nom.

En Java, quan declarem una variable, aquesta és accessible només dins l'estructura on es declarada. En el cas dels arguments, només són visibles en el mètode en el qual s'usen. Posem un exemple:

```java 
public double m2km (double m)
{
    double km;
    km = m / 1000;
    return km;
}
```

En aquest cas les variables m i km només són accessibles dins del mètode m2km.

Un altre exemple:

```java 
public int sumElements (int[] array)
{
    int sum = 0;

    for(int i = 0; i < array.length; i++)
        sum = sum + array[i];
 
    return sum;
}
```

Les variables sum i array només són accessibles dins del mètode sumElements, però
la variable i només és visible dins del for.


### 4. Pas per valor o per referència

Arguments o paràmetres
Els **arguments o paràmetres formals** són les dades que apareixen a la signatura de la funció.

Els **paràmetres o paràmetres actuals** són les dades transferides en la crida d'una funció.


Transferència per valor o per referència:
1. En la **transferència per valor**, el valor del paràmetre actual es **copia** en una altra posició de memòria, a la qual es pot accedir pel nom del paràmetre formal. Aquesta NO ÉS la variable inicial, n'és una còpia del seu valor en una altra posició de memòria.

2. En la **transferència per referència**, el subprograma rep **l’adreça de memòria* en què es troba el paràmetre actual, a la qual es pot accedir llavors pel nom del paràmetre formal. Per això en manipular una variable passada per referència es modifica l'original ja que actua sobre la MATEIXA posició de memòria.

{{% notice note %}}
**A Java, les dades simples es passen per valor i les compostes (com els arrays o els Strings) es passen per referència.**
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

*Observació:* les cadenes (tipus String) són objectes, però són immutbales, per tant **no**
poden canviar el seu valor


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
```

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
