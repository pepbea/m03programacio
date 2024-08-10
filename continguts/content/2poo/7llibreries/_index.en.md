---
title: Llibreries
weight: 7
pre: "7. "
chapter: false
---

##### Definició

En el context de la programació una llibreria es un conjunt de codi re-utilitzable, encapsulat (paquets, classes, moduls, dll, ...) i documentat adequadament.
* En el cas de Java tenim llibreries de classes i les seves propietats.
* Per exemple podriem considerar la classe Math, que ens proporciona un conjunt de funcions matematiques, una llibreria en si mateixa. Ex:

```java
int x = -15;
int y = Math.abs(x);
```

* Tambe tenim paquets com java.util que agrupen de forma organitzada un conjunt de classes amb unes funcionalitats comunes (utilitats). Veieu més exemples de les llibreries del SDK.

```java
import java.util.Scanner;
```

![array](../images/llibreriesJava.png?width=500px)

#### Llibreries de classes: paquets
* Una llibreria de classes, o package (paquet) en Java, es un conjunt de classes vinculades entre elles d’acord a algun criteri tematic o d’organitzacio del seu codi.
* Els paquets s'organitzen de forma jeràrquica, de manera que podem crear sub-paquets dins d'altres paquets: paquet1.paquet2.paquetn
* Els noms dels packages s’escriuen tots en minúscula i separant paquets i sub-paquets per un punt. (Naming Conventions)
* Totes les classes de Java pertanyen a algun package. En cas de no incloure cap sentència package, es considera que aquella classe pertany a un package especial anomenat per defecte (default package).
* Donada una classe, aquesta únicament pot pertanyer a un paquet.
* Donat un paquet, a dins seu mai hi poden haver dues classes amb el mateix nom.


##### Inclusio de classes dins d'un paquet
* Per incloure una classe dins d'un paquet nomes cal incloure la següent sentencia al inici del fitxer de codi font, abans de qualsevol altra instrucció:
``package nomdelpaquet``
##### Ús de classes d'altres paquets
*  Per usar classes definides en altres paquets cal usar la sentencia import:

```java
import nomdelpaquet.Classe;
import nomdelpaquet.*;
package dam.uf2;
import java.util.*;

public class ComptaChar
{
...
```

#### Estructura dels fitxers dins dels paquets
* Els arxius ``.class`` pertanyents a paquets i subpaquets han d'estar organitzats de manera adequada perquè tant el compilador com la màquina virtual de Java puguin utilitzar-los.
* Cada paquet es situa en un directori. Cada sub-paquet s'ubica en un directori de nivell inferior, i així successivament.
* El nom de cada directori ha de ser el del propi paquet.

![array](../images/llibreries.png?width=500px)

#### Paquets bàsics del JDK (Java Development Kit)

* **java.lang**: es el paquet principal i el compilador l’incorpora de manera automatica (no cal importar-lo). Conté les
classes bàsiques de Java, incloent-hi el tractament de cadenes de caràcters, el maneig de nombres i funcions
matemàtiques, l’accés als recursos del sistema, i la programació multiarea.
* **java.io**: controla les operacions d’entrada i sortida i els arxius.
* **java.util**: conte classes i metodes de propòsits molt diversos, com ara generació de nombres aleatoris (Random),
tractament d'arrays (Arrays), propietats del sistema, etc.
* **java.net**: dona suport a les comunicacions TCP/IP. Inclou les classes que fan referència a la comunicació en xarxa.
* **java.applet**: conté només la classe applet que permet el desenvolupament d’aplicacions incrustades en pàgines
HTML.
* **java.awt**: conté les classes i els mètodes de l’Abstract Windows Toolkit, independents del sistema, per al maneig
de la interfície d’usuari.
* **java.awt.image**: conté classes i mètodes independents del sistema, necessaris pel maneig de gràfics i imatges.
* **java.awt.peer**: com que les classes i els mètodes són específics de cada sistema, java.awt.peer conté les classes
necessàries per connectar els components definits en el paquet java.awt amb els components correctes de cada sistema. 

#### Exemple

Si tenim un projecte amb el següent arbre de fitxers:

![array](../images/projecte.png?width=250px)

L'estructura que necessitem en cada fitxer per poder veure la resta de fitxers és la següent:

1. En el ``Main.java`` principal necessitem importar els dos fitxers que no tenim al mateix directori:

```java
import classes.classes2.Funcions2;
import classes.Funcions;
```

2. Per emprar Funcions3 desde Main no ens cal indicar-hi res ja que es troba al mateix directori i per tant ja és visible per Main.

3. Funcions es troba dins el package classes, per això en el Main cal importar-lo i en Funcions.java cal indicar-li a quin package pertany:
```java
package classes;
```

4. De la mateixa manera Funcions2 es troba dins el package classes.classes2, per això en el Main cal importar-lo i en Funcions3.java cal indicar-li a quin package pertany:
```java
package classes.classes2;
```

<br>
Aquí teniu l'enllaç al projecte:

[Projecte imports/package](../images/Llibreries.zip)
