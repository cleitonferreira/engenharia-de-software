# Mockito

## O que é o Mockito e como usá-lo com JUnit?

Mockito é uma biblioteca popular de código aberto para testes unitários em Java. Ele permite criar objetos "mock" (simulados) para substituir componentes reais durante os testes. Isso facilita a escrita de testes isolados, ajudando a garantir que as unidades de código funcionem corretamente sem depender de outras partes do sistema.

## Vantagens do Mockito
- Facilidade de Uso: A API do Mockito é simples e intuitiva.
- Isolamento de Testes: Permite testar uma classe sem precisar de suas dependências reais.
- Verificação de Comportamento: É possível verificar se métodos foram chamados com parâmetros específicos.
- Flexibilidade: Simula comportamentos complexos e excepcionais.

#### Com usar:
- Adicionar Dependências: Certifique-se de adicionar as dependências do Mockito e do JUnit jupiter no seu pom.xml (para projetos Maven) ou build.gradle (para projetos Gradle).

Para Maven:

```xml
<!-- https://mvnrepository.com/artifact/org.mockito/mockito-core -->
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-core</artifactId>
    <version>5.12.0</version>
    <scope>test</scope>
</dependency>

<!-- https://mvnrepository.com/artifact/org.mockito/mockito-junit-jupiter -->
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-junit-jupiter</artifactId>
    <version>5.12.0</version>
    <scope>test</scope>
</dependency>


```
Para Gradle:

```groovy
// https://mvnrepository.com/artifact/org.mockito/mockito-core
testImplementation group: 'org.mockito', name: 'mockito-core', version: '5.12.0'

// https://mvnrepository.com/artifact/org.mockito/mockito-junit-jupiter
testImplementation group: 'org.mockito', name: 'mockito-junit-jupiter', version: '5.12.0'

```

## Principais Anotações do Mockito:

- ``@ExtendWith(MockitoExtension.class)``: Executa testes com suporte do Mockito no JUnit 5.

### ``@Mock``
A anotação @Mock é usada para criar um mock de uma classe ou interface. Isso permite simular o comportamento de objetos reais durante os testes.

Exemplo:

```java
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.Test;
import org.mockito.Mock;

import java.util.List;

public class MockitoMockAnnotationExample {

    @Mock
    private List<String> mockedList;

    @Test
    public void testMockedList() {
        // Define comportamento do mock
        when(mockedList.get(0)).thenReturn("Mockito");

        // Usa o mock
        String result = mockedList.get(0);

        // Verifica o resultado
        assertEquals("Mockito", result);
    }
}
```
Neste exemplo, mockedList é um mock da interface ``List<String>``. Quando o método ``get(0)`` é chamado no mock, ele retorna "Mockito", permitindo testar o comportamento do código que usa essa lista.

### ``@InjectMocks``
A anotação @InjectMocks é usada para injetar automaticamente mocks marcados com @Mock em uma instância da classe sob teste.

Exemplo:

```java
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;

import java.util.ArrayList;
import java.util.List;

public class MockitoInjectMocksAnnotationExample {

    @Mock
    private List<String> mockedList;

    @InjectMocks
    private ServiceUnderTest service;

    @Test
    public void testServiceMethod() {
        // Define comportamento do mock
        when(mockedList.get(0)).thenReturn("Mockito");

        // Chama método do serviço sob teste
        String result = service.processList();

        // Verifica o resultado do serviço
        assertEquals("Mockito", result);
    }

    // Classe de serviço sob teste
    class ServiceUnderTest {
        private List<String> list;

        ServiceUnderTest(List<String> list) {
            this.list = list;
        }

        public String processList() {
            return list.get(0);
        }
    }
}
```
Neste exemplo, mockedList é injetado automaticamente na classe ServiceUnderTest através da anotação @InjectMocks. O método processList() do serviço é testado usando o mock configurado.

### ``@Spy``
A anotação @Spy é usada para criar um "spy" (ou espião) de um objeto real. Um spy permite monitorar chamadas de método no objeto real e, opcionalmente, modificar seu comportamento.

Exemplo:

```java
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.Test;
import org.mockito.Spy;

import java.util.ArrayList;
import java.util.List;

public class MockitoSpyAnnotationExample {

    @Spy
    private List<String> spyList = new ArrayList<>();

    @Test
    public void testSpyList() {
        // Adiciona elemento à lista real usando o spy
        spyList.add("Mockito");

        // Verifica se o elemento foi adicionado
        assertEquals(1, spyList.size());

        // Define comportamento adicional do spy
        doReturn("Spy").when(spyList).get(0);

        // Usa o spy
        String result = spyList.get(0);

        // Verifica o resultado modificado
        assertEquals("Spy", result);
    }
}
```
Neste exemplo, spyList é um spy de uma ArrayList. Primeiro, um elemento é adicionado à lista real usando o spy. Depois, é modificado o comportamento do spy para retornar "Spy" ao invés do elemento adicionado.

### ``@Captor``
A anotação @Captor é usada para capturar argumentos de métodos para posterior verificação em testes.

Exemplo:

```java
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.Test;
import org.mockito.ArgumentCaptor;
import org.mockito.Captor;

import java.util.List;

public class MockitoCaptorAnnotationExample {

    @Captor
    private ArgumentCaptor<String> captor;

    @Test
    public void testListAddition() {
        List<String> mockedList = mock(List.class);

        // Executa método que adiciona um elemento à lista
        mockedList.add("Teste");

        // Captura o argumento passado para o método add()
        verify(mockedList).add(captor.capture());

        // Verifica o valor capturado
        assertEquals("Teste", captor.getValue());
    }
}
```
Neste exemplo, captor captura o argumento passado para o método add() de mockedList. O valor capturado é então verificado para garantir que corresponda ao esperado ("Teste").
