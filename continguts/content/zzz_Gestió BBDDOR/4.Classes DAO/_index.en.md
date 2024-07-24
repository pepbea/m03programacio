---
title: Classes DAO
weight: 4
---

Les operacions relacionades amb la persistència dels objectes en bases de dades, en realitat, no formen part de la responsabilitat de l’entitat que representa la classe. Per exemple, la classe Album dels exemples ha d’ocupar-se de les operacions relacionades amb la lògica del negoci que estem modelant però els mètodes CRUD quedarien fora de la seva responsabilitat.

Si volem que una classe es guardi en una base de dades, hem de crear una segona classe amb nom NomClasseDAO que implementi les operacions CRUD d’accés a base de dades. Idealment, a més, aquest DAO serà una interfície i implementarem una classe concreta per a cada tecnologia de base de dades que necessitem.

Classe de negoci / model del domini:

```java
public class Album {
   private int idAlbum;
   private String nom;
   private int idArtista;

   public Album(int idAlbum, String nom, int idArtista) {
       this.idAlbum = idAlbum;
       this.nom = nom;
       this.idArtista = idArtista;
   }

   public Album() {
   }

   //… (getters + setters + toString)

 }
```

Interfície AlbumDAO:

```java
public interface AlbumDao {

   public int create(Album album) throws SQLException;
   public void delete(int idAlbum) throws SQLException;
   //public void delete(Album album) throws SQLException;
   public Album read(int idAlbum) throws SQLException;
   public void update(Album album) throws SQLException;
   public List<Album> getAlbums() throws SQLException;
}
```

Classe que implementa AlbumDAO per a a base de dades SQLLite:

```java
public class AlbumDaoImplementacio implements AlbumDao{

   private static Connection con = Connexio.getConnection();

   @Override
   public int create(Album album) throws SQLException
   {
       String query = "insert into Album(Title, ArtistId) VALUES (?, ?)";
       PreparedStatement ps = con.prepareStatement(query);
       ps.setString(1, album.getNom());
       ps.setInt(2, album.getIdArtista());
       int n = ps.executeUpdate();
       return n;
   }

   @Override
   public void delete(int id) throws SQLException
   {
       String query = "delete from Album where AlbumId =?";
       PreparedStatement ps
               = con.prepareStatement(query);
       ps.setInt(1, id);
       ps.executeUpdate();
   }

   @Override
   public Album read(int id)
           throws SQLException
   {

       String query = "select * from Album where AlbumId= ?";
       PreparedStatement ps = con.prepareStatement(query);

       ps.setInt(1, id);
       Album album = new Album();
       ResultSet rs = ps.executeQuery();
       boolean check = false;

       while (rs.next()) {
           check = true;
           album.setIdAlbum(rs.getInt("AlbumId"));
           album.setNom(rs.getString("Title"));
           album.setIdArtista(rs.getInt("ArtistId"));
       }

       if (check == true) {
           return album;
       }
       else
           return null;
   }

   @Override
   public void update(Album album) throws SQLException
   {
       String query= "update Album set Title=?, ArtistId= ? where AlbumId = ?";
       PreparedStatement ps = con.prepareStatement(query);
       ps.setString(1, album.getNom());
       ps.setInt(2, album.getIdArtista());
       ps.setInt(3, album.getIdAlbum());
       ps.executeUpdate();
   }

   @Override
   public List<Album> getAlbums() throws SQLException
   {
       String query = "select * from Album";
       PreparedStatement ps = con.prepareStatement(query);
       ResultSet rs = ps.executeQuery();
       List<Album> ls = new ArrayList();

       while (rs.next()) {
           Album album = new Album();
           album.setIdAlbum(rs.getInt("AlbumId"));
           album.setNom(rs.getString("Title"));
           album.setIdArtista(rs.getInt("ArtistId"));
           ls.add(album);
       }
       return ls;
   }
}
```