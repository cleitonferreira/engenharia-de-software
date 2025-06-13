# Generics
### O que são Generics em Java?
Generics são uma funcionalidade do Java que permite a definição de classes, interfaces e métodos com tipos de dados genéricos. Isso significa que você pode criar uma estrutura que pode operar com diferentes tipos de dados, sem a necessidade de especificar o tipo exato de dado no momento da criação.

- Declaração de Generics: Você declara um generic com o uso de chaves angulares <>, onde você coloca um tipo de parâmetro, como T. Por exemplo, ArrayList<T> pode armazenar qualquer tipo de objeto.
- Benefícios: Generics proporcionam segurança de tipo e reduzem a necessidade de conversões de tipo (casting), o que pode evitar erros em tempo de execução.
- Uso com Coleções: Um dos usos mais comuns de Generics é com as coleções do Java, como List, Set e Map, permitindo que você especifique o tipo de objetos que eles podem conter.

## Exemplos
```java
// Uma classe genérica simples
public class Caixa<T> {
    private T conteudo;

    public void setConteudo(T conteudo) {
        this.conteudo = conteudo;
    }

    public T getConteudo() { return conteudo; }
}
```