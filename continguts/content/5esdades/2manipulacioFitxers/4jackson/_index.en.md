---
title: Fitxers JSON
weight: 4
pre: "2.4. "
---

Per finalitzar parlarem d'una estructura de fitxers molt comú en el mercat i que és important que sapiguem com manipular per lectura i escriptura, es tracta de fitxers JSON (Javascript Object Notation). Per tal de treballar amb aquesta estructura de fitxers utilitzarem la llibreria `Jackson` i implementarme un CRUD complert que ens permetrà veure'n les seves funcionalitats.

#### Què és Jackson?

Jackson és una llibreria que permet convertir Objectes Java a JSON i viceversa. Això s'anomena:

- _Serialització_ = Objecte Java → JSON
- _Desserialització_ = JSON → Objecte Java

És la llibreria més utilitzada en Java per treballar amb JSON i plenament integrada dins del framework de Java Spring.

#### Com s'afegeix la llibreria Jackson

Cal que en el fitxer `pom.xml` del vostre projecte, afegiu després de l'etiqueta `<properties>`, la següent dependència:

```
<dependencies>
	<dependency>
		<groupId>com.fasterxml.jackson.core</groupId>
		<artifactId>jackson-databind</artifactId>
		<version>2.20.0</version>
	</dependency>
</dependencies>
```

#### L'entitat

L'entitat amb la que treballarem serà la ja coneguda classe Alumne.java. Fixeu-vos que crearem una constructora buida, Jackson necessita aquesta constructora ja que mitjançant els diferents setters anirà modificant la informació en els atributs corresponents.

```java
public class Alumne {

    private int id;
    private String nom;
    private int edat;

    public Alumne() {
    }

    public Alumne(int id, String nom, int edat) {
        this.id = id;
        this.nom = nom;
        this.edat = edat;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getNom() {
        return nom;
    }

    public void setNom(String nom) {
        this.nom = nom;
    }

    public int getEdat() {
        return edat;
    }

    public void setEdat(int edat) {
        this.edat = edat;
    }

	@Override
    public String toString() {
        return "Alumne{" +
                "id=" + id +
                ", nom='" + nom + '\'' +
                ", edat=" + edat +
                '}';
    }
}
```

#### La clau: ObjectMapper

Aquesta classe de Jackson ens permetrà actuar davant una entitat. Amb ella podem **llegir i escriure JSON i convertir a objectes** :

```java
mapper.readValue(fitxer, new TypeReference<List<Alumne>>() {};  //List<Alumne>
mapper.writeValue(fitxer, alumnes);
```

#### AlumneDAO

```java
import com.fasterxml.jackson.core.type.TypeReference;
import com.fasterxml.jackson.databind.ObjectMapper;
import java.io.File;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;

public class AlumneDAO {
    private ObjectMapper mapper = new ObjectMapper();
    private File fitxer = new File("data.json");


    //CREATE
    public void create(Alumne alumne) throws IOException {
        List<Alumne> alumnes = findAll();
        alumnes.add(alumne);
        save(alumnes);
    }

    //READ ALL
    public List<Alumne> findAll() throws IOException {
        if (!fitxer.exists()) {
            return new ArrayList<>();
        }
        return mapper.readValue(fitxer, new TypeReference<List<Alumne>>() {}
        );
    }

	//READ BY ID
    public Alumne findById(int id) throws IOException {
        for (Alumne a : findAll()) {
            if (a.getId() == id)
                return a;
        }
        return null;
    }

    //UPDATE
    public void update(Alumne alumne) throws IOException {
        List<Alumne> alumnes = findAll();
        for (int i = 0; i < alumnes.size(); i++) {
            if (alumnes.get(i).getId() == alumne.getId()) {
                alumnes.set(i, alumne);
            }
        }
        save(alumnes);
    }

    //DELETE
    public void delete(int id) throws IOException {
        List<Alumne> alumnes = findAll();
        alumnes.removeIf(a -> a.getId() == id);
        save(alumnes);
    }

    //SAVE
    private void save(List<Alumne> alumnes) throws IOException {
        mapper.writeValue(fitxer, alumnes);
    }
}

```

#### Main

Amb el següent aplicatiu, observareu com es creen dos objectes Alumne, es guarden en el fitxer data.json, i tot seguit s'actualitza el que té id=2 i s'elimina el que té id=1. S'observen totes les funcionalitats del CRUD que podeu aplicar a qualsevol exemple.

La dificultat rau en dissenyar bé les entitats que necessiteu pels vostres projectes.

```java
public class Main {

    public static void main(String[] args) throws IOException {

        AlumneDAO dao = new AlumneDAO();

        dao.create(new Alumne(1,"Anna",20));
        dao.create(new Alumne(2,"Joan",22));

        System.out.println(dao.findAll());

        dao.update(new Alumne(2,"Joan Garcia",23));

        dao.delete(1);

    }
}
```

#### Resum i a tenir en compte

{{% notice note %}}
**Objecte buit**: Sense l'objecte buit, Jackson no sabrà com crear els objectes. Error: "Cannot construct instance"<br>
**Setters**: Cal posar en les entitats els setters necessaris per manipular la informació, sense els setters no apareixeran els atributs en JSON.<br>
**Mala Formatació del JSON**: vigilar amb la mala formatació del JSON ja que sinó Jackson no podrà llegir el document correctament.<br>
**FileNotFoundException**: Assegureu-vos que el fitxer existeix.
{{% /notice %}}

**Idea clau**: Jackson no modifica directament un registre dins del fitxer JSON. En una aplicació senzilla basada en fitxers, el patró habitual és llegir tota la col·lecció, modificar-la en memòria i tornar-la a escriure completa.

| Operació | Passos                       |
| -------- | ---------------------------- |
| Create   | Llegir → Afegir → Guardar    |
| Read     | Llegir el fitxer JSON        |
| Update   | Llegir → Modificar → Guardar |
| Delete   | Llegir → Eliminar → Guardar  |
