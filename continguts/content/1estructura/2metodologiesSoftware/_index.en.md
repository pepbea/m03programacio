---
title: Metodologies de Software
weight: 2
---


El **programari** no es fabrica com qualsevol altre producte clàssic, sinó que es desenvolupa seguint una sèrie d'etapes. D'aquí sorgeix el concepte d'enginyeria de programari, que consisteix en l'aplicació de l'enginyeria per obtenir desenvolupaments
que optimitzin l'efectivitat i els costos.

Els processos d'enginyeria de programari comprenen per tant, diverses etapes, que constitueixen el que s'anomena el **cicle de vida** del programari. Per dur a terme aquestes fases és necessari partir d'un enfocament amb el qual iniciar el procés de
enginyeria. Un cop iniciat, s'ha d'utilitzar una metodologia amb unes eines que permetin completar les diferents etapes de l'cicle.

En l'actualitat, l'enfocament més estandaritzat és **l'orientació a objectes**. la creació el 1998 de l'estàndard UML (Unified Modeling Language) per a la definició de problemes i el desenvolupament de llenguatges de programació com Java o C ++ pel desenvolupament i integració de solucions, són els principals causants que aquest enfocament s'estigui consolidant.

#### Què és l'enginyeria del software?

{{% notice note %}}
De l'aplicació de l'enginyeria a l'programari sorgeixen els processos de desenvolupament de programari. Aquest procés es defineix com __"aquell en què les necessitats de l'usuari són traduïdes en requisits de programari, aquests requisits transformats en disseny, i el disseny implementat en codi, que és provat, documentat i
certificat pel seu ús operatiu"__ [Jacobson, 1998].
{{% /notice %}}

#### aracterístiques del software
+ S'ha invertit la demanda i el preu respecte al HW.
+ El Software es un producte lògic que es desenvolupa, no es construeix com la resta de productes.
+ La gestió de costos es centra en l'enginyeria, amb la qual difereix d'altres projectes d'enginyeria.
+ El Software no es deteriora amb el temps, però sí és necessari un manteniment.
+ La reutilització de productes software creixent.
+ Existeixen restriccions de recursos en el desenvolupament de software, de forma que és necessari assegurar-ne la qualitat per obtenir un software: documentat, fiable, eficient i amb una bona interfície gràfica.

#### Cicles de desenvolupament del software. Tipus de cicles

Anomenem cicle de vida del software al temps necessari per la producció d'un projecte software desde la recopilació de requisits fins a l'entrega final del producte. El cicle de vida inclou una sèrie d'etapes que pot canviar en funció del model, la metodologia i l'autor. Existeixen varis tipus de cicles de vida que passem a
comentar.

#### Model en cascada o lineal

Es tracta d'un model molt genèric i que estableix una sèrie de fases o etapes, que han de ser seguides en un ordre seqüencial, ja que cada fase genera entrades i documentació per a la següent fase. Les fases d'un cicle de vida en cascada segueixen el següent esquema:

![Waterfall](../images/waterfall.png?width=500px)

Les **característiques** del model són:
+ Cada etapa s'inicia un cop acabada l'anterior.
+ Ajuda a la planificació temporal i el càlcul de costos, a causa de la seqüencialitat i estructura lògica de les etapes.
+ Hi ha una realimentació en el manteniment.

Quant als **inconvenients** que s'han detectat, aquests són:
+ Es tracta d'un model rígid, sense robustesa ni adaptabilitat als problemes a resoldre.
+ Hi ha dificultats a l'hora d'establir els requisits inicials, ja que aquests solen venir donats per persones alienes al coneixement del cicle de desenvolupament de programari.
+ Els errors solen detectar-se molt tard, el que implica que el cost per solucionar l'error sigui molt més gran.
+ El manteniment es realitza mitjançant petites actualitzacions o "pegats". Torna a aplicar cadascuna de les fases del cicle al programari ja existent, sense crear un de nou.

**Fases:**
+ **Anàlisi de sistema:** el sistema de programari forma part sobre un sistema major amb el qual es relaciona. S'analitza el sistema en el seu conjunt per treure objectius que han de ser abordables pel programari.
+ **Anàlisi de requisits:** definint funcions a realitzar, dades, comportament, i interacció entre elements funcionals.
+ **Disseny:** a partir de requisits dissenyem els components de programari, estructures de dades, mòduls, procediments, algoritmes i interfícies...
+ **Codificació:** a partir d'informació generada implementem sistema, codifiquem procediments en un llenguatge de programació.
+ **Prova:** validem i verifiquem que els requisits establerts pel client es realitzen correctament.
+ **Manteniment:** la producció de programari no finalitza amb el lliurament, ha de ser revisat i reajustat quan això sigui necessari.

#### Cicle de vida prototipat

Aquest model tracta de solucionar problemes del model en cascada, en concret les dificultats a l'hora d'establir els requisits inicials. El client sol definir els objectius generals del programari, però no acostuma a tenir en compte tots els requisits reals que ha de tenir una aplicació. Al mateix temps, el desenvolupador pot no arribar a entendre què vol el client. Per tal de solucionar això, un cicle basat en prototips pot ser un millor enfocament.

Les **característiques** d'aquest model són:
+ Client i desenvolupador defineixen una sèrie d'objectius globals, dels quals s'identifiquen els requisits, amb els quals es realitza un disseny ràpid, i amb aquest, la creació d'un prototip.
+ El prototip és avaluat per l'usuari, qui pot veure les deficiències del prototip, a partir de les quals es redefineixen els requisits.
+ Es van construint nous prototips, amb els quals el client pot anar polint els requisits de programari, al mateix temps que el desenvolupador pot comprendre millor el que ha de fer. Aquestes interaccions finalitzen quan el prototip satisfà les necessitats del client.

**Inconvenients** d'aquest tipus de cicle de vida:
+ És un procés molt lent. Si es desitja generar un programari de qualitat no n'hi ha prou que un prototip sigui com l'anterior amb uns petits ajustos, sinó que es requereix crear el producte de nou. això succeeix fonamentalment amb els primers prototips de cada desenvolupament.
+ El client veu cada prototip com una versió de programari final, sense prendre consciència que cada prototip únicament ajuda a aclarir els requisits, i per tant, és generat des del principi, per aconseguir una robustesa en el desenvolupament.
+ Els primers prototips que es rebutgen suposen un cost addicional, ja que amb prou feines poden emprar-se per al mateix desenvolupament ni poden ser reutilitzats per a altres.

#### Cicles de vida evolutius

El programari és un producte que va evolucionant per això els desenvolupadors necessiten un nou model de cicle de vida, que permeti que les funcionalitats del programari puguin anar canviant amb el temps. El model en cascada assumeix que es lliura un producte una vegada acabades totes les fases del procés, sense considerar possibles evolucions. Tampoc es té en compte l'evolució en el
model de prototips, en que aquests es dissenyen per ajudar al client a comprendre els requisits, però no per disposar de versions a millorar. 

La solució la presenten els cicles de vida evolutius, que amb una estructura iterativa, permeten als enginyers desenvolupar versions cada vegada més completes del programari.

#### Cicle de vida incremental

Aquest model combina el model lineal seqüencial amb la filosofia de creació de prototips. Per a això, va generant seqüències lineals de desenvolupament al mateix temps que cada seqüència lineal produeix un "increment" en el programari, el qual va
progressant.

El primer increment sol ser un desenvolupament que tan sols incorpora els requisits i funcionalitats més bàsiques. Les versions successives consisteixen en modificacions de cada versió anterior, a la qual s'afegeixen noves funcionalitats i
modificacions, es van lliurant les diferents versions o increments d'acord es van acabant. A diferència del prototipat, cada increment aprofita la versió anterior, i és una versió del producte final a falta d'algunes
funcionalitats. L'esquema que segueix aquest tipus de cicle de vida és el següent:

![Incremental](../images/incremental.png?width=700px)


Aquest tipus de cicle de vida és molt avantatjós des del punt de vista de costos temporals i flexibilitat en la planificació del projecte. Els primers increments no requereixen molt personal, mentre que per als següents es poden anar afegint més o menys funcionalitats segons la quantitat de personal de què es disposi o bé segons que es disposi o no de determinats recursos.

#### Cicle de vida en espiral
És un procés evolutiu que combina la interactivitat del prototipat amb els aspectes sistemàtics del model en cascada. Cada volta de l'espiral consta de les mateixes fases que el cicle en cascada:
+ **Planificació:** determina objectius, requisits i restriccions de el projecte.
+ **Anàlisi de risc:** analitza alternatives, identifica i resol riscos
+ **Enginyeria:** desenvolupament del producte.
+ **Avaluació de client:** es valoren els resultats obtinguts.

Segueix les directrius del model PDCA (Plan Develop Check Act) de Demming, i segueix la filosofia del moviment Agile resumit en el [Manifiesto Agile](https://agilemanifesto.org/), una de les seves implementacions més conegudes és [SCRUM](https://es.wikipedia.org/wiki/Scrum_(desarrollo_de_software)).

![Incremental](../images/espiral.png?width=700px)


El principal **avantatge** del model en espiral és que és el més adequat per projectes amb **riscs**. Com el programari va evolucionant, el desenvolupador i client poden anar comprenent cada vegada millor els riscos conforme es va passant per diferents nivells d'evolució. El mecanisme utilitzat per minimitzar
riscos es basa en poder incorporar el prototipat en qualsevol etapa d'evolució del producte.

Davant d'aquest avantatge, es troba l'inconvenient de requerir una alta habilitat en els enginyers per avaluar riscos. L'èxit depèn molt d'ella, ja que un risc no descobert pot donar lloc a problemes.
