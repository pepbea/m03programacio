---
title: Text
weight: 1
pre: "2.1. "
---

Els fitxers de text emmagatzemen dades en format llegible per als humans, amb caràcters codificats, com ara l'ASCII o l'UTF-8.

#### L/E caràcter a caràcter (de fitxers de text plà)

FileReader: [https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/FileReader.html](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/FileReader.html)

FileWriter: [https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/FileWriter.html](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/FileWriter.html)


#### L/E per caràcters amb buffer (més eficient)

BufferedReader: [https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/BufferedReader.html](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/BufferedReader.html)

BufferedWriter: [https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/BufferedWriter.html](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/BufferedWriter.html)



#### Lectura d'un fitxer de text

Lectura d'un fitxer utilitzant FileReader i BufferedReader. Observeu que calculem el temps en realitzat el mateix amb dos fitxers diferents. Com que utilitzant FileReader l'accés de Lectura al fitxer és caràcter a caràcter és molt més lent que si podem llegir les dades del buffer amb BufferedReader ja que podem realitzar lectures línia a línia i a més es poden emmagatzemar en el buffer que genera la classe BufferedReader.

``` java
package exemples;

import java.io.BufferedReader;
import java.io.FileReader;

public class LTextPla {

	public static void main(String[] args) {
		

		long time_start, time_end;
		time_start = System.currentTimeMillis();
		System.out.print(llegirFitxerTextPla("f1.txt"));
		time_end = System.currentTimeMillis();
		System.out.println("the task has taken "+ ( time_end - time_start ) +" milliseconds");
		System.out.println();
		System.out.println();


		time_start = System.currentTimeMillis();
		System.out.print(llegirFitxerTextPlaBuffered("f1.txt"));
		time_end = System.currentTimeMillis();
		System.out.println("the task has taken "+ ( time_end - time_start ) +" milliseconds");
	}
	
	/**
	 * Llegeix el contingut d'un fitxer de text plà caràcter a caràcter.
	 * @param path Path del fitxer de text plà.
	 * @return Contingut del fitxer.
	 */
	public static String llegirFitxerTextPla(String path) {
		try {
			String res = "";

			FileReader fr = new FileReader(path);
			int ch = fr.read();
			while (ch != -1) {
				res = res + (char)ch;
				ch = fr.read();
			}
			fr.close();
			return res;
		}
		catch (Exception e) {
			System.out.println(e.getMessage());
			return null;
		}
	}

	/**
	 * Llegeix el contingut d'un fitxer de text plà accedint amb buffer.
	 * @param path Path del fitxer de text plà.
	 * @return Contingut del fitxer.
	 */
	public static String llegirFitxerTextPlaBuffered(String path) {
		try {
			String res = "";

			FileReader fr = new FileReader(path);
			BufferedReader br = new BufferedReader(fr);
			String linia = br.readLine();

			while (linia != null) {
				res = res + linia + "\n"; //readLine() no inclou els salts de línia.
				linia = br.readLine();
			}

			br.close();
			return res;
		}
		catch (Exception e) {
			System.out.println(e.getMessage());
			return null;
		}
	}
}
```

Una altra manera de llegir un fitxer que sabem que conté diferents tipus de dades i on estan ubicades seria utilitzant el Scanner però enlloc de passar-li l'entrada estàndard `System.in` que venim fent fins ara (ja que llegíem de teclat), ara passem a llegir de Fitxer (Scanner permet que com a paràmetre li passem un Fitxer que és l'origen de les dades). Quedaria de la següent manera:

```java
import java.io.File;
import java.util.Scanner;
...

public static void main(String args[]) {
try{
	File file = new File("/home/pbea/Documents/textFile.txt");
	PrintWriter pwr = new PrintWriter(file);
	for (int i = 1; i <= 1000; i++) {
		pwr.print(i + " ");
		if (i % 100 == 0) pwr.println();
	}
	pwr.close();

	Scanner lector = new Scanner(file);
	while(scn.hasNext())
		System.out.println("Valor: " + scn.nextInt());

	scn.close();
}catch (IOException e) { 
	System.out.println(e.getMessage()); 
}
...
```


#### Escriptura d'un fitxer de text

De nou tenim un exemple amb FileWriter i BufferedFileWriter. A destacar d'aquí la creació del FileWriter, observeu que té un segon paràmetre booleà, això ens permet començar l'escriptura a l'inici del fitxer (truncar el fitxer) amb l'opció false, mentre que true ens permet afegir el contingut al final del fitxer. És important que tanquem els fitxers, sobretot els que són per escriptura ja que així ens assegurem que el pròxim cop que s'obre hi haurà la informació que acabem d'escriure. En el cas del BufferedFileWriter s'escriu en el fitxer quan el buffer està ple o quan cridem al mètode `flush()`.


``` java
package exemples;

import java.io.BufferedWriter;
import java.io.FileWriter;

public class ETextPla {

	public static void main(String[] args) {
		
		EscriureFitxerTextPla("f2.txt", "\nHola");
		EscriureFitxerTextPlaBuffered("f3.txt", "Hola amb buffer.\n");
		System.out.println("Done.");
	}
	
	/**
	 * Escriu un String a un fitxer de text plà.
	 * @param path Path del fitxer de text plà.
	 * @param text Text a escriure.
	 */
	public static void EscriureFitxerTextPla(String path, String text) {
		try {
			FileWriter fw = new FileWriter(path, true); // true = afegir al fitxer
			fw.write(text);
			fw.close();
		}
		catch (Exception e) {
			System.out.println(e.getMessage());
		}
	}

	/**
	 * Llegeix el contingut d'un fitxer de text plà accedint amb buffer.
	 * @param path Path del fitxer de text plà.
	 * @param text Text a escriure.
	 */
	public static void EscriureFitxerTextPlaBuffered(String path, String text) {
		try {
			FileWriter fw = new FileWriter(path, false); // false = truncar el fitxer
			BufferedWriter bw = new BufferedWriter(fw);
			bw.write(text);
			bw.close();
		}
		catch (Exception e) {
			System.out.println(e.getMessage());
		}
	}
}
```