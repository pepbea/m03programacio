---
title: Accés aleatori
weight: 3
pre: "2.3. "
---

#### Modes d'accés a fitxers

Moltes de les situacions que ens trobem en la L/E de fitxers són processos pensats per realitzar una lectura seqüencial, ara bé, podríem realitzar-ne també una lectura aleatòria si el que volem és accedir a un punt concret del fitxer on sabem que hi ha una determinada dada.

| Accés seqüencial | Accés aleatori |
| --- | --- |
| * Les dades es llegeixen i s'escriuen en ordre <br>* Si es vol accedir una dada situada al final del fitxer és necessari llegir abans totes les dades des de l'inici<br>* L'escriptura de dades es realitza a partir de la última dada escrita, no és possible realitzar insercions  enmig del document sense fer-ho utilitzant un algorisme<br>* Accés binari: FileInputStream, FileOutputStream<br>* Accés text: FileReader, FileWriter | * Permet accedir directament a una dada determinada sense necessitat de recorre les anteriors<br>* Les dades s'emmagatzemen en registres de tamany conegut, per tant si coneixem  els tipus ens podem moure saben el seu tamany en el fitxer<br>* RandomAccessFile |


En l'accés aleatori, es pot llegir o escriure en qualsevol part del fitxer sense seguir una seqüència predefinida. Això és útil quan es necessita accedir a una posició específica del fitxer, com ara en bases de dades emmagatzemades en fitxers o en fitxers amb registres d'una mida fixa. Java proporciona la classe `RandomAccessFile` per a aquest propòsit.

#### Accés aleatori

RandomAccessFile: [https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/RandomAccessFile.html](https://docs.oracle.com/javase/8/docs/api/java/io/RandomAccessFile.html)


#### Altres classes

PrintWritter: [https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/PrintWriter.html](https://docs.oracle.com/javase/8/docs/api/java/io/PrintWriter.html)

PrintStream: [https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/PrintStream.html](https://docs.oracle.com/javase/8/docs/api/java/io/PrintStream.html)

DataInputStream: [https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/DataInputStream.html](https://docs.oracle.com/javase/8/docs/api/java/io/DataInputStream.html)

DataOutputStream: [https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/DataOutputStream.html](https://docs.oracle.com/javase/8/docs/api/java/io/DataOutputStream.html)

#### Exemple de RandomAccessFile

Observa diferents circumstàncies d'ús d'aquesta classe. És molt útil quan guardem informació en un fitxer de text i sabem la posició exacta on hi ha cada peça d'informació. Aquesta classe permet moure'ns per tot el fitxer, sense haver de fer-ho seqüencialment, sinó que permet posar el punter de L/E en qualsevol posició del fitxer.

``` java
import java.io.File;
import java.io.IOException;
import java.io.RandomAccessFile;

public class RandomAccessFileExample {
    public static void main(String[] args) {
        String filePath = "example.dat";
        
        try {
            try (RandomAccessFile file = new RandomAccessFile(filePath, "rw")) {
                file.writeInt(12345);
                file.writeUTF("Hello, RandomAccessFile!");
                file.writeDouble(3.14159);
                
                System.out.println("File length after writing: " + file.length());
                System.out.println("Current file pointer after writing: " + file.getFilePointer());
            }
            
            // Lectura de Dades
            try (RandomAccessFile file = new RandomAccessFile(filePath, "r")) {
                System.out.println("File length before reading: " + file.length());
                int intValue = file.readInt();
                System.out.println("Integer value: " + intValue);
                
                // Llegeix la cadena partir de la posicio 4
                String stringValue = file.readUTF();
                System.out.println("String value: " + stringValue);
                
                // Llegeix el double a partir de la posicio 24
                double doubleValue = file.readDouble();
                System.out.println("Double value: " + doubleValue);
                
                // Posicio actual
                System.out.println("Current file pointer after reading: " + file.getFilePointer());
            }
            
            // Modificacio de dades
            try (RandomAccessFile file = new RandomAccessFile(filePath, "rw")) {
                // Moure cursor a l'inici i modifiquem int
                file.seek(0);
                file.writeInt(54321);
                
                // Ens movem a la posicio 24 i modifiquem double 
                file.seek(24);
                file.writeDouble(2.71828);
                
                System.out.println("File length after modifications: " + file.length());
                System.out.println("Current file pointer after modifications: " + file.getFilePointer());
            }
            
            // Llegim de nou per verificar els canvis
            try (RandomAccessFile file = new RandomAccessFile(filePath, "r")) {
                int intValue = file.readInt();
                System.out.println("Modified Integer value: " + intValue);
                String stringValue = file.readUTF();
                System.out.println("String value remains unchanged: " + stringValue);
                double doubleValue = file.readDouble();
                System.out.println("Modified Double value: " + doubleValue);
                System.out.println("Current file pointer after final reading: " + file.getFilePointer());
            }
            
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

#### DataInputStream i DataOutputStream

Aquesta classe es treballa àmpliament en el mòdul d'Accés a Dades, aquí ens quedem amb la idea que permet lectura i escriptura indicant el tipatge de la dada que estem treballant. L'exemple següent és utilitzant un enter (writeInt readInt).

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
			DataOutputStream dos = new DataOutputStream(new FileOutputStream(path, true));
			dos.writeInt(num);
			dos.close();

			// Llegir un int (4 bytes) d'un fitxer.
			// Es llegeixen el 4 primers bytes del fitxer
			DataInputStream dis = new DataInputStream(new FileInputStream(path));
			System.out.println(dis.readInt());
			dis.close();
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
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
		try(BufferedReader in = new BufferedReader(new FileReader(f))){
			char[] car = new char[1];
			String text = "";
			while((in.read(car, 0, 1)) > -1)
				text = text + new String(car, 0, 1);
				
			System.out.println(text);
		}
		catch(Exception e)
		{
			System.out.println("Error de fitxer: " + e.getMessage());
		}
	}
	
	public static void llegirLiniaALinia(File f)
	{
		try(BufferedReader in = new BufferedReader(new FileReader(f))){
			String linia, text = "";
			while((linia = in.readLine()) != null)
			{
				text = text + linia;
				if (in.ready())
					text = text + "\n";

			}
			System.out.println(text);
		}
		catch(Exception e)
		{
			System.out.println("Error de fitxer: " + e.getMessage());
		}
	}
	
	public static void llegirBinariInt(File f)
	{
		try(RandomAccessFile raf = new RandomAccessFile(f, "r")) {
			long numInts = f.length()/4;
			for (int i = 0; i < numInts; i++) {
				System.out.println(raf.readInt());
			}
		} catch (Exception e) {
			System.out.println("Error mostrant fitxer: " + e.getMessage());
		}
	}

	public static void llegirBinariReal(File f)
	{
		try(RandomAccessFile raf = new RandomAccessFile(f, "r")) {
			long numReals = f.length()/8;
			for (int i = 0; i < numReals; i++) {
				System.out.println(raf.readDouble());
			}
		} catch (Exception e) {
			System.out.println("Error mostrant fitxer: " + e.getMessage());
		}
	}
	
	public static void llegirBinariByte(File f)
	{
		try(RandomAccessFile raf = new RandomAccessFile(f, "r")) {
			long numReals = f.length();
			for (int i = 0; i < numReals; i++) {
				System.out.println(raf.readByte());
			}
		} catch (Exception e) {
			System.out.println("Error mostrant fitxer: " + e.getMessage());
		}
	}
}
```