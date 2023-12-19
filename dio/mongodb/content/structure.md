<h1> Estrutura e modelagem de dados no MongoDB </h1>

<h2> Sumário </h2>

- [Estrutura do MongoDB](#estrutura-do-mongodb)
- [Modelagem de Dados no MongoDB](#modelagem-de-dados-no-mongodb)

## Estrutura do MongoDB

![Estrutura do MongoDB](../assets/mongodb-structure.PNG)

A estrutura do banco de dados do MongoDB é composta da seguinte forma:

- **Banco de dados:** podemos dizer que é a instância do banco de dados em si
- **Coleções:** São como as tabelas, são um agrupamento lógico de documentos, não exigindo um esquema pré-definido
- **Documentos:** São como os registros, são armazenados em documentos BSON (estruturas flexíveis e semiestruturadas) composta de campos (que são pares de chaves e valores)
  - Cada documento possui um identificador único chamado "_id"
  - Tamanho máximo de 16 MB
  - Pode haver aninhamento de documentos (Embedded Data)
- **Campos (Fields)**: são as **propriedades** do documentos, feitas dos pares de chaves e valor

Os tipos de dados simples são: String, Number, Boolean, Date, Null e ObjectId
Os tipos de dados complexos são: Array, Embedded Document, Reference e GeoJson

Exemplo de Documento:

```json
{
  "user": {
    "username": "John Doe",
    "email": "email@email.com",
    "address": {
      "street": "2323 Example Street",
      "city": "Sao Paulo",
      "state": "SP"
    }
  }
}
```

## Modelagem de Dados no MongoDB

- A modelagem de dados no MongoDB deve ser orientada pelas consultas (query) que serão realizadas com mais frequência
- É comum **desnormalizar** os dados, para evitar operações de junção (joins no SQL) custosas. Ou seja, os dados relacionados poem ser armazenados juntos em um único **document**, em vez e serem distribuídos em várias coleções.
