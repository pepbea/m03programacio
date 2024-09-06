---
title: Accés aleatori
weight: 3
pre: "3.3. "
---


#### Accés aleatori

RandomAccessFile: [https://docs.oracle.com/javase/8/docs/api/java/io/RandomAccessFile.html](https://docs.oracle.com/javase/8/docs/api/java/io/RandomAccessFile.html)


#### Altres classes

PrintWritter: [https://docs.oracle.com/javase/8/docs/api/java/io/PrintWriter.html](https://docs.oracle.com/javase/8/docs/api/java/io/PrintWriter.html)

PrintStream: [https://docs.oracle.com/javase/8/docs/api/java/io/PrintStream.html](https://docs.oracle.com/javase/8/docs/api/java/io/PrintStream.html)

DataInputStream: [https://docs.oracle.com/javase/8/docs/api/java/io/DataInputStream.html](https://docs.oracle.com/javase/8/docs/api/java/io/DataInputStream.html)

DataOutputStream: [https://docs.oracle.com/javase/8/docs/api/java/io/DataOutputStream.html](https://docs.oracle.com/javase/8/docs/api/java/io/DataOutputStream.html)

#### Exemple de RandomAccessFile

Observa diferents circumstàncies d'ús d'aquesta classe. És molt útil quan guardem informació en un fitxer de text i sabem la posició exacta on hi ha cada peça d'informació. Aquesta classe permet moure'ns per tot el fitxer, sense haver de fer-ho seqüencialment, sinó que permet posar el punter de L/E en qualsevol posició del fitxer.

``` java
package exemples;

import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.RandomAccessFile;

public class RAF {

	public static void main(String[] args) {

		String path = "f1.txt";
		String data = "data";
		RandomAccessFile raf;

		try {
			// RAF L/E fitxer text plà
			// Lectura
			System.out.println("Fitxer " + path + ":");
			raf = new RandomAccessFile(path, "rw");		
			String line;
			while ((line = raf.readLine()) != null) {
				System.out.println(line);
			}
			// Escriptura
			//raf.writeChars("RAF\n");
			raf.close();

			System.out.println("\nFitxer " + data + ":");

			// RAF L/E fitxer binari
			int num = 1000000;
			raf = new RandomAccessFile(data, "rw");
			raf.seek(raf.length()); // Situem el cursor al final del fitxer
			//raf.seek(12); // Situem el cursos al byte 12, és a dir per sobreescriure el 4art int
			raf.writeInt(num);
			raf.seek(0); // Situem el cursor al principi del fitxer
			// Mentre la posició del cursor sigui més petita que el tamany del fitxer
			while (raf.getFilePointer() < raf.length()) {
				num = raf.readInt();
				System.out.println(num);
			}
			raf.close();
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}

}
```

#### DataInputStream i DataOutputStream

Aquesta classe es treballa àmpliament al M06 Accés a Dades, aquí ens quedem amb la idea que permet lectura i escriptura indicant el tipatge de la dada que estem treballant. L'exemple següent és utilitzant un enter (writeInt readInt).

``` java
package exemples;

import java.io.DataInputStream;
import java.io.DataOutputStream;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

public class DataIOStream {

	public static void main(String[] args) {

		String path = "fint.data";
		int num = 39568;
		
		try {
			// Escriure a un fitxer un int (4 bytes)
			// Si el fitxer no existeix es crea
			// Si el fitxer existeix el true del FileOutputStream fa que el int s'afegeixi al final
			DataOutputStream dos = new DataOutputStream(new FileOutputStream(path, true));
			dos.writeInt(num);
			dos.close();

			// Llegir un int (4 bytes) d'un fitxer.
			// Es llegeixen el 4 primers bytes del fitxer
			DataInputStream dis = new DataInputStream(new FileInputStream(path));
			System.out.println(dis.readInt());
			dis.close();
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}

```

#### Resum Recordatori

Aquest és un exemple que permet llegir fitxers de text caràcter a caràcter, llegir línies, llegir fitxers binaris d'enters, de reals o de bytes.

```java
package exemples;

import java.io.*;

public class LecturaFitxer
{
	public static void main (String[] args)
	{
		File f = new File ("Fitxer.txt");
		System.out.println("Tamany del fitxer en bytes: " + f.length());
		System.out.println("-----------------------------");
		System.out.println("Lectura com a fitxer de text plà caràcter a caràcter:");
		llegirCharAChar(f);
		System.out.println("-----------------------------");
		System.out.println("Lectura com a fitxer de text plà línia a línia:");
		llegirLiniaALinia(f);
		System.out.println("-----------------------------");
		System.out.println("Lectura com a fitxer binari llegint enters (4 bytes):");
		llegirBinariInt(f);
		System.out.println("-----------------------------");
		System.out.println("Lectura com a fitxer binari llegint reals (8 bytes):");
		llegirBinariReal(f);
		System.out.println("-----------------------------");
		System.out.println("Lectura com a fitxer binari llegint bytes:");
		llegirBinariByte(f);
	}

	public static void llegirCharAChar(File f)
	{
		try
		{
			BufferedReader in = new BufferedReader(new FileReader(f));
			char[] car = new char[1];
			String text = "";
			while((in.read(car, 0, 1)) > -1)
			{
				text = text + new String(car, 0, 1);

			}
			in.close();
			System.out.println(text);
		}
		catch(Exception e)
		{
			System.out.println("Error de fitxer: " + e.getMessage());
		}
	}
	
	public static void llegirLiniaALinia(File f)
	{
		try
		{
			BufferedReader in = new BufferedReader(new FileReader(f));
			String linia, text = "";
			while((linia = in.readLine()) != null)
			{
				text = text + linia;
				if (in.ready())
					text = text + "\n";

			}
			in.close();
			System.out.println(text);
		}
		catch(Exception e)
		{
			System.out.println("Error de fitxer: " + e.getMessage());
		}
	}
	
	public static void llegirBinariInt(File f)
	{
		try {
			RandomAccessFile raf = new RandomAccessFile(f, "r");
			long numInts = f.length()/4;
			for (int i = 0; i < numInts; i++) {
				System.out.println(raf.readInt());
			}
			raf.close();
		} catch (Exception e) {
			System.out.println("Error mostrant fitxer: " + e.getMessage());
		}
	}

	public static void llegirBinariReal(File f)
	{
		try {
			RandomAccessFile raf = new RandomAccessFile(f, "r");
			long numReals = f.length()/8;
			for (int i = 0; i < numReals; i++) {
				System.out.println(raf.readDouble());
			}
			raf.close();
		} catch (Exception e) {
			System.out.println("Error mostrant fitxer: " + e.getMessage());
		}
	}
	
	public static void llegirBinariByte(File f)
	{
		try {
			RandomAccessFile raf = new RandomAccessFile(f, "r");
			long numReals = f.length();
			for (int i = 0; i < numReals; i++) {
				System.out.println(raf.readByte());
			}
			raf.close();
		} catch (Exception e) {
			System.out.println("Error mostrant fitxer: " + e.getMessage());
		}
	}
}
```