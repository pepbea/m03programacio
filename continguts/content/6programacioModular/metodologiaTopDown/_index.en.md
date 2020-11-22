---
date: 2016-04-09T16:50:16+02:00
title: Metodologia Top Down
weight: 2
---

**Metodologia Top Down**: L'aplicació de la programació funcional en el desenvolupament d'un programa, dóna lloc a
2 tipus de fluxos de disseny oposats:
1. *Disseny Top-Down*: consisteix a resoldre un problema complex dividint successivament en parts cada vegada més elementals fins que siguin fàcilment abordables per separat. Normalment s'aplica a la fase de disseny.

2. *Disseny Bottom-Up*: consisteix en partir de blocs (funions) elementals i anar unint-los per aconseguir resoldre un problema. Normalment s'aplica a la fase d'implementació.


![topdown](../images/topdown.png?width=500px)

Entre els múltiples avantatges de la programació funcional, es poden citar:
* Afavoreix la reutilització del codi.
* Permet una completa divisió de tasques entre els programadors.
* Facilita el manteniment i l'escalabilitat dels programes.
* Facilita la depuració i la verificació.
* Es complementa perfectament amb la programació estructurada. de fet normalment s'utilitzen juntes.
* Facilita el disseny descendent (top-down) i la filosofia divideix i guanyaràs, disminuint la complexitat dels programes.
* Millora la productivitat.

<br>

**Exemple3: Programa amb diferents funcionalitats**
```java
import java.util.Arrays;
import java.util.Scanner;

public class Activitats {

	
	//Métode que retorna el màxim de 2 nombres. Retorna num1 si són iguals
	public static int maxim (int num1, int num2){
		if(num1>=num2) return num1;
		else return num2;
	}
	
	//Métode que retorna el mínim de 2 nombres. Retorna num2 si són iguals
	public static int min (int num1, int num2){
		if(num1>=num2)return num2;
		else return num1;
	}

	//Métode que donats 3 nombres, retorna una llista ordenada ascendent
	public static int[] ordena (int num1, int num2, int num3){
		int[] llista = {num1,num2,num3};
		Arrays.sort(llista);
		return llista;			
	}
	
	//Métode que retorna el màxim de 3 nombres.
	public static int maxim3 (int num1, int num2, int num3){
		int [] llista = ordena(num1, num2, num3);
		return llista[2];
	}
	
	//Métode que retorna el mínim de 3 nombres.
	public static int min3 (int num1, int num2,int num3){
		int [] llista = ordena(num1, num2, num3);
		return llista[0];
	}
	
	//Métode que retorna el valor màxim d'una matriu.
	public static int minimMatriu (int[][] mat){
		int files = mat.length;
		int columnes = mat[0].length;
		int maxim = 0;
		for(int i=0; i<files;i++){
			for(int j=0; j<columnes;j++){
				if(mat[i][j] > maxim)maxim = mat[i][j];
				//maxim = maxim(maxim, mat[i][j]);
			}
		}
		return maxim;
	}
	
	//Métode que permet crear una matriu amb nombres aleatoris
	public static int[][] creaMatriu (){
		int files = 3;
		int columnes = 3;
		int[][] matriu = new int[files][columnes];

		for (int i = 0; i <files ; i++) {
		    System.out.println("");
		    for (int j = 0; j < columnes; j++) {
		        matriu[i][j] = (int)(Math.random()*100);
		        System.out.print(matriu[i][j] + " ");
		    }
		}
        
        	System.out.println("\n");
		return matriu;
	}
	
	public static void main (String[] args){
		
		Scanner sc = new Scanner(System.in);
		int opcio = 9;
		int num1, num2, num3;
		while(opcio!=0){
			System.out.println("\n\n\n---Tria una opció---\n");
			System.out.println("1. Màxim de dos nombres");
			System.out.println("2. Mínim de dos nombres");
			System.out.println("3. Màxim de tres nombres");
			System.out.println("4. Mínim de tres nombres");
			System.out.println("5. Ordena de forma ascendent tres nombres");
			System.out.println("6. Màxim valor d'una matriu");
			System.out.println("0. Sortir\n");
			System.out.println("---Tria una opció---\n");
			
			opcio = sc.nextInt();
			
			switch(opcio){
				case 1: 
					System.out.println("Introdueix primer valor");
					num1 = sc.nextInt();
					System.out.println("Introdueix segon valor");
					num2 = sc.nextInt();
					System.out.println("El màxim és: "+ maxim(num1,num2));
				break;
				
				case 2: 
					System.out.println("Introdueix primer valor");
					num1 = sc.nextInt();
					System.out.println("Introdueix segon valor");
					num2 = sc.nextInt();
					System.out.println("El mínim és: "+ min(num1,num2));
				break;
				
				case 3: 
					System.out.println("Introdueix primer valor");
					num1 = sc.nextInt();
					System.out.println("Introdueix segon valor");
					num2 = sc.nextInt();
					System.out.println("Introdueix tercer valor");
					num3 = sc.nextInt();
					System.out.println("El màxim és: "+ maxim3(num1,num2, num3));
				break;
				
				case 4: 
					System.out.println("Introdueix primer valor");
					num1 = sc.nextInt();
					System.out.println("Introdueix segon valor");
					num2 = sc.nextInt();
					System.out.println("Introdueix tercer valor");
					num3 = sc.nextInt();
					System.out.println("El mínim és: "+ min3(num1,num2, num3));
				break;
				
				case 5: 
					System.out.println("Introdueix primer valor");
					num1 = sc.nextInt();
					System.out.println("Introdueix segon valor");
					num2 = sc.nextInt();
					System.out.println("Introdueix tercer valor");
					num3 = sc.nextInt();
					int[] llista = ordena(num1,num2,num3);
					System.out.print("L'ordre ascendent dels tres valors és:");
					for(int i=0; i<llista.length; i++){
						System.out.print(llista[i]+" ");				
					}
				break;
				
				case 6: 
					System.out.println("Aquesta és la matriu:");
					int maxim = minimMatriu(creaMatriu());
					System.out.println("El màxim valor de la matriu és: "+ maxim);
				break;
				
				case 0:
					System.out.println("Programa finalitzat");
				break;
			}
		}
		sc.close();
	}
}
```

<br>

