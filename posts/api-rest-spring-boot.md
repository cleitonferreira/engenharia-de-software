![](https://www.astera.com/wp-content/uploads/2020/01/rest.png)
# REST API no Spring Boot
REST (Representational State Transfer)
REST é um estilo de arquitetura para sistemas distribuídos, como a web. Ele foi introduzido por Roy Fielding em sua tese de doutorado em 2000. REST utiliza o protocolo HTTP e princípios simples para a comunicação entre clientes e servidores. As principais características do REST são:

- Stateless: Cada requisição do cliente para o servidor deve conter todas as informações necessárias para entender e processar a requisição.
- Cacheable: Respostas podem ser armazenadas em cache para melhorar a performance.
- Client-Server: Separação de responsabilidades entre cliente e servidor.
- Uniform Interface: Interface uniforme para comunicação entre cliente e servidor.
- RESTful: É um adjetivo que descreve APIs que aderem aos princípios do REST. Se uma API é RESTful, ela segue os princípios de REST, usando métodos HTTP padrão como GET, POST, PUT, DELETE para realizar operações CRUD (Create, Read, Update, Delete).

## REST API
Uma REST API (Application Programming Interface) é uma interface de programação que segue os princípios REST. Ela permite que diferentes sistemas se comuniquem pela web de forma simples e eficiente. As operações em uma REST API são feitas usando os métodos HTTP:

- GET: Recupera dados do servidor.
- POST: Envia dados ao servidor para criar um novo recurso.
- PUT: Atualiza um recurso existente no servidor.
- DELETE: Remove um recurso do servidor.

## Como Usar REST API com Spring Boot
Spring Boot é um framework que facilita a criação de aplicações Java, incluindo REST APIs. Ele fornece várias ferramentas e convenções que permitem construir APIs de forma rápida e eficiente.

1. Configuração do Projeto
Primeiro, você precisa criar um novo projeto Spring Boot. Você pode usar o Spring Initializr para gerar o esqueleto do projeto. Inclua as seguintes dependências:

Spring Web
Spring Boot DevTools (opcional, para desenvolvimento)

### Anotações Mais Utilizadas
- ``@RestController``
A anotação ``@RestController`` combina as anotações @Controller e @ResponseBody. Ela é usada para definir uma classe como um controlador REST, o que significa que cada método em um @RestController retorna diretamente um objeto serializado em JSON (ou XML, dependendo da configuração).

- ``@RequestMapping``
A anotação ``@RequestMapping`` é usada para mapear solicitações HTTP para métodos específicos dentro de um controlador.


- ``@GetMapping``, ``@PostMapping``, ``@PutMapping``, ``@DeleteMapping``
Essas anotações são usadas para mapear métodos específicos para operações HTTP GET, POST, PUT e DELETE, respectivamente.

- ``@PathVariable``
A anotação ``@PathVariable`` é usada para vincular variáveis de caminho de URL aos parâmetros do método em um controlador REST.

- ``@RequestBody``
A anotação @RequestBody é usada para vincular o corpo da solicitação HTTP a um objeto Java.

Exemplo:

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @GetMapping("/{id}")
    public User getUserById(@PathVariable Long id) {
        // Retorna um usuário por ID
    }

    @PostMapping
    public User createUser(@RequestBody User user) {
        // Cria um novo usuário
    }

    @PutMapping("/{id}")
    public User updateUser(@PathVariable Long id, @RequestBody User user) {
        // Atualiza um usuário existente
    }

    @DeleteMapping("/{id}")
    public void deleteUser(@PathVariable Long id) {
        // Deleta um usuário por ID
    }
}
```
