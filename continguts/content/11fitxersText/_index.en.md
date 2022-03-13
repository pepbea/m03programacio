---
title: Gestió de fitxers
weight: 11
pre: "<b>11. </b>"
---


#### File

La classe File és útil per portar la gestió sobre fitxers i carpetes en Java, la seva especificació en Java Oracle és: [https://docs.oracle.com/javase/8/docs/api/java/io/File.html](https://docs.oracle.com/javase/8/docs/api/java/io/File.html) 

El sistema de fitxers en UNIX separa els directoris usant “/” mentre que en Windows es separen amb “\”.


__Creació de File__

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
