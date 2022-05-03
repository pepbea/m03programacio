---
title: PreparedStatement
weight: 1
---

Si una mateixa consulta s’ha d’executar diverses vegades, és millor usar PreparedStatement com a alternativa a Statement, ja que la instrucció SQL es manté precompilada i això la fa més eficient. A més, **permet l’ús de paràmetres** dins de la instrucció i asignar-los en temps d’execució, cosa que protegeix la consulta de possibles **SQLInjection**.

Els paràmetres de la consulta s’indiquen amb el signe **‘?’**. I l’assignació es fa mitjançant el mètode de PreparedStatement adequat al tipus de dada (setInt, setString, etc) i el número de paràmetre al que assignar el valor dins de la consulta.

```java
public void seleccionaAlbum(int idAlbum)
{
   Statement stmt = null;
   try {
       String query = "SELECT * FROM Album WHERE AlbumId = ?";
       PreparedStatement ps = con.prepareStatement(query);
       ps.setInt(1,idAlbum);

       ResultSet rs = ps.executeQuery();
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
       ps.close();
   } catch ( Exception e ) {
       System.err.println( e.getClass().getName() + ": " + e.getMessage() );
       System.exit(0);
   }
   System.out.println("Operation done successfully");
} 
```