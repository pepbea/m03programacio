---
title: Binari
weight: 2
pre: "2.2. "
---

Els fitxers binaris emmagatzemen dades en format no llegible per als humans, és a dir, en format binari. Això és útil per emmagatzemar dades que no són textuals, com ara imatges, fitxers de vídeo, o objectes serialitzats. 

Els fitxers s'emmagatzemen com a seqüència de bits. Això permet que sigui **més compacte i eficient** en quant a espai i temps de processament que en un fitxer de text, ja que no cal conversions addicionals. Per altra banda, els fitxers binaris **no són legibles pels humans** i poden ser incompatibles entre diferents sistemes operatius, plataformes, o llenguatges de programació.

##### L/E byte a byte

FileInputStream: [https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/FileInputStream.html](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/FileInputStream.html)

FileOutputStream: [https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/FileOutputStream.html](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/FileOutputStream.html)


#####    L/E per bytes amb buffer (més eficient)

BufferedInputStream: [https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/BufferedInputStream.html](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/BufferedInputStream.html)

BufferedOutputStream: [https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/BufferedOutputStream.html](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/BufferedOutputStream.html)


#### Lectura fitxer binari

Com s'observa en cada exemple permet llegir d'un ArrayList o bé d'un Array. Els dos primers exemples fan referència a FileInputStream i els dos últims a BufferInputStream. Proveu la lectura d'una imatge per exemple, o un fitxer binari i observeu que passa amb els temps.

``` java
package exemples;

import java.io.BufferedInputStream;
import java.io.FileInputStream;
import java.util.ArrayList;
import java.util.Arrays;

public class LBinari {

	public static void main(String[] args) {
		long time_start, time_end;
		time_start = System.currentTimeMillis();
		System.out.print(llegirFitxerBinari2AList("f1.txt"));
		time_end = System.currentTimeMillis();
		System.out.println("the task has taken "+ ( time_end - time_start ) +" milliseconds");
		System.out.println();


		time_start = System.currentTimeMillis();
		System.out.print(Arrays.toString(llegirFitxerBinari2Array("f1.txt")));
		time_end = System.currentTimeMillis();
		System.out.println("the task has taken "+ ( time_end - time_start ) +" milliseconds");
		System.out.println();
		System.out.println();
		
		System.out.println("\n");
		time_start = System.currentTimeMillis();
		System.out.print(llegirFitxerBinariBuffered("f1.txt"));
		time_end = System.currentTimeMillis();
		System.out.println("the task has taken "+ ( time_end - time_start ) +" milliseconds");
		
		System.out.println();


		time_start = System.currentTimeMillis();
		System.out.print(Arrays.toString(llegirFitxerBinari2ArrayBuffered("f1.txt")));
		time_end = System.currentTimeMillis();
		System.out.println("the task has taken "+ ( time_end - time_start ) +" milliseconds");
		System.out.println();
		System.out.println();
	}
	
	
	/**
	 * Llegeix el contingut d'un fitxer byte a byte.
	 * @param path Path del fitxer de text plà.
	 * @return ArrayList de bytes amb el contingut del fitxer.
	 */
	public static ArrayList<Byte> llegirFitxerBinari2AList(String path) {
		try {
			ArrayList<Byte> res = new ArrayList<Byte>();

			FileInputStream fis = new FileInputStream(path);
			byte b;
			while ((b = (byte)fis.read()) != -1) {
				res.add(b);
			}
			fis.close();
			return res;
		}
		catch (Exception e) {
			System.out.println(e.getMessage());
			return null;
		}
	}

	/**
	 * Llegeix el contingut d'un fitxer byte a byte.
	 * @param path Path del fitxer de text plà.
	 * @return Array de bytes amb el contingut del fitxer.
	 */
	public static byte[] llegirFitxerBinari2Array(String path) {
		try {
			FileInputStream fis = new FileInputStream(path);
			int len = fis.available();
			byte[] res = new byte[len];
			fis.read(res);
			fis.close();
			return res;
		}
		catch (Exception e) {
			System.out.println(e.getMessage());
			return null;
		}
	}

	/**
	 * Llegeix el contingut d'un fitxer byte a byte, usant classes buffered.
	 * @param path Path del fitxer de text plà.
	 * @return ArrayList de bytes amb el contingut del fitxer.
	 */
	public static ArrayList<Byte> llegirFitxerBinariBuffered(String path) {
		try {
			ArrayList<Byte> res = new ArrayList<Byte>();

			BufferedInputStream bis = new BufferedInputStream(new FileInputStream(path));
			byte b;
			while ((b = (byte)bis.read()) != -1) {
				res.add(b);
			}
			bis.close();
			return res;
		}
		catch (Exception e) {
			System.out.println(e.getMessage());
			return null;
		}
	}

	/**
	 * Llegeix el contingut d'un fitxer byte a byte, usant classes buffered.
	 * @param path Path del fitxer de text plà.
	 * @return Array de bytes amb el contingut del fitxer.
	 */
	public static byte[] llegirFitxerBinari2ArrayBuffered(String path) {
		try {
			BufferedInputStream bis = new BufferedInputStream(new FileInputStream(path));
			int len = bis.available();
			byte[] res = new byte[len];
			bis.read(res);
			bis.close();
			return res;
		}
		catch (Exception e) {
			System.out.println(e.getMessage());
			return null;
		}
	}
}
```

Un dels principals problemes d'eficiència en el tractament de fitxers consisteix en **minimitzar l'accés a disc** per aconseguir les dades que ens demanen. Mitjançant els `wrappers` de Buffer ens permet lectures i escriptures on podem aconseguir més dades que si no utilitzessim la classe de Buffer, així doncs amb menys accessos aconseguim les mateixes dades i per tant fem el programa més eficient. (És molt més eficient fer una lectura/escriptura de 10k que realitzar 10k lectures/escriptures d'un 1B).

