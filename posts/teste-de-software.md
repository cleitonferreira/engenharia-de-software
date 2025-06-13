# Testes unitarios com JUnit 5

JUnit 5 é uma das bibliotecas de teste mais populares para Java, permitindo que desenvolvedores escrevam e executem testes automatizados de forma eficiente. Aqui está um guia simples sobre como começar com JUnit 5.

## O Que é JUnit 5?
JUnit 5 é a versão mais recente do JUnit, uma biblioteca de testes unitários para a linguagem Java. Ele introduz várias melhorias e novos recursos em comparação com suas versões anteriores.

### Estrutura de um Teste JUnit 5
Para criar um teste com JUnit 5, você precisa seguir alguns passos básicos:

- Adicionar JUnit 5 ao Projeto:

Você precisa incluir a dependência do JUnit 5 no seu projeto. Se estiver usando Maven, adicione o seguinte ao seu pom.xml:

```xml
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-engine</artifactId>
    <version>5.7.0</version>
    <scope>test</scope>
</dependency>
```
Se estiver usando Gradle, adicione ao build.gradle:

```groovy
testImplementation 'org.junit.jupiter:junit-jupiter:5.7.0'
```
- Criar uma Classe de Teste:

Crie uma classe para os seus testes. Uma convenção comum é nomear a classe de teste com o mesmo nome da classe que está sendo testada, adicionando o sufixo Test.

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class CalculadoraTest {

    @Test
    void testSomar() {
        Calculadora calculadora = new Calculadora();
        int resultado = calculadora.somar(2, 3);
        assertEquals(5, resultado, "2 + 3 deve ser 5");
    }
}
```
### Anotações Importantes do JUnit 5:

- ```@Test```: Indica que o método é um método de teste.
- ```@BeforeEach```: Executa um método antes de cada teste.
- ```@AfterEach```: Executa um método após cada teste.
- ```@BeforeAll```: Executa um método antes de todos os testes da classe.
- ```@AfterAll```: Executa um método após todos os testes da classe.

```java
import org.junit.jupiter.api.*;

public class ExemploTeste {

    @BeforeAll
    static void configurarAntesDeTodosOsTestes() {
        System.out.println("Executa antes de todos os testes");
    }

    @AfterAll
    static void limparDepoisDeTodosOsTestes() {
        System.out.println("Executa depois de todos os testes");
    }

    @BeforeEach
    void configurarAntesDeCadaTeste() {
        System.out.println("Executa antes de cada teste");
    }

    @AfterEach
    void limparDepoisDeCadaTeste() {
        System.out.println("Executa depois de cada teste");
    }

    @Test
    void testeExemplo() {
        System.out.println("Executa o teste");
        assertTrue(true);
    }
}
```
## Assertivas:

Assertivas são usadas para verificar se os resultados dos testes são como esperado. Algumas das assertivas mais comuns são:

- ```assertEquals(expected, actual)```: Verifica se os valores são iguais.
- ```assertTrue(condition)```: Verifica se a condição é verdadeira.
- ```assertFalse(condition)```: Verifica se a condição é falsa.
- ```assertNotNull(object)```: Verifica se o objeto não é nulo.

```java
import static org.junit.jupiter.api.Assertions.*;

public class CalculadoraTest {

    @Test
    void testSubtrair() {
        Calculadora calculadora = new Calculadora();
        int resultado = calculadora.subtrair(5, 2);
        assertEquals(3, resultado, "5 - 2 deve ser 3");
    }

    @Test
    void testDividirPorZero() {
        Calculadora calculadora = new Calculadora();
        assertThrows(ArithmeticException.class, () -> calculadora.dividir(1, 0), "Divisão por zero deve lançar ArithmeticException");
    }
}
```

## Assumptions
Além das funcionalidades básicas de testes, JUnit 5 introduz o conceito de assumptions (ou suposições). As suposições são usadas para indicar que um teste deve ser executado apenas se certas condições forem verdadeiras. Se uma suposição falhar, o teste será ignorado, mas não será considerado um fracasso. Isso é útil para situações onde certos testes só devem ser executados em condições específicas.

### Quando Usar Assumptions
Assumptions são particularmente úteis para:

- Testes que dependem de um ambiente específico (por exemplo, um sistema operacional ou uma versão específica do JDK).
- Testes que só devem ser executados em determinadas configurações de hardware ou software.
- Testes condicionais em ambientes de integração contínua onde certas variáveis de ambiente ou propriedades do sistema devem estar presentes.

### Tipos de Assumptions
JUnit 5 fornece várias funções de assunção que você pode usar em seus testes:

- assumeTrue: Executa o teste somente se a condição for verdadeira.
- assumeFalse: Executa o teste somente se a condição for falsa.
- assumingThat: Executa uma parte do teste somente se a condição for verdadeira.

Exemplos de Uso
- 1. assumeTrue:

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assumptions.*;

public class AssumptionsTest {

    @Test
    void testSomenteEmAmbienteDeDesenvolvimento() {
        assumeTrue("DEV".equals(System.getenv("ENV")),
            "Teste ignorado porque não está no ambiente de desenvolvimento");
        // Código do teste que deve ser executado apenas no ambiente de desenvolvimento
    }
}
```
- 2. assumeFalse:

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assumptions.*;

public class AssumptionsTest {

    @Test
    void testIgnoradoEmAmbienteDeProdução() {
        assumeFalse("PROD".equals(System.getenv("ENV")),
            "Teste ignorado porque está no ambiente de produção");
        // Código do teste que não deve ser executado no ambiente de produção
    }
}
```
- 3. assumingThat:

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assumptions.*;
import static org.junit.jupiter.api.Assertions.*;

public class AssumptionsTest {

    @Test
    void testExecutarParteCondicional() {
        String ambiente = System.getenv("ENV");
        assumingThat("DEV".equals(ambiente),
            () -> {
                // Código que só será executado se a condição for verdadeira
                assertEquals(2, 1 + 1);
            });
        // Código que será executado independentemente da condição
        assertTrue(3 > 2);
    }
}
```

## Ordenação de Testes
Em algumas situações, pode ser necessário garantir que os testes sejam executados em uma ordem específica. Por padrão, JUnit 5 não garante a ordem de execução dos testes, já que cada teste deve ser independente e não depender de outro para seus resultados. No entanto, JUnit 5 oferece mecanismos para ordenar os testes quando necessário.

Como Ordenar Testes
JUnit 5 fornece a anotação ```@TestMethodOrder``` para especificar a ordem de execução dos testes. Aqui estão as principais maneiras de ordenar testes:

Alfabética (Nome dos Métodos)
Order Anotação
Ordem Personalizada (Classe de Ordenação Personalizada)
- 1. Ordem Alfabética
A ordem alfabética usa o nome dos métodos para determinar a sequência de execução dos testes.

```java
import org.junit.jupiter.api.*;

@TestMethodOrder(MethodOrderer.Alphanumeric.class)
public class TestesOrdenados {

    @Test
    void testeB() {
        System.out.println("Executando teste B");
    }

    @Test
    void testeA() {
        System.out.println("Executando teste A");
    }

    @Test
    void testeC() {
        System.out.println("Executando teste C");
    }
}
```
- 2. Ordem Usando @Order
Você pode usar a anotação @Order para especificar explicitamente a ordem dos testes.

```java
import org.junit.jupiter.api.*;

@TestMethodOrder(MethodOrderer.OrderAnnotation.class)
public class TestesOrdenados {

    @Test
    @Order(2)
    void testeB() {
        System.out.println("Executando teste B");
    }

    @Test
    @Order(1)
    void testeA() {
        System.out.println("Executando teste A");
    }

    @Test
    @Order(3)
    void testeC() {
        System.out.println("Executando teste C");
    }
}
```
- 1. Ordem Personalizada
Você pode definir uma classe de ordenação personalizada implementando a interface MethodOrderer.

```java
import org.junit.jupiter.api.*;
import org.junit.jupiter.api.MethodOrderer.OrderAnnotation;
import org.junit.jupiter.api.MethodOrdererContext;

import java.lang.reflect.Method;
import java.util.List;

@TestMethodOrder(CustomOrderer.class)
public class TestesOrdenados {

    @Test
    void testeB() {
        System.out.println("Executando teste B");
    }

    @Test
    void testeA() {
        System.out.println("Executando teste A");
    }

    @Test
    void testeC() {
        System.out.println("Executando teste C");
    }
}

class CustomOrderer implements MethodOrderer {
    @Override
    public void orderMethods(MethodOrdererContext context) {
        List<Method> methods = context.getMethodDescriptors().stream()
                .map(MethodDescriptor::getMethod)
                .sorted((m1, m2) -> {
                    if (m1.getName().equals("testeA")) return -1;
                    if (m2.getName().equals("testeA")) return 1;
                    return m1.getName().compareTo(m2.getName());
                })
                .toList();
        context.getMethodDescriptors().sort((md1, md2) -> methods.indexOf(md1.getMethod()) - methods.indexOf(md2.getMethod()));
    }
}
```