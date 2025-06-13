
# Method Reference
Referências de método, introduzidas no Java 8, são uma forma simplificada de expressões lambda para chamar métodos diretamente. Elas permitem referenciar métodos ou construtores existentes por nome, tornando o código mais legível e conciso.

### Tipos de Referências de Método
Existem quatro tipos principais de referências de método:


- 1 Referência a um Método Estático
```java
import java.util.function.Function;

public class MethodReferenceExample {
    public static void main(String[] args) {
        Function<String, Integer> methodReferenceFunction = Integer::parseInt;
        System.out.println(methodReferenceFunction.apply("123")); // 123
    }
}
```
- 1. Referência a um Método de Instância de um Objeto Específico
```java
import java.util.function.Supplier;

public class MethodReferenceExample {
    public static void main(String[] args) {
        String str = "Hello, World!";
        Supplier<Integer> methodReferenceSupplier = str::length;
        System.out.println(methodReferenceSupplier.get()); // 13
    }
}
```
- 3. Referência a um Método de Instância de um Objeto Arbitrário de um Tipo Específico
```java
import java.util.Arrays;
import java.util.List;

public class MethodReferenceExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
        names.forEach(System.out::println);
    }
}
```
- 4. Referência a um Construtor

```java
import java.util.function.Supplier;
class Person {
    private String name;

    public Person() {
        this.name = "Default Name";
    }

    @Override
    public String toString() {
        return name;
    }
}
public class MethodReferenceExample {
    public static void main(String[] args) {
        Supplier<Person> methodReferenceSupplier = Person::new;
        System.out.println(methodReferenceSupplier.get()); // Default Name
    }
}
```