package application;

import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;
import java.util.Locale;

import entities.Product;
import services.CalculationService;

public class Program {

	public static void main(String[] args) {

		Locale.setDefault(Locale.US);
		
		List<Product> list = new ArrayList<>();

		String path = "C:\\Projetos\\inn.txt";

		try (BufferedReader br = new BufferedReader(new FileReader(path))) {

			String line = br.readLine();
			while (line != null) {
				String[] fields = line.split(",");
				/*
				 * Esse split vai recortar cada pedaço do string entre asd virgulas, guardando cada pedaço no vetor
				 */
				list.add(new Product(fields[0], Double.parseDouble(fields[1])));
				/*
				 * então agora aqui na hora de inserir a lista, eu vou instanciar um produto ai eu vou passar aqui o nome
				 * do produto(fields) na posição zero, antes da virgula, que é aonde ficou armazenado o pedaço do nome, e o preço do 
				 * produto vai ser o fields na posição 1, depois da virgula.
				 */
				line = br.readLine();
			}
			
			Product x = CalculationService.max(list);
			System.out.println("Most expensive:");
			System.out.println(x);

		} catch (IOException e) {
			System.out.println("Error: " + e.getMessage());
		} 
	}
}

===========================================================================

package entities;

public class Product implements Comparable<Product> {

	private String name;
	private Double price;
	
	public Product(String name, Double price) {
		this.name = name;
		this.price = price;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public Double getPrice() {
		return price;
	}

	public void setPrice(Double price) {
		this.price = price;
	}

	@Override
	public String toString() {
		return name + ", " + String.format("%.2f", price);
	}

	@Override
	public int compareTo(Product other) {
		return price.compareTo(other.getPrice());
	}
}

===========================================================================

package services;

import java.util.List;

public class CalculationService {

	public static <T extends Comparable<T>> T max(List<T> list) {
		/*
		 * eu estou falando aqui que esse metodo vai trabalhar com algum tipo <T> que extende o comparable do tipo<T>
		 * com um metodo chamando max que retorna um objeto do tipo <T>, que tem uma lista do tipo <T>.
		 * 
		 * esse meu metodo (max) ele vai trabalhar com qualquer tipo <T>, desde que o <T> seja qualquer subtipo 
		 * de Comparable<T>.
		 */
		if (list.isEmpty()) {
			throw new IllegalStateException("List can't be empty");
		} 
		T max = list.get(0);
		for (T item : list) {
			if (item.compareTo(max) > 0) {
				max = item;
			}
		}
		return max;
	}
}

[13-generics-set-map.pdf](https://github.com/yarisb/generics/files/8111353/13-generics-set-map.pdf)
	
![1](https://user-images.githubusercontent.com/61166475/155007335-bf35430f-8690-4af4-bbc9-7dd6b26d41be.png)
