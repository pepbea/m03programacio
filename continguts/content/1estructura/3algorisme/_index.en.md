---
title: Algorisme
weight: 3
pre: "3. "
chapter: false
---


#### Què és un algorisme?

{{% notice note %}}
Un algorisme és un mètode per **resoldre un PROBLEMA**, són un conjunt d'operacions finites i ordenades que s'han de seguir per a la resolució d'un problema.
{{% /notice %}}


**Característiques dels algorismes**

Les característiques bàsiques d'un algorisme són:

+ **Ordenat.** Cada instrucció té una posició dins el conjunt.
+ **Precís.** Cada instrucció és unívoca i obeeix a un objectiu.
+ **Definit.** Si es segueix un algorisme dues vegades, s'ha d'obtenir **el mateix** resultat cada vegada.
+ **Finit.** L'algorisme ha d'acabar en algun moment, per tant, tindrà un nombre finit de passos.
+ Un bon disseny algorítmic contindrà tres parts: _Entrada (Input), Procés (Tractament de la informació) i Sortida (Output)_.

![Algorisme](../images/algorisme.jpg?width=700px)

**Pseudocodi**
{{% notice note %}}
El **pseudocodi** és un llenguatge informal d’alt nivell que usa les convencions i l’estructura d’un llenguatge de programació, però que està orientat a ser entès pels humans.
{{% /notice %}}

_Exemple_

``` 
//El problema consisteix en: Llegir el radi d'un cercle i calcular i imprimir per pantalla l'àrea i el perímetre.
//Inputs: Radi del cercle (Variable radi).
//Outputs: Àrea del cercle (Variable area) i Perímetre del cercle (Variable perimetre) 
//Variables: radi, area i perimetre de tipus Real.    

IniciProces Cercle
    Definir radi, area i perimetre com a tipus Reals;
    Escriure "Introdueix el radi de la circumferència";
    Llegir radi;
    area <- PI * radi ^ 2;
    perimetre <- 2 * PI * radi;
    Escriure "L'àrea és ", area;
    Escriure "El perímetre és ", perimetre;
FiProces
``` 


**Diagrama de flux**
{{% notice note %}}
Un **diagrama de flux** de control consisteix en una subdivisió de passes seqüencials, d’acord amb les sentències i estructures de control d’un programa, que mostra els diferents camins que pot seguir un programa a l’hora d’executar les seves instruccions. Cada passa s’associa a una figura geomètrica específica.
{{% /notice %}}

Una eina per dibuixar diagrames de flux és [Code2Flow](https://app.code2flow.com/), a partir d'un pseudocodi és capaç de dibuixar automàticament el diagrama de flux pertinent.

Si agafem el cas anterior i 'l'adaptem' a les regles que ens demanen aconseguim el següent resultat:
![Code2Flow](../images/code2flow.png?width=1100px)



**Complexitat ciclomàtica**
{{% notice note %}}
La **Complexitat ciclomàtica** (en anglès, Cyclomatic Complexity) és una mètrica de programari en enginyeria de programari que proporciona una mesura quantitativa de la complexitat lògica d'un programa. Consisteix en __comptar el nombre de camins necessaris per tal d'anar de la primera a la última instrucció passant per tots els camins possibles i cobrint tots els casos__.
{{% /notice %}}
