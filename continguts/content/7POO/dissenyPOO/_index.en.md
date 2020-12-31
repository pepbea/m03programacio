---
title: Recursivitat
weight: 4
---

{{% notice note %}}
**Definició** 
Un subprograma és recursiu quan al llarg de la seva execució s’efectua alguna crida **a si mateix**.<br><br>
Des d’un punt de vista tècnic s’efectua una crida d’un programa a un altre programa, amb la particularitat de que aquest programa és el mateix.

{{% /notice %}}

<br>

#### PARTS de la crida recursiva

En una situació recursiva s’ha de pensar en:
1. **Quan acaba? Cas Base:**
  * Solució senzilla
  * No s’activa més recursió.
  * En tot algorisme recursiu hi ha d’haver almenys un cas base

2. **Com continua? Cas recurrent:**
  * Efectuarem una crida a la mateixa funció per acostar-nos al cas base.
  * Poden incloure’s passos addicionals a més de la crida recursiva

<br>

#### Avantatges

> **Què ofereix la recursivitat?**
>> * Codi elegant i senzill
>> * Solucions òptimes a problemes iteratius que computacionalment són complexos

> **Què NO ofereix la recursivitat?**
>> * Creació de moltes variables
>> * Guardem molta informació de crides a funció en memòria.

<br>

#### Com funciona?

El procés d’execució recursiu consisteix en una cadena de generació de crides a la mateixa funció.
En cada crida:
* Es reserva l’espai en memòria necessari per emmagatzemar els paràmetres i els objectes locals usats en el subprograma.
* Es reben els paràmetres i es cedeix l’execució d’instruccions al subprograma que comença a executar-se.
* A l’acabar la seva feina, allibera l’espai reservat, els identificadors locals deixen de tenir vigència i passa l’execució de la instrucció següent a la crida.

<br>

#### Comparativa Iteratiu vs Recursiu

|Iteratiu|Recursiu|
|---|---|
|Realitza una petició|Realitza una petició|
|Repeteix el cos del bucle|Repeteix les crides a mètodes recursius|
|Té una condició d’acabament|Té una condició d’acabament|
|S’acaba quan es compleix la condició  de continuació del bucle|S’acaba quan la crida arriba al cas base, desencadenant una sequència de crides enrera|
|S’ha de complir la condició d’acabament|S’ha de complir que s’arriba al cas base|


{{% notice note %}}
**TOT algorisme iteratiu es pot representar recursiu i tot algorisme recursiu es pot representar iteratiu** 
{{% /notice %}}


<br>

#### Exemple factorial

**Iteratiu**

```java
int factorial;
int nombre = sc.nextInt();
for(int i=0; i < nombre; i++){
    factorial = factorial * i;
}
```

**Recursiu**
```java
int nombre = 5;
5 * factorial(4)
    4 * factorial(3)
        3 * factorial(2)
            2 * factorial(1)
                1;


public int factorial (n){
    if(n==1) return 1;
    else return n * factorial (n-1);
}                
```

![array](../images/factorialRecursiu.png?width=500px)

![array](../images/factorialRecursiu2.png?width=700px)

#### Exemples
<br>
Suma de dos nombres: 

```java
public static int suma(int a, int b) {
    if (b == 0) return a;
    else if (a == 0) return b;
    else  return 1 + suma(a, b - 1);
}
```
<br>
Suma elements d'un vector: 

```java
public static int sumaVector(int t[], int n){
        if(n==0)return t[0];
        else return t[n] + sumaVector(t,n-1);
    }
```
<br>
Cerca dicotòmica: 

```java
public class CercaDicotomica {
 
public static void main(String[] args) {
    CercaDicotomica programa = new CercaDicotomica();
    programa.inici();
}
 
public void inici() {
    int[] array = {2, 4, 6, 8, 10, 12, 14, 16, 18, 20};
    int cercaDivuit = cercaDicotomica(array, 0, array.length-1, 18);
    int cercaCinc = cercaDicotomica(array, 0, array.length-1, 5);
    System.out.println("Cerca del 18: " + cercaDivuit);
    System.out.println("Cerca del 5: " + cercaCinc);
}
 
/** Cerca dicotòmica recursiva sobre un array d'enters.
  *
  * @param array On es fa la cerca
  * @param inici Posició inicial de la cerca
  * @param fi Posició final
  * @param valor Valor a cercar
  * @return Índex on és el valor, o -1 si no existeix
  */
public int cercaDicotomica(int[] array, int inici, int fi, int valor) {
    //CAS BASE: No s'ha trobat el valor
    if (inici > fi) return -1;

    //Es calcula la posició central entre els dos índexs de cerca
    int pos = inici + (fi - inici) / 2;

    //CAS RECURSIU: Si el valor es menor que la posició que s'ha mirat
    //llavors cal seguir cercant per la part "dreta" de l'array
    if (array[pos] > valor) return cercaDicotomica(array, inici, pos - 1, valor);
    
    //CAS RECURSIU: Si el valor és més gran que la posició que s'ha mirat
    //llavors cal seguir cercant per la part "esquerra" de l'array
    else if (array[pos] < valor) return cercaDicotomica(array, pos + 1, fi, valor);
     
    //CAS BASE: És igual, per tant, s'ha trobat
    else return pos;
}
```


