---
title: Operacions CRUD i mapeig objecte-relacional
weight: 3
---

Les sigles CRUD fan referència a create, *read, update i delete*, que són les operacions bàsiques que es realitzen en una base de dades.

En el nostre paradigma de la Programació Orientada a Objectes, haurem de dotar a les nostres classes de mètodes que gestionin la seva persistència en base de dades. Això ho farem amb la **tècnica de mapeig objecte-relacional**, que consisteix en mapejar cada classe amb una taula de la base de dades, i cada atribut, amb una columna de la taula corresponent. Convertint cada objecte en un registre de la taula i cada registre, en un objecte Java.

Per tant, cada classe persistent, haurem de dotar-la dels mètodes create(), read(), update() i delete().

Exemple de read:
```java
public Album llegeixAlbum(int idAlbum)
{
   Statement stmt = null;
   Album album = null;
   try {
       String query = "SELECT * FROM Album WHERE AlbumId = ?";
       PreparedStatement ps = con.prepareStatement(query);
       ps.setInt(1,idAlbum);
       ResultSet rs = ps.executeQuery();
       while ( rs.next() ) {
           int albumId = rs.getInt("AlbumId");
           String  title = rs.getString("Title");
           int  artistId = rs.getInt("ArtistId");
           album = new Album(albumId, title, artistId);
       }
       rs.close();
       ps.close();
   } catch ( Exception e ) {
       System.err.println( e.getClass().getName() + ": " + e.getMessage() );
   }
   System.out.println("Operation done successfully");
   return album;
}
```

Exemple de delete:
```java
public void eliminaAlbum(int idAlbum)
{
   try {
       con.setAutoCommit(false);
       String query = "DELETE from Album where AlbumId=?";
       PreparedStatement ps = con.prepareStatement(query);
       ps.setInt(1,idAlbum);
       ps.executeUpdate();
       con.commit();
       ps.close();
   } catch ( Exception e ) {
       System.err.println( e.getClass().getName() + ": " + e.getMessage() );
   }
   System.out.println("Operation done successfully");
}
```