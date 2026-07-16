---
date: 2016-04-09T16:50:16+02:00
title: Records
weight: 5
pre: "5.1. "
---

Els Records en Java son classes que serveixen per representar dades, similars a les classes POJO (Plan Old Java Object) però amb algunes diferències. Els Records disponibles en Java des de la versió 16 (estable).

| Característica | POJO                                                                | Record                                                             |
| -------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------ |
| Mutabilitat    | Pot ser mutable o immutable                                         | Sempre és immutable (els camps son sempre finals)                  |
| Codi           | Cal escriure constructors, getters,equals(), hashCode(), toString() | Java els genera automàticament                                     |
| Herència       | Pot extendre altres classes                                         | No pot extendre classes (implícitamnet exten java.lang.Record)     |
| Ús principal   | Pot ser mutable o immutable                                         | Sempre és immutable (els camps son sempre finals)                  |
| Mutabilitat    | Objectes amb lògica de negoci o estat modificable                   | Objectes que només transporten dades (DTOs, respostes d'API, etc.) |

### Exemple de classe POJO

```java
public class Persona {
    private String nom;
    private int edat;

    public Persona(String nom, int edat) {
        this.nom = nom;
        this.edat = edat;
    }

    public String getNom() {
        return nom;
    }

    public int getEdat() {
        return edat;
    }

    public void setNom(String nom) {
        this.nom = nom;
    }

    public void setEdat(int edat) {
        this.edat = edat;
    }
}

Persona p = new Persona("Maria", 20);
p.setEdat(21);
```

### Exemple de Record

```java
public record Persona(String nombre, int edad) {}

Persona p = new Persona("Maria", 20);

System.out.println(p.nom());
System.out.println(p.edat());

```

Com podeu comprovar de l'exemple anterior, Java genera automàticament els mètodes get amb el mateix nom que els declara, de fet es generen els següents mètodes automàticament:

- Constructor
- Getters (nombre() y edad())
- equals()
- hashCode()
- toString()

Com que és un objecte immutable `no genera mètodes set`, no tindrien sentit en un objecte on no es pot modificar el seu estat.

## Quan usar POJO o Record

Usarem Record quan:

- Només volem emmagatzemar dades en objectes.
- Crees DTOs.
- Representes respostes de APIs REST.
- Menys codi i objectes immutables.

Usarem POJO quan:

- L'objecte canvia l'estat.
- Necessites setters.
- Tens lògica de negoci.
- Cal extendre una altra classe.
- Utilizes frameworks o biblioteques que requereixen classes mutables.

{{% notice note %}}
**Record**: Tipus especial de Java per representar dades de forma concisa i immutable. En aplicacions modernes (per ex. Spring Boot) és comú usar Records per DTO's.<br>
**POJO**: Classe Java tradicional, pot ser mutable i contenir tantes dades com comportament. POJO s'utilitza en classes de lògica de negoci, o per representar entitats en JPA.  
{{% /notice %}}
