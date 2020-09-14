---
date: 2016-04-09T16:50:16+02:00
title: Tipus de Llenguatges
weight: 3
---

Els llenguatges de programació es poden classificar a partir de diferents criteris
1. Segons la proximitat al nucli.
2. Segons el paradigma de programació.
3. Segons la traducció a codi màquina.
4. Segons la generació.

#### 1. Segons la proximitat al nucli

{{% notice note %}}
La proximitat al nucli queda determinat per saber en quin moment s'executa aquest llenguatge. Poden ser llenguatges d'alt nivell, dins el sistema de capes, molt allunyat del nucli, o llenguatges de baix nivell propers al nucli.
{{% /notice %}}

Els llenguatges de programació es poden classificar segons la seva proximitat al llenguatge màquina:

| Llenguatges de baix nivell |
| --- |
| Llenguatge de programació pròxim al nucli de la màquina i que només entén la màquina.|
| Es composa per codi binari (símbols 0 i 1). |
| És el llenguatge més bàsic i també més difícil d'entendre pels humans ja que totes les instruccions són tires de 0s i 1s. |
| És un llenguatge molt lligat a l'arquitectura de la màquina. |
| S'utilitzen adreces de memòria per fer referència a les dades. |
| Les instruccions tenen un format rígid. |

| Llenguatges ensambladors |
| --- |
| Separen les característiques del maquinari de la tasca de programació. |
| Es substitueixen els codis numèrics per representacions textuals equivalents a les instruccions màquina que representen. |
| Segueixen tenint una forta relació amb els llenguatges màquina però permeten utilitzar adreces simbòliques i incloure línies de comentaris. |

| Llenguatges  d'alt nivell |
| --- |
| Alliberen el programador de tasques tedioses i complexes que frenen la productivitat i l'eficiència. | 
| Tenen un gran nivell d'abstracció que fa innecessari el coneixement de l'arquitectura de la màquina. | 
| Les instruccions s'expressen per caràcters alfanumèrics; permeten definir variables; disposen d'instruccions molt ponents de tipus aritmètic, lògiques, tractament de caràcters, etc .; són fàcils de corregir i actualitzar i fàcils d'aprendre. | 
| Per contra, no són tant conscients en quant a consum de recursos.| 

#### 2. Segons el paradigma de programació

{{% notice note %}}
Un paradigma de programació és un **enfoc particular/filosofia** pel disseny i construcció de codi. Depenent de cada context resulta més idoni utilitzar-ne un o altre
{{% /notice %}}

![Paradigmes](../images/paradigms.png?width=500px)

A grans trets diferenciarem entre

+ **Llenguatges imperatius:** 
        - Descriu la programació com una seqüència instruccions o ordres que canvien l'estat d'un programa. 
        - Formen part d'aquest tipus molts llenguatges d'alt nivell i d'ús general: python, c, java, c++ etc.
        - Es fixen en el COM es desenvolupa el codi (com s'aconsegueix un objectiu pas a pas).
        - En aquest paradigma s'inclouen altres paradigmes com el modular, orientació a objectes, concurrent, etc.

+ **Llenguatges declaratius:** 
        - Es fixen en QUÈ descriu (declara la solució), es basa en les propietats de la solució buscada.
        - No es coneix l'algorisme usat per trobar aquesta solució. 
        - No es coneix el rendiment i/o eficiència del codi a priori
        - Molt útil en la resolució de problemes i situacions determinades.
        - En aquest paradigma s'inclouen els paradigmes funcional, lògic i no procedimental.

Com a subtipus dels anteriors destaquem:

{{% expand "Programació estructurada" %}}
 Utilitza únicament seqüències, instruccions condicionals i instruccions repetitives. Es tracta en la UF1 de M03 Programació.
{{% /expand %}}
{{% expand "Programació modular" %}}
 El programa es dissenya per parts(mòduls). Es tracta en la UF2 de M03 Programació.
{{% /expand %}}
{{% expand "Programació orientada a objectes" %}}
 Programació basada en la comunicació i el pas de missatges entre objectes (estructures amb atributs i mètodes). Es tracta en la UF4 de M03 Programació.
{{% /expand %}}
{{% expand "Programació concurrent" %}}
 Útil quan hem de realitzar diverses accions a la vegada i utilitzant recursos compartits. Es tracta en M09 Programació de serveis.
{{% /expand %}}
{{% expand "Programació funcional" %}}
 Tot el codi es basa en funcions, des de l'expressió mínima a qualsevol estructura complexa. Exemple d'aquest paradigma és el llenguatge Lisp o Haskel.
{{% /expand %}}
{{% expand "Programació lògica" %}}
 A partir d'una sèrie de predicats i una base de coneixement es desenvolupa aquest paradigma de relacions lògiques. Exemple d'aquest paradigma és el llenguatge de programació Prolog.
{{% /expand %}}


#### 3. Segons la traducció a codi màquina
{{% notice note %}}
Els llenguatges de programació poden tenir diferents tractaments fins a ser executats, així diferenciem els llenguatges interpretats, compilats i els híbrids.
{{% /notice %}}

Desde que un programa és escrit i és executat per la màquina hi ha un seguit de passos que cal tenir presents:
- Anàlisi (lèxic, sintàtic i semàntic)
- Traducció(generació i optimització de codi)

Depenent de com es realitza aquesta traducció tenim llenguatges compilats i interpretats:

| Llenguatges compilats |
| --- |
| Una vegada el codi és analitzat es genera el codi objecte d'acord amb les característiques del compilador del llenguatge. Depenent del tipus de compilador l'objecte pot ser directament executable o necessita altres passos previs com l'acoblament, l'enllaçat i la càrrega (Com per exemple el llenguatge C).  |
| Per tal de flexibilitzar el codi, els compiladors treballen amb biblioteques de mòduls objecte. Per incloure-les en el codi màquina final s'ha d'usar un enllaçador que retorna un únic programa executable.  |
| Els programes objecte s'executen molt més ràpidament que els interpretats ja que estan optimitzats per uns determinats recursos HW, però no permet transportar codi objecte entre diferents plataformes d'execució.  |
| Exemples de llenguatges els traductors són compiladors són FORTRAN, COBOL, C, PASCAL, ADA ... |


| Llenguatges interpretats |
| --- |
| En aquest cas es duu a la vegada el procés de traducció i el d'execució. La seva forma de treball és anar analitzant instruccions de codi del programa font, generant el codi màquina corresponent i executant.  |
| Són més lents que els compilats, per contra, són fàcilment transportables entre diferents màquines, ja que és el propi programa font el que es mou.  |
| Exemples de llenguatge interpretat són PROLOG, i SQL, Javascript, Python, etc. |


| Llenguatges híbrids |
| --- |
| Aprofiten el millor d'ambdós mons com Java o Visual Studio .NET. Són capaços de compilar el codi a un llenguatge intermedi denominat bytecode en JAVA i MSI en .NET, que després són interpretats per una màquina virtual (MVJ o .NET Framework), així aconsegueixen una substancial millora en el rendiment i mantenen la característica de transportabilitat entre diferents plataformes |

### 4. Segons la generació
{{% notice note %}}
Depenent de quan es va crear el llenguatge s'emmarca en unes necessitats i usos concrets que han donat lloc a generacions. Són seqüencials en el temps.
{{% /notice %}}

{{% expand "Primera generació" %}}
 Són els que corresponen als llenguatges ja vistos de baix nivell o llenguatges màquina.
{{% /expand %}}
{{% expand "Segona generació" %}}
 Són aquells que pertanyen als llenguatges assembladors.
{{% /expand %}}
{{% expand "Tercera generació" %}}
 A la tercera generació pertanyen aquells llenguatges estructurats que seguien un ordre alhora d'executar les instruccions. Llenguatges com C, pascal, cobol, etc.
{{% /expand %}}
{{% expand "Quarta generació" %}}
 A partir d'una sèrie de predicats i una base de coneixement es desenvolupa aquest paradigma de relacions lògiques. Exemple d'aquest paradigma és el llenguatge de programació Prolog.
  Els llenguatges de quarta generació, són els més propers a la sintaxi de la llengua humana, i s'acostumen a utilitzar en les creacions de bases de dades o com a llenguatges de programació dels llenguatges o sistemes d'autor. Són llenguages no procedimentals com SQL que permeten definir quins seran els resultats finals sense necessitat de preocupar-se per saber com fer-ho.
{{% /expand %}}
{{% expand "Cinquena generació" %}}
 Amb la incorporació i expansió dels llenguatges orientats a objectes i amb la generalització de l'ús de les GUI, és possible abarca problemes de major abstracció. Alguns exemples són Java, C++, etc. S'ha generalitzat tant els IDEs de desenvolupament com els CLIs per cada servei/llenguatge.
{{% /expand %}}

