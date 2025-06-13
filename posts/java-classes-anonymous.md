# Classes Anônimas
## O que são Classes Anônimas?
Classes anônimas em Java são classes sem nome definidas e instanciadas em uma única expressão. Elas são úteis para criar rapidamente uma implementação de uma interface ou classe abstrata sem a necessidade de definir uma nova classe explicitamente.

## Exemplo
Classe Anônima com Runnable
```java
public class ExemploClasseAnonima {
    public static void main(String[] args) {
        // Criando uma classe anônima que implementa Runnable
        Runnable executavel = new Runnable() {
            @Override
            public void run() {
                System.out.println("Executando classe anônima com Runnable!");
            }
        };
        
        // Executar o método run da classe anônima
        executavel.run();
    }
}
```
Explicação
Definição da Classe Anônima:

```java
Runnable executavel = new Runnable() {
    @Override
    public void run() {
        System.out.println("Executando classe anônima com Runnable!");
    }
};
```
Aqui, criamos uma classe anônima que implementa a interface Runnable. Implementamos o método run para que ele imprima uma mensagem no console.

Execução da Classe Anônima:

```java
executavel.run();
```
Chamamos o método run da instância da classe anônima para executar o código definido no método run.