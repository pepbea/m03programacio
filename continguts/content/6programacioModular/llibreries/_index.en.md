---
title: Llibreries
weight: 3
---

##### Definició

En el context de la programacio una llibreria es un conjunt de codi re-utilitzable, encapsulat d'alguna manera
(paquets, classes, moduls, dll, ...) i documentat adequadament.
* En el cas de Java tenim llibreries de classes i les seves propietats.
* Per exemple podriem considerar la classe Math, que ens proporciona un conjunt de funcions matematiques, una
llibreria en si mateixa. Ex:

```java
int x = -15;
int y = Math.abs(x);
```

* Tambe tenim paquets com java.util que agrupen de forma organitzada un conjunt de classes amb unes
funcionalitats comunes (utilitats). Veieu mes exemples de les llibreries del SDK a la última pagina del document.
import java.util.Scanner;

```java
import java.util.Scanner;
```

![array](../images/llibreriesJava.png?width=500px)

#### Llibreries de classes: paquets
* Una llibreria de classes, o package (paquet) en Java, es un conjunt de classes vinculades entre elles d’acord a
algun criteri tematic o d’organitzacio del seu codi.
* Els paquets s'organitzen de forma jerarquica, de manera que podem crear sub-paquets dins d'altres paquets:
paquet1.paquet2.paquetn
* Els noms dels packages s’escriuen tots en minúscula i separant paquets i sub-paquets per un punt.
* Totes les classes de Java pertanyen a algun package. En cas de no incloure cap sentencia package, es considera que
aquella classe pertany a un package especial anomenat per defecte (default package).
* Donada una classe, aquesta únicament pot pertanyer a un paquet.
* Donat un paquet, a dintre seu mai hi poden haver dues classes amb el mateix nom.


#### Inclusio de classes dins d'un paquet
* Per incloure una classe dins d'un paquet nomes cal incloure la següent sentencia al inici del fitxer de codi font,
abans de qualsevol altra instruccio:
``package nomdelpaquet``
Ús de classes d'altres paquets
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
* Els arxius ``.class`` pertanyents a paquets i subpaquets han d'estar organitzats de manera adequada perque tant el
compilador com la maquina virtual de Java puguin utilitzar-los.
* Cada paquet es situa en un directori. Cada sub-paquet s'ubica en un directori de nivell inferior, i així
successivament.
* El nom de cada directori ha de ser el del propi paquet.

![array](../images/llibreries.png?width=500px)

#### Paquets bàsics del JDK (Java Development Kit)

* **java.lang**: es el paquet principal i el compilador l’incorpora de manera automatica (no cal importar-lo). Conte les
classes basiques de Java, incloent-hi el tractament de cadenes de caracters, el maneig de nombres i funcions
matematiques, l’acces als recursos del sistema, i la programacio multiarea.
* **java.io**: controla les operacions d’entrada i sortida i els arxius.
* **java.util**: conte classes i metodes de proposits molt diversos, com ara generacio de nombres aleatoris (Random),
tractament d'arrays (Arrays), propietats del sistema, etc.
* **java.net**: dona suport a les comunicacions TCP/IP. Inclou les classes que fan referencia a la comunicacio en xarxa.
* **java.applet**: conte nomes la classe applet que permet el desenvolupament d’aplicacions incrustades en pagines
HTML.
* **java.awt**: conte les classes i els metodes de l’Abstract Windows Toolkit, independents del sistema, per al maneig
de la interfície d’usuari.
* **java.awt.image**: conte classes i metodes independents del sistema, neces- saris per al maneig de grafics i imatges.
* **java.awt.peer**: com que les classes i els metodes son específics de cada sistema, java.awt.peer conte les classes
necessaries per connectar els components defi- nits en el paquet java.awt amb els components correctes de cada
sistema. 

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

[projecte](../images/Llibreries.zip)
