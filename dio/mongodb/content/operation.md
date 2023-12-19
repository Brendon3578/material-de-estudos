# Operações no MongoDB

## Criando um Banco de Dados e uma Collection

Tecnicamente não existe um comando pré-definido de "criação" de banco de dados. Para essa operação usa-se o comando `use <db_name>`, no qual é alterado o banco de dados que está sendo usado atualmente. Por exemplo:

```bash
use viagens_db
```

Para criar uma collection usa-se o comando `db.createCollection("collection_name")`

```bash
db.createCollection("usuarios")
```

## Inserção de documentos

Para a inserção de documentos dentro de uma collection usa-se o comando `db.nome_collection.insertOne({})`, para a inserção de vários documentos usa-se o comando `db.nome_collection.insertMany([{}])`. Por exemplo:

```bash
db.usuarios.insertOne({
  "name": "John Doe",
  "email": "john@email.com"
})
```

É criado então dentro do MongoDB o seguinte documento:

```json
{
  "_id": {
    "$oid": "65809e7556ad0a7b69b0ad6b" // ObjectId
  },
  "name": "John Doe",
  "email": "john@email.com"
}
```

Para a inserção de vários documentos utiliza-se o comando insertMany em vez do insertOne, no qual é passado como um parâmetro um array de vários documentos

```bash

db.usuarios.insertMany([
  {
    "name": "John Doe",
    "email": "john@email.com"
  },
  {
  "name": "Jane Doe",
  "email": "jane@email.com"
  }
]);
```

## Consulta de documentos

> A documentação do MongoDB disponibiliza vários bancos de dados para serem testados livremente, [clique aqui para abrir o link da documentação](https://www.mongodb.com/docs/atlas/sample-data/). As consultas abaixo serão aplicadas nesse banco de dados

É possível utilizar os seguintes comandos do MongoDB para fazer a consulta de documentos, dentro das chaves é inserido os parâmetros de consulta do MongoDB:

- `db.movies.find({})`: consultar todos os documentos
- `db.movies.findOne({})`: consultar e retornar apenas um documento
- `db.movies.findOneAndUpdate({})`: será consultado e será atualizado o documento
- `db.movies.findOneAndDelete({})`: será consultado e será apagado o documento

```bash
# Procurar por todos os filmes lançados
db.movies.find({})
```

### Operadores de Comparação de consultas

Para fazer consultas que compara determinados valores aos documentos, utiliza-se operadores de comparação:

- `$ne` (*not equals* - **diferente**)
- `$gt` (*greater than* - **maior que**),
- `$lt` (*lower than* - **menor que**),
- `$gte` (*greater than or equals* - **maior ou igual a**),
- `$lte` (*lower than or equals* - **menor ou igual a**),
- `$in` (*in an array* - **pertence a uma lista**):
- `$nin` (*not in an array* - **não pertence a uma lista**),

Por exemplo:

```shell
# definir o banco de dados que será utilizado
use sample_mflix

# retornar todos os filmes que têm o idioma "Português", a data dde lançamento seja 2003 ou 2004 e
# que foi seja um filme brasileiro (veja a imagem do resultado abaixo)
db.movies.find({
  languages: "Portuguese",
  year: {$in: [2003, 2004]},
  countries: {$eq: "Brazil"}
})
```

![Imagem da query executada](../assets/example-of-return.PNG)

### Operadores Lógicos de consultas

Para fazer consultas filtrando através de condições definidas, é utilizado operadores lógicos:

- `$and`: filtrar por várias condições
- `$or`: filtrar por possíveis condições
- `$not`: filtrar por nenhuma condição definida

Para a consulta filtrada por várias condições

## Exclusão de Documentos

Para remover documentos no MongoDB usa-se os comandos `db.usuarios.deleteOne({<critérios>})` ou o `db.usuarios.deleteMany({})`.

## Bibliografia

- [Operadores de Comparação de Consulta - MongoDB](https://www.mongodb.com/docs/manual/reference/operator/query-comparison/)
- [Consultando e Filtrando dados - MongoDB](https://www.mongodb.com/docs/compass/current/query/filter/?utm_source=compass&utm_medium=product#match-by-multiple-conditions---and-)
