## Class Optional em Java
A classe Optional foi introduzida no Java para lidar com o problema de valores nulos de maneira mais segura e funcional. Ela encapsula um valor que pode ou não estar presente e fornece métodos para lidar com essa possibilidade de forma mais expressiva. Neste artigo, exploraremos o que é a classe Optional, por que ela é útil e como utilizá-la corretamente em suas aplicações Java.

## O Problema dos Valores Nulos
Valores nulos (null) em Java podem levar a exceções NullPointerException, especialmente ao acessar métodos ou propriedades de objetos que podem não ter sido inicializados corretamente. O uso de Optional ajuda a evitar essas exceções ao permitir um tratamento mais seguro e explícito dos casos em que um valor pode ou não estar presente.

## Criando um Optional
Você pode criar um Optional de várias maneiras:

- **of()**: Cria um Optional com um valor não nulo.

```java
Optional<String> optionalString = Optional.of("valor não nulo");
```
- **ofNullable()**: Cria um Optional com um valor que pode ser nulo.

```java
String valorPossivelmenteNulo = null;
Optional<String> optionalNullable = Optional.ofNullable(valorPossivelmenteNulo);
```
- **empty()**: Cria um Optional vazio.

```java
Optional<String> optionalVazio = Optional.empty();
```
## Métodos Principais do Optional
Verificação e Acesso ao Valor
- **isPresent()**: Verifica se o valor está presente no Optional.

```java
Optional<String> optional = Optional.of("valor");
if (optional.isPresent()) {
    // fazer algo com optional.get()
}
```
- **ifPresent()**: Executa uma ação se o valor estiver presente.

```java
Optional<String> optional = Optional.of("valor");
optional.ifPresent(valor -> System.out.println("Valor presente: " + valor));
```
- **get()**: Obtém o valor se presente (evite usar get() sem verificar isPresent() para evitar NoSuchElementException).

```java
Optional<String> optional = Optional.of("valor");
String valor = optional.get();
```
Tratamento de Valores Ausentes
- **orElse()**: Retorna o valor se presente ou um valor padrão se ausente.

```java
Optional<String> optional = Optional.empty();
String valor = optional.orElse("valor padrão");
```
- **orElseGet()**: Retorna o valor se presente ou obtém um valor gerado por uma função se ausente.

```java
Optional<String> optional = Optional.empty();
String valor = optional.orElseGet(() -> "valor gerado dinamicamente");
```
- **orElseThrow()**: Retorna o valor se presente ou lança uma exceção se ausente.

```java
Optional<String> optional = Optional.empty();
String valor = optional.orElseThrow(() -> new RuntimeException("Valor ausente"));
```
Exemplo de Uso do Optional
```java
Copiar código
import java.util.Optional;

public class ExemploOptional {
    public static void main(String[] args) {
        String valorPossivelmenteNulo = null;
        Optional<String> optional = Optional.ofNullable(valorPossivelmenteNulo);

        // Usando métodos Optional
        String valor = optional.orElse("valor padrão");
        System.out.println("Valor: " + valor);

        optional.ifPresent(v -> System.out.println("Valor presente: " + v));
    }
}
```