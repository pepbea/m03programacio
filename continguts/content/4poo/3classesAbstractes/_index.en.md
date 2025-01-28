---
date: 2016-04-09T16:50:16+02:00
title: Classes abstractes i finals
weight: 3
pre: "3. "
---

#### Classes abstractes

{{% notice note %}}
**Classes abstractes** (Abstract class). Quan definim **una classe abstracta indiquem a Java que NO VOLEM instanciar/crear objectes concrets d'aquesta classe**. Segurament ens servirà com a template per tal d'adoptar un comportament comú i extendre-la a una sèrie de fills que SÍ tenen sentit. El mateix és aplicable als mètodes, **un mètode abstract és només la signatura del mètode sense implementació** i s'extendrà en les seves subclasses.
{{% /notice %}}

```java
public abstract class Vehicle {
    protected int preu=-1;

    public Vehicle(){}

    public int getPreu (int preu){
        return preu;
    }

    public void setPreu (int preu){
        this.preu += preu;
    }

    public abstract int factura(int dies);

}
public class Cotxe extends Vehicle{
    protected int preu=25;

    public Cotxe(){
        super();
    }

    public int factura(int dies){
        return dies * preu;
    }
}
public class Moto extends Vehicle{
    protected int preu=10;

    public Moto(){
        super();
    }

    public int factura(int dies){
        if(dies>10) return dies * preu;
        else return 0;
    }
}

public class Caravana extends Vehicle{
    protected int preu=40;

    public Caravana(){
        super();
    }

    public int factura(int dies){
        return (dies * preu) / 2;
    }
}

....

public static void main (String[] params){
    Cotxe cotxe = new Cotxe();
    Moto moto = new Moto();
    Caravana caravana = new Caravana();

    cotxe.factura(10);
    moto.factura(10);
    caravana.factura(10);
    ...
}

//També podria tenir
public static void main (String[] params){
    Vehicle cotxe = new Cotxe();
    Vehicle moto = new Moto();
    Vehicle caravana = new Caravana();
}
```

Amb l'exemple anterior, si modelitzem un parking, cada vehicle pagarà una factura diferent en funció al vehicle que tingui. Ens interessa tenir una classe principal Vehicle, la qual no tindrà implementació i que serveix per definir un mètode factura abstracte que hauran d'implementar-se en totes les subclasses. Volem aplicar diferent comportament en funció a cada vehicle per això definim el mètode de pagament `factura(int dies)` dins les subclasses. En aquest exemple Vehicle no tindria sentit com a instància de classe però sí que serveix per establir QUÈ han de tenir els Vehicles del nostre model implementat obligatòriament.

El mètode abstracte `factura(int dies)` de Vehicle no té implementació i obligatòriament cal implementar-lo en les classes concretes filles que tingui Vehicle. Això ens permet establir condicionants a la factura EN FUNCIÓ de cada Vehicle, per exemple si és una Moto i aparca menys de 10 dies no paga, si és una Caravana pagarà la meitat, etc.

Una **classe abstracta pot contenir mètodes concrets implementats**, com getPreu o setPreu en l'exemple, ** i mètodes abstractes** com factura.

- El que ens indica `que una classe sigui abstracta és que no podem crear objectes/instàncies d'aquesta classe`. S'ha d'instanciar a partir dels seus fills.
- El que ens indica `que un mètode sigui abstracte és que no té implementació definida`. Els mètodes abstractes només tenen sentit dins de classes abstractes. Serveixen per indicar que tots els fills concrets han d'implementar aquest mètode.

Aquesta unificació de criteris fa que **sigui molt fàcil extendre el model** i incorporar de forma fàcil nous Vehicles: Camions, Bicicletes o Patinets, només ens cal pensar quins són els mètodes abstractes que necessitem tenir per incorporar i implementar-los, en el cas anterior només cal el mètode factura(). Molts cops es fa necessari tenir tots els vehicles dins un array per a que facin una determinada acció, posem per cas l'exemple anterior i fem que tots els vehicles paguin la factura de cop:

```java
public static void main (String[] params){
        Cotxe cotxe1 = new Cotxe();
        Moto moto1 = new Moto();
        Caravana caravana2 = new Caravana();
        ArrayList<Vehicle> vehicles = new ArrayList();
        vehicles.add(cotxe1);
        vehicles.add(moto1);
        vehicles.add(caravana2);

        for(Vehicle v : vehicles){
            v.factura(10);
            System.out.println("El vehicle "+ v.getClass()+" li toca pagar per 10 dies: " + v.factura(10)+" euros.");
        }

    }
    ...
}
```

Resumint:

- Una classe abstracta no s'instancia, sinó que només ho poden fer les seves subclasses i els anomenarem classes concretes.
- Una classe abstracta pot tenir mètodes abstractes i implementats dins la mateixa classe.
- Un mètode abstracte no té implementació i obliga que les subclasses l'implementin.
- Podríem tenir una classe abstracta amb tots els mètodes implementats, però en canvi, si un mètode és abstracte obliga que la classe també ho sigui.
- No podem tenir un mètode estàtic i abstracte ja que el podríem usar sense necessitat de crear un objecte, i ja sabem que un mètode abstracte no té implementació.
- Podríem tenir una jerarquia de classes abstractes. Una classe abstracta que a la vegada la subclasse sigui abstracta. L'únic requisit és que les classes concretes implementin TOTS els mètodes abstractes de totes les classes abstractes.
