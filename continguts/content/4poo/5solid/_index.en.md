---
date: 2016-04-09T16:50:16+02:00
title: Principis SOLID
weight: 4
pre: "5. "
---

{{% notice note %}}
Els principis sòlids són una sèrie de directrius de disseny de classes orientades a objectes que busquen millorar la qualitat del programari i facilitar-ne el manteniment i l'extensió. Són un conjunt de regles i millores pràctiques a seguir al dissenyar una estructura de classe. SOLID és un acrònim que representa els cinc principis bàsics. 
{{% /notice %}}

Aquests principis són fonamentals per al disseny de programari orientat a objectes i ajuden a crear sistemes que siguin més robustos, flexibles i fàcils de mantenir.


* S - Single Responsibility Principle (SRP)
* O - Open/Closed Principle (OCP)
* L - Liskov Substitution Principle (LSP)
* I - Interface Segregation Principle (ISP)
* D - Dependency Inversion Principle (DIP)


#### S - Single Responsibility Principle (SRP):
Principi de Responsabilitat Única: Una classe ha de tenir una, i només una, raó per canviar. Això vol dir que cada classe s'ha d'encarregar d'una sola part de la funcionalitat del sistema i totes les seves responsabilitats han d'estar estretament relacionades. En seguir aquest principi, es facilita la comprensió del codi i el manteniment, ja que **cada classe té una responsabilitat clarament definida**.

Imaginem-nos una classe Report que generi contingut de l'informe i que també l'enviï per correu electrònic.

```java
public class Report {
    public void generateReport() {
        // Codi para generar l'informe
    }

    public void sendReport(String emailAddress) {
        // Codi per enviar l'informe
    }
}
```

En aquest cas la classe Report té dues responsabilitats: generar informe i enviar-lo per correu. De forma que no és coherent amb SRP.

Si seguim el principi SRP, refactoritzem i:
```java
public class ReportGenerator {
    public void generateReport() {
        // Codi para generar l'informe
    }
}

public class ReportSender {
    public void sendReport(String emailAddress) {
        // Codi per enviar l'informe
    }
}
```

D'aquesta manera cada classe té la seva pròpia responsabilitat.



#### O - Open/Closed Principle (OCP):
Principi d'Obert/Tancat: Les entitats de programari (com ara classes, mòduls, funcions, etc.) han d'estar **obertes per a la seva extensió, però tancades per a modificar-les**. Això implica que hauríeu de poder afegir noves funcionalitats sense alterar el codi existent. Això se sol aconseguir mitjançant la utilització d'interfícies o classes abstractes, permetent que noves implementacions puguin ser afegides sense canviar el codi que ja funciona.


Imaginem-nos una classe que calcula l'àrea de diferents objectes geomètrics.
```java
public class AreaCalculator {
    public double calculateArea(Shape shape) {
        if (shape instanceof Circle) {
            Circle circle = (Circle) shape;
            return Math.PI * circle.getRadius() * circle.getRadius();
        } else if (shape instanceof Square) {
            Square square = (Square) shape;
            return square.getSide() * square.getSide();
        }
        // Agregar nous tipus de formes aqui
        return 0;
    }
}
```
En aquest exemple, si vull incloure un triangle fa que hagi de **modificar** el codi, de forma que violem el principi OCP. Si refactoritzem seguint OCP:
```java
public interface Shape {
    double calculateArea();
}

public class Circle implements Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    public double getRadius() {
        return radius;
    }

    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

public class Square implements Shape {
    private double side;

    public Square(double side) {
        this.side = side;
    }

    public double getSide() {
        return side;
    }

    @Override
    public double calculateArea() {
        return side * side;
    }
}

public class AreaCalculator {
    public double calculateArea(Shape shape) {
        return shape.calculateArea();
    }
}
```
D'aquesta manera la classe AreaCalculator no necessita modificar-se per admetre noves formes, però en canvi s'ha traslladat la funcionalitat de calcular l'àrea a una interfície que totes les formes geomètriques poden implementar i per tant extendre-ho a noves formes geomètriques.

#### L - Liskov Substitution Principle (LSP):
 Principi de substitució de Liskov: **Els objectes d'una classe derivada han de poder substituir objectes de la classe base sense alterar el funcionament del programa**. En altres paraules, les subclasses han de ser intercanviables amb les superclasses sense causar errors o comportaments inesperats. **Això garanteix que les classes derivades són veritables extensions de les classes base**, mantenint la integritat del comportament del sistema.

 Suposem les classes Bird i Penguin:
```java
 public class Bird {
    public void fly() {
        // Codi per volar
    }
}

public class Penguin extends Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException("Penguins can't fly");
    }
}
```
En aquest cas es trenca LSP ja que si es vol cridar el mètode fly de Penguin es produiria una excepció, no es poden intercanviar. Refactoritzem:
```java
 public abstract class Bird {
    public abstract void move();
}

public class Sparrow extends Bird {
    @Override
    public void move() {
        // Codi per volar
    }
}

public class Penguin extends Bird {
    @Override
    public void move() {
        // Codi para caminar
    }
}
```
En aquest cas, "generalitzant" la funcionalitat a `move()` i implementant-la de forma concreta en cada classe permet tenir un model coherent amb LSP i per tant amb classes substituïbles.

#### I - Interface Segregation Principle (ISP):
Principi de Segregació d'Interfícies: Els clients no s'han de veure obligats a dependre d'interfícies que no utilitzen. **Aquest principi suggereix que és millor tenir diverses interfícies específiques en comptes d'una interfície general**. D'aquesta manera, les classes implementen només les interfícies que necessiten, evitant la dependència de mètodes que no hi són rellevants.

Tenim una interfície Worker que realitza diferents accions:

```java

public interface Worker {
    void work();
    void eat();
}
```

Podria passar que Chief no implementés el mètode `eat()` i per tant violaria la ISP. Refactoritzem:
```java
public interface Workable {
    void work();
}

public interface Eatable {
    void eat();
}

public class Chief implements Workable {
    @Override
    public void work() {
        ...
    }
}

public class Employee implements Workable, Eatable {
    @Override
    public void work() {
        ...
    }

    @Override
    public void eat() {
        ...
    }
}
```
Separant cada funcionalitat en diferents interfícies permet adaptar cadascuna a on li pertany i compleix ISP.


#### D - Dependency Inversion Principle (DIP):
Principi d'inversió de dependències: Les dependències han d'estar en abstraccions, no en concrecions. **En lloc de dependre de classes concretes, les classes han de dependre d'interfícies o classes abstractes**. A més, les abstraccions no han de dependre de detalls; els detalls han de dependre de les abstraccions. Això facilita la modularitat i el desacoblament, fent que el sistema sigui més flexible i fàcil de mantenir.

Suposem una classe UserService que depen directament d'una classe UserRepository
```java
public class UserRepository {
    public void save(User user) {
        // Códi per guardar usuari en BBDDs
    }
}

public class UserService {
    private UserRepository userRepository;

    public UserService() {
        this.userRepository = new UserRepository();
    }

    public void registerUser(User user) {
        userRepository.save(user);
    }
}
```

En aquest cas UserService està fortament acoblat amb UserRepository. UserService depèn de UserRepository la qual cosa no ens permet canviar amb facilitat el codi de UserRepository. Refactoritzem:

```java
public interface UserRepository {
    void save(User user);
}

public class SqlUserRepository implements UserRepository {
    @Override
    public void save(User user) {
        // Códi per guardar usuari en BBDDs
    }
}

public class UserService {
    private UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public void registerUser(User user) {
        userRepository.save(user);
    }
}
```

D'aquesta manera UserService ja no depèn d'una classe concreta sinó d'una interfície. Això permet injectar en UserService diferents implementacions de la interfície UserRepository, permet el canvi d'implementació sense tocar la classe UserRepository.

