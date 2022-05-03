---
title: Introducció a la Persistència en BBDDs
weight: 12
pre: "<b>12. </b>"
---

Java ofereix la interfície de programació JDBC (Java DataBase Connectivity) per a l’accés a bases de dades.  L’**API JDBC** conté una gran quantitat de interfícies que permeten **desenvolupar aplicacions que interactuen amb bases de dades, facilitant-ne la connexió i la consulta**.

Amb JDBC escrivim aplicacions usant les seves interfícies i els seus mètodes definits, de manera independent a com són realment implementats per les classes reals que les implementen. Els fabricants de les diferents bases de dades són els encarregats de proporcionar aquestes classes que implementen la interfície JDBC.

Aquests conjunt de classes que implementen JDBC són els **controladors o drivers** proporcionats pels fabricants per a poder interactuar amb la seva base de dades des de Java.



#### Passos de connexió i consulta amb JDBC

Passos habituals en una aplicació que usa JDBC per a l'accés a una base de dades:
 1. Creació d’una instància del controlador o driver JDBC, usant el nom de la classe Java del driver

```java
private static Connection con;
public static Connection getConnection() {
   if (con == null ) {
       try {
           //Creació d’una instància del controlador JDBC
           //(es creen els objectes en carregar-se la classe)
           Class.forName("org.sqlite.JDBC");
```

2. Crear una connexió a la base de dades amb un objecte Connection, a partir de la URL de connexió a la base de dades. La sintaxis de la URL és
`jdbc:subprotocol:paràmetres`

```java
//Crear una connexió a la base de dades amb un objecte Connection
           con = DriverManager.getConnection("jdbc:sqlite:Chinook_Sqlite.sqlite");
       } catch (ClassNotFoundException | SQLException e) {
           System.err.println(e.getClass().getName() + ": " + e.getMessage());
           System.exit(0);
       }
       System.out.println("Opened database successfully");
   }
   return con;
}
```

3. Crear una consulta / query amb un objecte Statement

```java
public void seleccionaAlbums()
{
   Statement stmt = null;
   try {
       //Crear una consulta / query amb un object Statement
       stmt = con.createStatement();
```

4. Executar la consulta

```java
//Executar la consulta
  ResultSet rs = stmt.executeQuery( "SELECT * FROM Album;" ); 

```

Si la consulta ha de retornar resultats, com un **select**, usem **executeQuery**, que retorna un ResultSet amb les dades resultants de la consulta.
Si la consulta no ha de retornar resultats, com un **insert, update o delete**, usem **executeUpdate**, que retorna el número de registres afectats.

5. Procesar el resultat amb l’objecte ResultSet

```java
//Procesar el resultat amb l’objecte ResultSet
    while ( rs.next() ) {
        int albumId = rs.getInt("AlbumId");
        String  title = rs.getString("Title");
        int  artistId = rs.getInt("ArtistId");
        System.out.println( "albumId : " + albumId );
        System.out.println( "title : " + title );
        System.out.println( "artistId : " + artistId );
        System.out.println();
    }
    rs.close();
    stmt.close();
  } catch ( Exception e ) {
      System.err.println( e.getClass().getName() + ": " + e.getMessage() );
      System.exit(0);
  }
System.out.println("Operation done successfully");
}
```