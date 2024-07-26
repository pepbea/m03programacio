---
title: Excepcions
weight: 9
pre: "9. "
chapter: false
---

L'API de Java s'organitza per paquets que agrupen diferents funcionalitats. Entre elles trobem el tractament de les excepcions. En Java es distingeix una excepció d'un error, per això també tenen les seves pròpies classes Exception i Error. 

{{% notice note %}}
Els **Errors** corresponen a situacions irrecuperables que no depenen del programador i que per tant no tenim mecanismes per poder tractar-les. Quan apareix un error provoca la finalització del programa.
{{% /notice %}}
 
{{% notice note %}}
Les **Excepcions** són casuístiques que es produeixen en **temps d'execució** i que poden provocar problemes en el desenvolupament normal del nostre programa, aquestes sí que Java pot preveure-les i realitzar-ne un codi per tractar-les.
{{% /notice %}}

Existeixen dos tipus d'excepcions:
- **Implícites**: són aquelles casuístiques pròpies de la JVM i que estan incloses dins la classe RuntimeError. Normalment tenen a veure amb errors de programació.
- **Explícites**: són aquelles que no tenen a veure amb RuntimeError i que el programador les pot tractar allà on tenen lloc.

Per tal de tractar les excepcions quan es produeixen Java ofereix el mecanisme de try-catch-finally.

```java
try{
    //bloc de codi que provoca l'excepció
}catch(nomClasse Excepcio e){
    //tractament de l'excepció
}finally{
    //encara que hi hagi excepció codi que s'executarà sempre
}
```

El codi que trobem dins el bloc `try` és aquell que estem "vigilant" o és sospitós de llançar una excepció, per exemple quan obrim un fitxer que no existeix, tenim una ruta que està malament o intentem dividir entre 0. 

En casos com els anteriors la JVM genera una Excepció que pot ser tractada dins el bloc `catch`. Un cop es detecta l'existència d'una excepció el que fa Java és comprovar si existeix algun bloc catch (poden haver-ne més d'un, **els escriurem del més específic al més genèric**), entra en el primer que coincideixi l'Exception i n'executa el codi de dins el bloc. 

Si no existeix cap bloc catch que "capturi" el tipus d'excepció, aquesta és llançada al bloc de codi que ha cridat aquest mètode i funció, de forma que serà el responsable de tractar-la. 

Si es dóna el cas que aquesta excepció no es controla, ni tan sols en el main, es produeix una finalització anormal de l'execució del programa.

El codi contingut en el bloc `finally` s'executa sempre, hi hagi o no una excepció. Això ens pot anar molt bé quan hi ha codi que sempre s'ha d'executar independentment de l'existència o no d'una excepció, per exemple el tancament d'una base de dades o el tancament d'un descriptor de fitxer.

Resumint, quan dins un bloc try es produeix una excepció, la JVM llança (throw) una excepció que serà capturada (catch) per un bloc catch o per un codi superior que hagi cridat aquest mètode/funció.

Exemples d'error:
- Ens quedem sense memòria.
- Falla el canal d'E/S.
- Falla el servei d'algun proveïdor.

Exemples d'excepcions:
- Fitxer que no té permisos.
- Fitxer inexistent.
- Operació aritmètica errònia (dividir per zero).
- Accés a una posició d'una taula inexistent.
- Accés a una referència a un objecte inexistent.

**Exemples d'excepcions** 

*IllegalArgumentException*

En el cas del switch vist en l'apartat d'estructura de selecció hem vist aquest tipus d'excepció, es produïa quan s'intentava accedir a un element de l'enum (Enumeració) que no existia. En l'exemple veureu com es realitza el `try catch`.

*IllegalStateException*

També en els exemples de l'estructura de selecció, en l'exemple 4, s'observa com es pot tractar l'error inesperat de rebre un valor de l'argument del switch *inesperat*, una opció és que el propi default "llançi" una excepció si s'hi arriba. (**throw new Exception**).

*InputMismatchException*

Introducció d'un valor a una variable que NO és del mateix tipus.

```java
public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);
    int n;
    do{
        try{
            System.out.print("Introdueix un nombre > 0:";                                            
            n = sc.nextInt();
            System.out.println("Nombre introduït: " + n);
        }catch(InputMismatchException e){
            sc.nextLine();
            n = 0;
            System.out.println("Has d'introduir un nombre enter: " + e.toString());            
        }
      }while(n<=0);
}
```

*ArithmeticException*

Operació aritmètica errònia.

```java
public static void main(String[] args) {
    int numerador = 10;
    int denominador = 0;
    try{                                 
        int n = numerador / denominador;
    }catch(ArithmeticException e){
        System.out.println("Has volgut dividir entre 0 : " + e.toString());  
        n = 0;          
    }
}
```

En tots els casos anteriors haguessis pogut substituir el tipus de l'Excepció per `Exception` ja que tots són de tipus Exception només que estan especialitzats pel tipus d'error que capturen.

Fins el moment les excepcions han estat generades per la JVM quan s'ha detectat una casuística inesperada, però les excepcions es poden generar manualment emprant `throw new Exception`. Per exemple:

```java
public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);
    int numerador = sc.nextInt();
    int denominador = sc.nextInt();
    int n;
    try{                                
        if (denominador == 0) throw new ArithmeticException(); 
        else n = numerador / denominador;
    }catch(ArithmeticException e){
        System.out.println("Has volgut dividir entre 0 : " + e);  
        n = 0;          
    }finally{
        System.out.println(n);
    }
}
```
