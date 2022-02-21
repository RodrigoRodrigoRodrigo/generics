package application;

import java.util.Scanner;

import services.PrintService;

public class Program {

	public static void main(String[] args) {

		Scanner sc = new Scanner(System.in);

		PrintService<Integer> ps = new PrintService<>();
		/*
		 * e se eu quiser mudar pra tipo String, double, etc... é só eu mudar o Integer na lista.
		 * e mudar o tipo do resto tambem.
		 */
		
		System.out.print("How many values? ");
		int n = sc.nextInt();
		
		for (int i = 0; i < n; i++) {
			Integer value = sc.nextInt();
			ps.addValue(value);
		}

		ps.print();
		Integer x = ps.first();
		System.out.println("First: " + x);
		
		sc.close();
	}
}

===========================================================================

package services;

import java.util.ArrayList;
import java.util.List;

public class PrintService<T> {
	/*
	 * a minha classe é um PrintService do tipo <T>, esse T pode ser o nome que voce quiser
	 */

	private List<T> list = new ArrayList<>();
	/*
	 * se a minhya classe é de um tipo T qualquer, a minha lista tambem tem que ser, e eu vou fazer agora a mesma 
	 * coisa com as operações 
	 */

	public void addValue(T value) {
		list.add(value);
	}

	public T first() {
		if (list.isEmpty()) {
			throw new IllegalStateException("List is empty");
		}
		return list.get(0);
	}

	public void print() {
		System.out.print("[");
		if (!list.isEmpty()) {
			System.out.print(list.get(0));
		}
		for (int i = 1; i < list.size(); i++) {
			System.out.print(", " + list.get(i));
		}
		System.out.println("]");
	}
}
							  
[13-generics-set-map.pdf](https://github.com/yarisb/generics/files/8111340/13-generics-set-map.pdf)
							  
![1](https://user-images.githubusercontent.com/61166475/155007183-0ae352ae-61f1-4513-8e35-910d9492293b.png)
