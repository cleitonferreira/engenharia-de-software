# Lambda
As expressões lambda são uma característica poderosa do Java que permite criar instâncias de interfaces funcionais de forma concisa e simplificada. Além disso, podemos reduzir a quantidade de código necessário para criar e implementar interfaces funcionais utilizando expressões lambda.

#### Uma expressão lambda é composta por três partes:

- Lista de parâmetros: Uma lista de parâmetros separados por vírgulas e delimitados por parênteses.
- Operador lambda: ->
- Corpo: O corpo da expressão, que pode ser uma única instrução ou um bloco de código.

#### Sintaxe:

```java
(parameters) -> expression
```
ou

```java
(parameters) -> { statements; }
```
#### Exemplo Básico de Expressão Lambda
Vamos começar com um exemplo simples de expressão lambda que implementa a interface funcional Runnable.

```java
public class LambdaExample {
    public static void main(String[] args) {
        // Expressão lambda que implementa Runnable
        Runnable runnable = () -> System.out.println("Hello, Lambda!");
        
        // Executar o método run da expressão lambda
        runnable.run();
    }
}
```