# NoSQL com MongoDB

<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/mongodb/mongodb-original-wordmark.svg" />
          

## O que é MongoDB?
MongoDB é um banco de dados NoSQL orientado a documentos, projetado para armazenar grandes volumes de dados não estruturados e semi-estruturados. Ele armazena dados em formato BSON (uma versão binária do JSON) e oferece escalabilidade horizontal, alta disponibilidade e flexibilidade na modelagem de dados.
## Na Prática
### Criando um Banco de Dados e uma Coleção

Criar um banco de dados e uma coleção para armazenar documentos.

```javascript
// Selecionar (ou criar) o banco de dados 'biblioteca'
use biblioteca

// Criar a coleção 'livros'
db.createCollection('livros')
```
### Inserindo Documentos na Coleção
inserir documentos JSON na coleção 'livros'.

```javascript
// Inserir um único documento
db.livros.insertOne({ titulo: "1984", autor: "George Orwell", ano: 1949 })

// Inserir múltiplos documentos
db.livros.insertMany([
  { titulo: "O Senhor dos Anéis", autor: "J.R.R. Tolkien", ano: 1954 },
  { titulo: "Dom Quixote", autor: "Miguel de Cervantes", ano: 1605 }
])
```
### Consultando Documentos
Realizar consultas básicas para recuperar documentos da coleção 'livros'.

```javascript
// Buscar todos os documentos
db.livros.find().pretty()

// Buscar documentos com um filtro
db.livros.find({ ano: { $gt: 1950 } }).pretty()
```
### Atualizando Documentos
Atualizar documentos na coleção.

```javascript
// Atualizar documentos onde o autor é 'George Orwell'
db.livros.updateOne(
  { autor: "George Orwell" },
  { $set: { ano: 1950 } }
)
```
### Excluindo Documentos
Excluir documentos da coleção.

```javascript
// Excluir documentos onde o ano é menor que 1950
db.livros.deleteMany({ ano: { $lt: 1950 } })
```