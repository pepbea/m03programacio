---
title: Gestió de fitxers
weight: 1
pre: "1. "
---


Els fitxers són un conjunt de bytes guardats en memòria física que ens garanteix la seva persistència, de forma que sempre els tenim accessibles pel tractament de la informació que emmagatzemen.

#### File

La classe File és útil per portar la gestió sobre fitxers i carpetes en Java, proporciona una representació abstracta de fitxers i directoris, la seva especificació en Java Oracle és: [https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/File.html](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/File.html). Aquesta classe permet crear, eliminar, comprovar propietats, llistar continguts de directoris, gestionar rutes de fitxers, etc. Tot el que tingui a veure amb el maneig de fitxers en Java.

La classe File `no es fa servir per llegir o escriure dades` a un document determinat, sinó per accedir a la informació del fitxer o directori, com ara la ruta, la mida, els atributs, els permisos, etc. La resta de classes que manipulen fitxers parteixen de l‟existència d'una classe File, per tant, és la base de qualsevol operació de manipulació de fitxers.

El sistema de fitxers en UNIX separa els directoris usant “/” mentre que en Windows es separen amb “\”.


__Creació de File__ La classe File no representa un arxiu en si mateix sinó una ruta d'accés a un arxiu o directori.

```java
  //Creem objectes File
    File fitxer=new File("/home/nomUsuari/direccio/fitxer");
    File directori=new File("/home/nomUsuari/direccio");
 
  //Creem fitxers i directoris
    fitxer.createNewFile();
    directori.mkdir();
```


__Comprovacions de Fitxer o Directori__

Els següents mètodes són booleans.

```java
  //Indica si existeixen els arxius
    System.out.println("Fitxer "+fitxer.exists());
    System.out.println("Directori "+directori.exists());
 
  //Indica si son directori
    System.out.println("És directori? "+fitxer.isDirectory());
    System.out.println("És directori? "+directori.isDirectory());

  //Indica si son fitxers
    System.out.println("És fitxer? "+fitxer.isFile());
    System.out.println("És fitxer? "+directori.isFile());
```

__Gestió de rutes__

Tot seguit es crea una direcció relativa i una absoluta i després es comprova i se n'identifica nom i direcció.


```java
  //Creació ruta relativa i absoluta
  File fitxerRutaAbsoluta=new File("/home/nomUsuari/direccio/fitxer");
  File fitxerRutaRelativa=new File("../../../ruta/direccio");
 
  //Indica la ruta absoluta del File
  System.out.println("Ruta absoluta: "+fitxerRutaAbsoluta.getAbsolutePath());
  System.out.println("Ruta absoluta: "+fitxerRutaRelativa.getAbsolutePath());

  //Indica el nom del document/carpeta
  System.out.println("Ruta absoluta: "+fitxerRutaAbsoluta.getName());
  System.out.println("Ruta absoluta: "+fitxerRutaRelativa.getName());

  //Indica la ruta del document/carpeta
  System.out.println("Ruta absoluta: "+fitxerRutaAbsoluta.getParent());
  System.out.println("Ruta absoluta: "+fitxerRutaRelativa.getParent());
```

__Permisos en File__

Tots els mètodes són booleans.

```java
  File fitxer=new File("/home/nomUsuari/direccio/fitxer");
  fitxer.canRead();
  fitxer.canWrite();
  fitxer.canExecute();
```

__Llistar fitxers que hi ha dins una carpeta__

```java

  File directori=new File("/home/nomUsuari/direccio");

  File llista[]=directori.listFiles();
  for(File file: llista){
      System.out.println(file.getName());
  }

  String llista[]=directori.list();
  for(String file: llista){
      System.out.println(file);
  }
```

__Altres mètodes interessants__

```java
  File fitxer=new File("/home/nomUsuari/direccio/fitxer");

  //Mida del fitxer
  fitxer.length

  //Eliminar un file
  fitxer.delete()

  //Renombrar un file
  fitxer.renameTo(fileDesti)
```

**Limitacions**
1. La classe File no proporciona funcionalitats per llegir o escriure directament dins dels arxius. Per a això, s'han d'utilitzar classes com FileReader, FileWriter, BufferedReader, BufferedWriter, etc.
2. La classe File tampoc gestiona permisos més avançats ni cap mena de bloqueig d'arxius. Per a permisos més específics, es poden utilitzar altres APIs com java.nio.file