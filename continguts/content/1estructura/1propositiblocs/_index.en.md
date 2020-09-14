---
title: Introducció 
weight: 1
---

#### Breus definicions inicials


{{% notice note %}}
**Programació informàtica**: És el procés d'escriure, provar, depurar/solucionar problemes, i mantenir el codi font de programes.   
{{% /notice %}}


{{% notice note %}}
**Programa**: Conjunt d'instruccions d’un llenguatge de programació, ordenades d'una manera determinada, que l’ordinador és capaç d’entendre i executar per resoldre un problema. L'ordinador és capaç d'entendre unes normes sintàctiques i semàntiques que permeten realitzar multitud de funcions diferents.  
{{% /notice %}}

{{% notice note %}}
**Instrucció**: És una cadena de símbols d'un alfabet, formada d'acord amb certes regles sintàctiques que el processador (o el compilador) entén, i que finalment seran interpretades i executades pel processador.  
{{% /notice %}}

{{% notice note %}}
**Llenguatge informàtic**: Conjunt d'instruccions que ordenades d'una determinada manera generen un codi que l'ordinador és capaç d'entendre per realitzar una determinada tasca.  
{{% /notice %}}

{{% notice note %}}
**Dada**: Unitat d'informació que utilitzen els programes informàtics per ser tractada (llegir, modificar, eliminar, crear, transformar...).
{{% /notice %}}

{{% notice note %}}
**Codi font**: Codi que els humans poden entendre i manipular per tal de crear i modificar els diferents programes informàtics. En Java els fitxers que contenen codi font són fitxers amb extensió .java  
{{% /notice %}}

{{% notice note %}}
**Codi màquina**: Una vegada el codi font és escrit pels humans es transforma en un altre fitxer (compilació) que genera un altre fitxer/codi que està a més baix nivell i que enten la màquina. En Java els fitxers convertits a codi màquina són els fitxers executables, són diferents per cada plataforma, per això diem que java és un llenguatge multiplataforma, perquè el mateix codi font el podem executar en plataformes diferents.
{{% /notice %}}

#### Procés d'execució d'un programa

Els programes informàtics donen solució a una determinada necessitat o problemàtica. A partir d'un problema determinat dissenyem un conjunt de passos determinats, ordenats i finits que ens aporta la solució (algorisme). La implementació d'aquests passos amb un llenguatge de programació genera un codi que dóna lloc al programa informàtic final. 

![1](../images/1.png?width=500px)

Així doncs el programa té un iniciador, executa una sèrie d'instruccions que solucionen un problema determinat i existeix un punt de finalització quan es troba l'estat que soluciona el problema. 

En aquest procés es possible que tinguem dades d'entrada (input: dades necessàries per executar un codi determinat), i també és possible que tinguem dades de sortida (output: dades que desitgem retornar o mostrar quan s'acaba l'execució del codi).

Tot el codi que hem escrit i que posem a executar l'anomenarem procés (codi en execució).

![2](../images/2.png?width=500px)

#### Cas particular de Java

Tot seguit veiem què passa amb el programa HolaMon.java escrit en Java. És el primer programa que s'acostuma a mostrar de qualsevol llenguatge de programació. L'únic que fa aquest programa és escriure per pantalla "Hola Mundo". 

Si us fixeu en la següent il·lustració es mostra tot el procés de compilació. Inicialment tenim el codi font del fitxer HolaMundo.java escrit pel programador. El següent pas és transformar aquest fitxer en un codi intermig que és el bytecode que permetrà ser transportat a qualsevol plataforma. Aquest codi intermig és un fitxer .class que ens assegura que el procés de compilació del fitxer .java s'ha executat correctament, en java s'utilitza la comanda javac per poder obtenir-lo.
`javac HolaMundo.java` Amb aquesta instrucció "es compila" el programa i genera un HolaMundo.class.

Un cop tenim el fitxer .class, executant la comanda `java HolaMundo` obtenim l'execucio del nostre programa sobre la plataforma on estiguem, per això en la imatge següent el codi màquina que s'executa amb Win32 serà diferent que el que interpreta MacOS ja que són SO's diferents i obeeixen a instruccions diferents.

![45](../images/4.gif?width=500px)

En el següent exemple es pot veure com seria un fitxer .java que es llegeix i s'enten amb llenguatge humà. A continuació, en el procés de compilació, es genera el fitxer .class, aquí ja els humans no entenem el contingut del fitxer ja que està en hexadecimal, i finalment quan executem el programa es genera un fitxer en codi màquina amb una tira de 0s i 1s que són les instruccions que necessita la CPU en cada plataforma per ser executat. Aquest últim fitxer serà diferent en cada plataforma d'execució (Linux, Windows, MacOS...)

![5](../images/5.png?width=500px)



