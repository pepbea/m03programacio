---
date: 2016-04-09T16:50:16+02:00
title: Tractament de les excepcions
weight: 4
pre: "4.2. "
---

La Jerarquia de classes establerta de Java pel que fa Error i Exception és la següent.

![Jerarquia](./images/jerarquia.jpg?width=500px)

**Exemples d'excepcions** 

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

Els casos anteriors haguessis pogut substituir el tipus de l'Excepció per `Exception` ja que tots són de tipus Exception només que estan especialitzats pel tipus d'error que capturen.

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

En Java les excepcions que són subclases de Error o RuntimeException no necessiten ser especificades en la llista de throws, Java ho fa automàticament, la resta d'Excepcions sí és necessari, del contrari es produeix un error en temps de compilació.

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
                    System.out.println(nums[i] + " / " + denom[i] + " es " + nums[i] / denom[i]);
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
