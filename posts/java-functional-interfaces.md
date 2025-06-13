## Functional Interfaces
Interfaces funcionais são interfaces que possuem exatamente um método abstrato. Essas interfaces podem ter métodos default ou estáticos, mas devem ter apenas um método abstrato. Elas são usadas como o tipo de destino para expressões lambda e referências de método.

### Principais Interfaces Funcionais
Java fornece várias interfaces funcionais pré-definidas no pacote java.util.function. Vamos nos concentrar em algumas das mais comuns:

- Function<T, R>: Recebe um argumento do tipo T e retorna um resultado do tipo R.
```java
import java.util.function.Function;

public class ExemploInterfaceFuncional {
    public static void main(String[] args) {
        // Interface funcional Function (Função)
        Function<String, Integer> tamanhoString = str -> str.length();
        
        // Testando a função
        System.out.println(tamanhoString.apply("Olá")); // 3
    }
}

```
- Consumer<T>: Recebe um argumento do tipo T e não retorna resultado (consome o argumento).
```java
import java.util.function.Consumer;

public class ExemploInterfaceFuncional {
    public static void main(String[] args) {
        // Interface funcional Consumer (Consumidor)
        Consumer<String> imprimir = str -> System.out.println(str);
        
        // Testando o consumidor
        imprimir.accept("Olá, Consumidor!"); // Olá, Consumidor!
    }
}

```
- Supplier<T>: Não recebe argumentos e retorna um resultado do tipo T.
```java
import java.util.function.Supplier;

public class ExemploInterfaceFuncional {
    public static void main(String[] args) {
        // Interface funcional Supplier (Fornecedor)
        Supplier<String> saudacaoFornecedor = () -> "Olá, Fornecedor!";
        
        // Testando o fornecedor
        System.out.println(saudacaoFornecedor.get()); // Olá, Fornecedor!
    }
}

```
- Predicate<T>: Recebe um argumento do tipo T e retorna um booleano (usado para testes).
```java
import java.util.function.Predicate;

public class ExemploInterfaceFuncional {
    public static void main(String[] args) {
        // Interface funcional Predicate (Predicado)
        Predicate<Integer> ehPar = numero -> numero % 2 == 0;
        
        // Testando o predicado
        System.out.println(ehPar.test(4)); // true
        System.out.println(ehPar.test(3)); // false
    }
}

```