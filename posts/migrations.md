![](https://miro.medium.com/v2/resize:fit:363/1*Lr0qV2EIasIdF53nTqXzpw.png)
# Flyway Migrations com Spring Boot 

## Introdução
Manter o esquema do banco de dados sincronizado com a aplicação é um desafio contínuo no desenvolvimento de software. Uma maneira eficaz de gerenciar isso é através de migrations. Neste artigo, vamos explorar o conceito de migrations e como implementá-las usando Java, Spring Boot 3 e Flyway com Gradle.

## O Que São Migrations?
Migrations são uma série de scripts que permitem evoluir o esquema do banco de dados ao longo do tempo de forma controlada e reproduzível. Elas registram mudanças como criação de tabelas, modificação de colunas ou inserção de dados iniciais, garantindo que qualquer alteração no esquema do banco de dados seja rastreável e reversível.

## Benefícios das Migrations
- Controle de Versão: Cada mudança no banco de dados é versionada, facilitando o rastreamento do histórico de alterações.
- Automatização: Aplicar migrations pode ser automatizado durante o deploy, garantindo consistência.
- Colaboração: Em equipes, migrations garantem que todos os desenvolvedores trabalhem com o mesmo esquema de banco de dados.
- Reversibilidade: Migrations podem incluir scripts de reversão, permitindo desfazer alterações em caso de problemas.
- Flyway: Uma Ferramenta de Migrations
Flyway é uma ferramenta popular para gerenciar migrations de banco de dados em projetos Java. Ele aplica e rastreia mudanças no banco de dados usando scripts SQL ou Java.

## Configuração do Flyway com Spring Boot 3 e Gradle
Para configurar o Flyway em um projeto Spring Boot 3 usando Gradle, siga os passos abaixo:

### Adicionar Dependência do Flyway

Adicione a dependência do Flyway no arquivo build.gradle:

```groovy
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    implementation 'org.flywaydb:flyway-core'
    runtimeOnly 'org.postgresql:postgresql' // ou outro driver de banco de dados
}
```
### Configurar o Banco de Dados

Configure as propriedades do banco de dados no arquivo properties:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/meubanco
spring.datasource.username=usuario
spring.datasource.password=senha
spring.jpa.hibernate.ddl-auto=create
spring.flyway.enabled=true
```

ou .yml
```yml
spring:
    datasource:
        url: jdbc:postgresql://localhost:5432/meubanco
        username: usuario
        password: senha
spring:
    jpa: 
        hibernate:
            ddl-auto: create
    flyway:
        enabled: true
```


### Estrutura de Arquivos
Crie um diretório para armazenar seus scripts de migrations. Por padrão, Flyway procura por migrations no diretório src/main/resources/db/migration.

### Criação de Scripts de Migrations
Os scripts de migrations seguem uma convenção de nomenclatura para garantir a ordem de execução. Por exemplo:

- V1__Create_users_table.sql
- V2__Add_email_to_users.sql

Exemplo de um script de migration (V1__Create_users_table.sql):

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL
);
```
Exemplo de outro script de migration (V2__Add_email_to_users.sql):

```sql
ALTER TABLE users ADD COLUMN email VARCHAR(100) NOT NULL;
```

## Aplicando Migrations

Com a configuração acima, o Flyway aplicará automaticamente as migrations ao iniciar a aplicação. Não é necessário código adicional para iniciar o Flyway, pois a integração com Spring Boot gerencia isso automaticamente.

## Boas Práticas com Migrations
- Pequenas e Frequentes: Mantenha suas migrations pequenas e aplique-as frequentemente para evitar grandes mudanças que podem ser difíceis de reverter.
- Testes: Sempre teste suas migrations em um ambiente de desenvolvimento antes de aplicá-las em produção.
- Backup: Faça backup do banco de dados antes de aplicar novas migrations em produção.
- Descritividade: Use nomes descritivos para seus arquivos de migrations para facilitar a compreensão do histórico de mudanças.

## Conclusão
Migrations são uma parte essencial do desenvolvimento de software moderno, proporcionando uma maneira controlada e rastreável de gerenciar mudanças no esquema do banco de dados. Flyway é uma ferramenta poderosa que facilita a implementação de migrations em projetos Java com Spring Boot, garantindo que seu banco de dados esteja sempre em sincronia com sua aplicação. Adotar migrations e boas práticas associadas pode melhorar significativamente a manutenção e a evolução do seu banco de dados.