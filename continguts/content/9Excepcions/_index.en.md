---
title: Excepcions
weight: 9
pre: "<b>9. </b>"
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

En casos com els anteriors la JVM genera una Excepció que pot ser tractada dins un bloc `catch`. Un cop es detecta l'existència d'una excepció el que fa Java és comprovar si existeix algun bloc catch (poden haver-ne més d'un, els escriurem del més específic al més genèric), entra en el primer que coincideixi l'Exception i n'executa el codi de dins el bloc. 

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

La Jerarquia de classes establerta de Java pel que fa Error i Exception és la següent.

![Jerarquia](../images/jerarquia.jpg?width=500px)

**Exemples d'excepcions** 

*InputMismatchException*

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

*ArrayIndexOutOfBoundsException*

```java
public static void main(String[] args) {
    int arr[]=new int[10];
    try {
        int valor=arr[10];
    }catch (ArrayIndexOutOfBoundsException e){
        System.out.println("Índex fora de límit!: "+ e.getMessage());

    }
}
```

Tots els casos anteriors haguessis pogut substituir el tipus de l'Excepció per `Exception` ja que tots són de tipus Exception només que estan especialitzats pel tipus d'error que capturen.

Tot seguit anem a veure com capturem una excepció que es produeix en un altre mètode que cridem des del principal, posem per exemple l'ArithmeticException anterior.

```java
public static void main(String[] args) {
    public static int numerador = 10;
    public static int denominador = 0;
    try {
		dividir();
	} catch (ArithmeticException e) {
		System.err.println(e);
	}
}

public static void dividir() throws ArithmeticException {
		System.out.println(numerador / denominador);
}
```

En el cas anterior si no capturéssim l'excepció en el main() hi hauria un error i pararia el programa, però com que "capturem" l'excepció i en fem un tractament específic Java continua amb la seva excecució normal. Fixeu-vos que en aquest cas en el mètode dividir() hem utilitzat `throws ArithmeticException`, d'aquesta manera quan es detecta una excepció d'aquest tipus, l'excepció és propagada cap a la funció que ha cridat aquest mètode, derivant-ne així la responsabilitat del seu tractament. 

En Java les excepcions que soón subclases de Error o RuntimeException no necessiten ser especificades en la llista de throws, Java ho fa automàticament, la resta d'Excepcions sí és necessari, del contrari es produeix un error en temps de compilació.

Es podrien encadenar uns quants throws Exception com seria:

```java
public static void main(String[] args) {
    public static int numerador = 10;
    public static int denominador = 0;
    try {
		dividir1();
	} catch (ArithmeticException e) {
		System.err.println(e);
	}
}

public static void dividir1() throws ArithmeticException {
		dividir2;
}

public static void dividir2() throws ArithmeticException {
		System.out.println(numerador / denominador);
}
```

*Jerarquia de les Excepcions*

Com us he comentat anteriorment, la captura de l'Excepció és jeràrquica, de forma que l'excepció serà capturada pel primer Catch que l'accepti, per això és tant important ordenar els catch de més específic a més genèric. Continuant amb l'exemple anterior:

```java
public static void main(String[] args) {
    int numerador = 10;
    int denominador = 0;
    try{                                 
        int n = numerador / denominador;
    }catch(ArithmeticException e){
        System.out.println("Has volgut dividir entre 0 : " + e.toString());  
        n = 0;          
    }catch(Exception e){
        System.out.println("Aquí no s'hi accedirà ja que l'Excepció en aquest cas serà capturada per ArithmeticException");          
    }
}
```

*Exemples més complerts amb encadenament d'excepcions*

Un exemple més complert on barregem diferents Exceptions podria ser el següent:

```java
public class TryEncadenat{
    public static void main(String[] args) {
        int nums[]={4,8,16,32,64,128,256,512};
        int denom[]={2,0,4,4,0,8};
        try {
            for (int i = 0; i < nums.length; i++) {
                try { 
                    System.out.println(nums + " / " + denom + " es " + nums / denom);
                } catch (ArithmeticException exc) {
                    System.out.println("No es pot dividir entre 0!");
                }
            }
        }
        catch (ArrayIndexOutOfBoundsException exc) {
                    System.out.println("Un dels dos arrays s'ha quedat sense més valors. FINALITZA aquí!");
                }
            }
        }

```

Un altre exemple podria ser:

```java
public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);
    int [] array = {4,2,6,7};
    int n;
    boolean repetir = false;
    do{
         try{
                repetir = false;
                System.out.print("Introdueix un valor > 0 i < " + array.length + " ");                     
                n = sc.nextInt();
                System.out.println("Valor en la posició " + n + ": " + array[n]);
         }catch(InputMismatchException e){
                   sc.nextLine();
                   n = 0;
                   System.out.println("Has d'introduir un valor enter ");
                   repetir = true;
         }catch(IndexOutOfBoundsException e){
                  System.out.println("Has d'introduir un valor enter > 0 i < " + array.length + " ");           
                  repetir = true;
         }catch(Exception e){ //Resta d'excepcions
                   System.out.println("Error inesperat " + e.toString());
                   repetir = true;
         }
     }while(repetir);
}
```

Un altre exemple **multi-exception**


Fins el moment les excepcions han estat generades per la JVM quan s'ha detectat una casuística inesperada, però les excepcions es poden generar manualment emprant `new throw Exception`. Per exemple:

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
        System.out.println("Has volgut dividir entre 0 : " + e.toString());  
        n = 0;          
    }finally{
        System.out.println(n);
    }
}
```

**Excepcions pròpies**

També és possible generar les nostres pròpies Excepcions. Moltes vegades, degut a l'especificació que tenim, és necessari que creem les nostres pròpies excepcions que dónen sentit a certes circumstàncies i que el ventall d'Excepcions de Java no cobreix. L'únic que haurem de fer és heredar de la classe `Exception` i adaptar el comportament a la constructora i també al missatge de sortida que volem que es mostri quan es produeixi l'excepció. 

```java
public class MajoriaEdatExcepcio extends Exception{

    private int edat;

    MajoriaEdatExcepcio (int n){
        this.edat = n;
    }

    @Override
    public String toString() {
        return "Excepcio: Majoria Edat [edat "+this.edat+"]";
    }
}
```

Aquesta excepció s'instancia un cop es genera l'Excepció (*throw new MajoriaEdatExcepcio(n)*). Per tant, la situació podria ser la següent:

```java
public class MajoriaEdat {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        try{
            int edat = sc.nextInt();
            if(edat<18) throw new MajoriaEdatExcepcio(edat);
            System.out.println("L'edat introduida és major d'edat" + edat);
        }
        catch (MajoriaEdatExcepcio e){
            System.out.println(e);
        }
    }
}
```
