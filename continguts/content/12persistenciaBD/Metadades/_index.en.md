---
title: Metadades
weight: 2
---

Donat un objecte Connection, podem obtenir un objecte DatabaseMetaData, que conté informació relativa al base de dades en la que ens hem connectat.

```java
public static void main(String[] args) {
   DatabaseMetaData dbmd = null;
   try {
       Class.forName("org.sqlite.JDBC");
       Connection connection = DriverManager.getConnection("jdbc:sqlite:Chinook_Sqlite.sqlite");

       dbmd = connection.getMetaData();
       mostraInfoBD(dbmd);
       mostraTaules(dbmd);
       mostraColumnes(dbmd, "Album");
   } catch (SQLException e) {
       System.err.println(e.getMessage());
   } catch (ClassNotFoundException e) {
       throw new RuntimeException(e);
   }
}
```


```java
public static void mostraInfoBD(DatabaseMetaData dbmd) throws SQLException {
   String nom = dbmd.getDatabaseProductName();
   String driver = dbmd.getDriverName();
   String url = dbmd.getURL();
   String usuari = dbmd.getUserName();

   System.out.println("Informació de la BD:");
   System.out.println("Nom: "+nom);
   System.out.println("Driver: "+driver);
   System.out.println("URL: "+url);
   System.out.println("Usuari: "+usuari);
}
```

```java
public static void mostraTaules(DatabaseMetaData dbmd) throws SQLException {
   String[] types = {"TABLE"};
   try (ResultSet rs = dbmd.getTables(dbmd.getCatalogTerm(), dbmd.getSchemaTerm(), null, types);) {

       while (rs.next()) {
           String cataleg = rs.getString(1);
           String esquema = rs.getString(2);
           String taula = rs.getString(3);
           String tipus = rs.getString(4);
           System.out.println(tipus + " - Cataleg: " + cataleg +
                   ", Esquema: "+esquema+", Nom: "+taula);
       }
   }
}
```

```java
public static void mostraColumnes(DatabaseMetaData dbmd, String taula) throws SQLException {
   System.out.println("Columnes de la taula: "+taula);
   try (ResultSet columnes = dbmd.getColumns(null, null, taula, null);) {
       while (columnes.next()) {
           String nom = columnes.getString("COLUMN_NAME"); // 4
           String tipus = columnes.getString("TYPE_NAME"); // 6
           String mida = columnes.getString("COLUMN_SIZE"); // 7
           String nula = columnes.getString("IS_NULLABLE"); // 18
           System.out.println("Columna: "+nom+", Tipus: "+tipus+
                   ", Mida: "+mida+", Pot ser nul·la? "+nula);
       }
   }
} 
```