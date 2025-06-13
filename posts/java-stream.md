![](../assets/streamapi.jpg)
# Stream API
A Java Stream API é uma ferramenta introduzida no java que facilita o processamento de coleções de dados de maneira declarativa e funcional. Streams permitem operações sofisticadas em dados de forma simples e eficiente, proporcionando um código mais limpo e conciso. Neste artigo, exploraremos o que é Stream, como utilizá-lo e exemplos práticos de suas principais operações.

## O que é Java Stream?
Java Stream é uma sequência de elementos que suporta operações de agregação de dados em coleções, como listas, conjuntos e mapas. Ele permite que você execute operações de maneira paralela ou sequencial sem precisar escrever loops tradicionais. Stream não é uma estrutura de dados em si, mas sim uma sequência de elementos que pode ser processada de maneira declarativa.

## Características Principais do Java Stream
- Declarativo e Funcional: As operações do Stream são expressas de forma declarativa, permitindo um código mais limpo e conciso usando expressões lambda.

- Preguiçoso (Lazy): As operações em um Stream não são executadas até que um resultado seja necessário. Isso permite otimizações internas, como evitar processar elementos desnecessários.

- Possibilidade de Paralelismo: Muitas operações de Stream são projetadas para facilitar a execução paralela, melhorando o desempenho em sistemas com vários núcleos de processamento.

### Sintaxe

```java
List<Integer> numerosParesAoQuadrado = numeros.stream()       // Obtendo um Stream a partir da lista
                                                .filter(n -> n % 2 == 0)  // Filtrando números pares
                                                .map(n -> n * n)          // Mapeando para o quadrado de cada número
                                                .collect(Collectors.toList());  // Coletando o resultado em uma lista
                                                
```

## Métodos Principais do Stream API

### filter()
O método filter() é usado para filtrar elementos com base em um predicado. Ele retorna um Stream contendo apenas os elementos que satisfazem o predicado especificado.

Exemplo:

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class ExemploMetodosStream {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("maçã", "banana", "laranja", "abacaxi", "uva");

        // Filtrar frutas que começam com 'a'
        List<String> frutasFiltradas = frutas.stream()
                                            .filter(fruta -> fruta.startsWith("a"))
                                            .collect(Collectors.toList());

        System.out.println(frutasFiltradas); // Saída: [maçã, abacaxi]
    }
}
```
### map()
O método map() transforma cada elemento do Stream aplicando uma função e retorna um novo Stream com os elementos transformados.

Exemplo:

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class ExemploMetodosStream {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("maçã", "banana", "laranja");

        // Mapear frutas para seus tamanhos
        List<Integer> tamanhos = frutas.stream()
                                      .map(fruta -> fruta.length())
                                      .collect(Collectors.toList());

        System.out.println(tamanhos); // Saída: [4, 6, 7]
    }
}
```
### sorted()
O método sorted() classifica os elementos do Stream com base na ordem natural ou usando um Comparator personalizado e retorna um novo Stream com os elementos ordenados.

Exemplo:

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class ExemploMetodosStream {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("laranja", "banana", "maçã");

        // Ordenar as frutas em ordem alfabética
        List<String> frutasOrdenadas = frutas.stream()
                                            .sorted()
                                            .collect(Collectors.toList());

        System.out.println(frutasOrdenadas); // Saída: [banana, laranja, maçã]
    }
}
```
### collect()
O método collect() é usado para coletar os elementos do Stream em uma coleção específica, como List, Set ou Map.

Exemplo:

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class ExemploMetodosStream {
    public static void main(String[] args) {
        List<String> frutas = Arrays.asList("maçã", "banana", "laranja");

        // Coletar frutas que começam com 'a' em um Set
        List<String> frutasFiltradas = frutas.stream()
                                            .filter(fruta -> fruta.startsWith("a"))
                                            .collect(Collectors.toList());

        System.out.println(frutasFiltradas); // Saída: [maçã]
    }
}
```
### reduce()
O método reduce() realiza uma redução dos elementos do Stream para retornar um único resultado. Pode ser usado para calcular soma, produto, concatenação, etc.

Exemplo de soma:

```java
import java.util.Arrays;
import java.util.List;

public class ExemploMetodosStream {
    public static void main(String[] args) {
        List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5);

        // Somar todos os números
        int soma = numeros.stream()
                          .reduce(0, (a, b) -> a + b);

        System.out.println("Soma: " + soma); // Saída: Soma: 15
    }
}
```
