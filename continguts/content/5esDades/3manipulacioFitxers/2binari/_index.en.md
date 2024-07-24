---
title: Binari
weight: 2
pre: "3.2. "
---


##### L/E byte a byte

FileInputStream: [http://docs.oracle.com/javase/8/docs/api/java/io/FileInputStream.html](http://docs.oracle.com/javase/8/docs/api/java/io/FileInputStream.html)

FileOutputStream: [http://docs.oracle.com/javase/8/docs/api/java/io/FileOutputStream.html](http://docs.oracle.com/javase/8/docs/api/java/io/FileOutputStream.html)


#####    L/E per bytes amb buffer (més eficient)

BufferedInputStream: [http://docs.oracle.com/javase/8/docs/api/java/io/BufferedInputStream.html](http://docs.oracle.com/javase/8/docs/api/java/io/BufferedInputStream.html)

BufferedOutputStream: [http://docs.oracle.com/javase/8/docs/api/java/io/BufferedOutputStream.html](http://docs.oracle.com/javase/8/docs/api/java/io/BufferedOutputStream.html)


#### Lectura fitxer binari

Com s'observa en cada exemple permet llegir d'un ArrayList o bé d'un Array. Els dos primers exemples fan referència al FileInputStream i els dos últims al BufferInputStream. Proveu la lectura d'una imatge per exemple, o un fitxer binari i observeu que passa amb els temps.

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