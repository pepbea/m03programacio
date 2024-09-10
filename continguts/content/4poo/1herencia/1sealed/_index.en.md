---
date: 2016-04-09T16:50:16+02:00
title: Sealed Classes
weight: 1
pre: "1.1. "
---

En Java, les sealed classes són una característica introduïda a Java 15 i es va convertir en part de l'estàndard a Java 17. Les sealed classes permeten restringir quines altres classes poden heretar d'una classe específica, cosa que ajuda a mantenir un control més estricte sobre la jerarquia de classes i pot ser útil per implementar patrons de disseny com el patró d'estat o el patró d'estratègia de manera més segura i predictible.

**Què és una Sealed Class?**

{{% notice note %}}
Una sealed class és una classe que especifica explícitament quines classes en poden heredar. Això es fa mitjançant l'ús de la paraula clau `sealed` a la declaració de la classe. Les classes que hereden d'una sealed class han de ser final, sealed o non-sealed.
{{% /notice %}}

Com es fa servir?

```java
// Sealed Class
public sealed class Shape permits Circle, Rectangle {
    public abstract double area();
}

// Classe permesa que hereda de Shape
public final class Circle extends Shape {
    private final double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double area() {
        return Math.PI * radius * radius;
    }
}

// Una altra clase permesa que hereda de Shape
public final class Rectangle extends Shape {
    private final double width;
    private final double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double area() {
        return width * height;
    }
}

```

**Explicació del Codi**

1. Declaració de la Sealed Class:
        `public sealed class Shape permits Circle, Rectangle` indica que Shape és una sealed class i que només Circle i Rectangle en poden heredar.

2. Classes Filles (Heredades):
        Circle i Rectangle són les úniques classes que poden estendre Shape. Totes dues estan marcades com a final, cosa que significa que no es poden estendre més.

3. Mètode Abstracte:
        La classe Shape té un mètode abstracte area() que ha de ser implementat per totes les classes que hereden de Shape.



**Propietats de les Sealed Classes**

1. `sealed`: Indica que la classe pot ser estesa només per un conjunt específic de classes.
2. `final`: Indica que la classe no pot ser estesa.
3. `non-sealed`: Permet que una subclasse (d'una classe segellada) sigui estesa per altres classes.

Aquí tens un exemple que utilitza aquestes paraules clau:

```java

public sealed class Vehicle permits Car, Truck {
}

public final class Car extends Vehicle {
}

public sealed class Truck extends Vehicle permits PickupTruck {
}

public final class PickupTruck extends Truck {
}

```

#### Beneficis de les Sealed Classes

* **Seguretat de Tipus**: Pots garantir que només un conjunt limitat de classes pot heredar d'una sealed class, cosa que ajuda a evitar errors i millora la seguretat del tipus.

* **Facilita el Patró de Disseny**: Les sealed class són útils per implementar patrons de disseny com el patró d'estat o el patró d'estratègia de manera més controlada i segura.

* **Millora la Manteniment del Codi**: En conèixer totes les possibles subclasses en temps de compilació, el codi pot ser més fàcil d'entendre i mantenir.

#### Consideracions

- Les sealed classes requereixen que especifiquis totes les subclasses permeses a la seva declaració. Això pot fer que la refactorització sigui més rigorosa.
- Assegureu-vos d'entendre l'impacte en l'herència i com això pot afectar el disseny de la vostra aplicació.
- Les Sealed Classes a Java proporcionen més control sobre la jerarquia de classes i poden ajudar a escriure codi més robust i mantenible.

#### Exemple

```java
public sealed class Color permits RGBColor, CMYKColor, NamedColor {
    public abstract String getColorRepresentation();
}


public final class RGBColor extends Color {
    private final int red;
    private final int green;
    private final int blue;

    public RGBColor(int red, int green, int blue) {
        this.red = red;
        this.green = green;
        this.blue = blue;
    }

    @Override
    public String getColorRepresentation() {
        return String.format("RGB(%d, %d, %d)", red, green, blue);
    }

    public int getRed() {
        return red;
    }

    public int getGreen() {
        return green;
    }

    public int getBlue() {
        return blue;
    }
}


public final class CMYKColor extends Color {
    private final double cyan;
    private final double magenta;
    private final double yellow;
    private final double key; // Key (negro)

    public CMYKColor(double cyan, double magenta, double yellow, double key) {
        this.cyan = cyan;
        this.magenta = magenta;
        this.yellow = yellow;
        this.key = key;
    }

    @Override
    public String getColorRepresentation() {
        return String.format("CMYK(%.2f, %.2f, %.2f, %.2f)", cyan, magenta, yellow, key);
    }

    public double getCyan() {
        return cyan;
    }

    public double getMagenta() {
        return magenta;
    }

    public double getYellow() {
        return yellow;
    }

    public double getKey() {
        return key;
    }
}

public final class NamedColor extends Color {
    
    private final String colorName;

    public NamedColor(String colorName) {
        this.colorName = colorName;
    }

    @Override
    public String getColorRepresentation() {
        return colorName;
    }

    public String getColorName() {
        return colorName;
    }
}

public class Main {
    public static void main(String[] args) {
        Color rgbColor = new RGBColor(255, 0, 0); // Vermell
        Color cmykColor = new CMYKColor(0.0, 1.0, 1.0, 0.0); // Cian, magenta, groc
        Color namedColor = new NamedColor("Sky Blue"); // Blaucel 

        System.out.println("RGB Color: " + rgbColor.getColorRepresentation());
        System.out.println("CMYK Color: " + cmykColor.getColorRepresentation());
        System.out.println("Named Color: " + namedColor.getColorRepresentation());
    }
}
```
