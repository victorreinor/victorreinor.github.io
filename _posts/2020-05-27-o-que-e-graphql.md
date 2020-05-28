---
title: "O que é GraphQl?"
published: true
---
É uma linguagem de consulta de dados em API's desenvolvida pelo facebook.
As consultas são interpretadas em tempo de execução no servidor usando um sistema de tipos que é definido para seus dados.

- Permite o client especificar exatamente os dados de pesquisa;
  - Quando consultamos API's geralmente é retornado muitos campos e na maioria das vezes se torna inúteis, com GraphQl ele permite que retornemos campos específicos, ou seja, pedimos para nosso backend o que é necessário com isso é otimizado a quantidade de tráfego do servidor para o client;
- Facilita buscar dados de várias fontes (vários bancos, outras API's, sistemas legados);
- Usa sistema de tipos para definir dados;
  
GraphQl não está vinculado a nenhum tipo de banco de dados.

### Conceitos Básicos
----

- **Type System:** Sistema de tipos que usamos para descrever nossos dados;
- **Queries:** Obtém dados da nossa API (read, **leitura de dados**);
- **Mutations:** Faz alterações nos dados da nossa api (write, **criar/alterar/deletar dados da nossa API**);
- **Subscriptions:** Permite ouvir mudanças em "tempo real" (real-time, **conseguimos ouvir mudanças em tempo real dos dados**);
- **Schema:** Define o "Esquema" da nossa API, um container para todos os tipos da nossa API, dentro do **Schema** é aonde que teremos todas nossas **Queries, Mutations, Subscriptions** e quando definimos toda a nossa estrutura da nossa API chamamos de (GraphQL Schema Definition - SDL);

### Type System
----
GraphQL tem seu próprio sistema de tipos para que possamos descrever dados para nossa API.

Veja abaixo alguns exemplos de tipagem no GraphQL.

```javascript
  type User {
    id: ID!,
    name: String!,
    email: String!,
    password: String!
  },

  type Chat {
    id: ID!,
    messages: [Message!]!,
    users: [User!]!,
    title: String,
    createdAt: DateTime!,
    isGroup: Boolean!
  },

  type Message {
    id: ID!,
    text: String!,
    createdAt: DateTime!,
    sender: User!,
    chat: Chat!
  }
```

Sempre começamos a tipagem com a palavra reservada **type** e em seguida o nome do tipo que queremos criar, nos exemplos acima foram criadas User, Chat e Message. 
Muito semelhante com um objeto em **javascript**, passamos os campos que teremos e seus respectivos tipos de cada campo.

Quando adicionado **!** (exclamação) na frente do campo significa que o campo é obrigatório.

Vejamos que no type Chat passamos como array, significa que teremos uma lista que foi criada a tipagem, neste exemplo temos duas exclamações **[User!]!**, a exclamação de fora do colchetes define que quando nao tivermos nenhuma mensagem para esse **User** é necessário retornar um array vazio **[ ]** e a de dentro significa que quando tivermos a mensagem os valores não podem ser nulos e seguem a tipagem que foi definida.

### Queries
----
Queries são o que usamos para buscar dados da nossa API.

Siga os exemplos abaixo para explicação (Analogia método GET do REST).

**[Exemplo 1]** Definição da Query.
```javascript
  type Query {
    allUsers: [User!]!
  }
```

Definimos a **query** que seria o root, aonde colocaremos todas as querys ali dentro.

No exemplo criamos uma query chamada **allUsers** que devolverá um listagem de usuários.

**[Exemplo 2]** Requisição no client.
```javascript
  {
    query {
      allUsers {
        name
        email
      }
    }
  }
```

Neste exemplo simulamos uma busca do front-end.

Buscamos a query AllUsers e pedimos para ela nos retornar somente o campo name e email da listagem de usuários.

**[Exemplo 3]** JSON retornado para o client.
```javascript
  {
    "data": {
      "allUsers": [
        { 
          "name": "Jon",
          "email": "jon@email.com"
        },
        ...
      ]
    }
  }
```

### Resolver
----
No GraphQL toda **query** ou **mutations** precisamos de um **resolver**, que basicamente e aonde implementamos a lógica para buscar as informações desses campos.

No caso das queries os resolver são resolvidos de uma maneira assíncrona e as mutations uma após a outra.

Cada campo no GraphQL possui uma função **Resolver**.git remote add origin https://github.com/victorreinor/o-que-e-graphql.git
git push -u origin master

### Mutations
----
Nos permitem criar, alterar e deletar dados.

Siga os exemplos abaixo para explicação (Analogia ao POST, PUT, DELETE do REST).

**[Exemplo 1]** Definição da Mutation.
```javascript
  type Mutation {
    createUser(
      name: String!,
      email: String!
    ):User!
  }
```
Criamos a **mutation** e chamamos de **createUser**, passamos os campos que serão criados seguindo a tipagem definida.

**[Exemplo 2]** Requisição no client.
```javascript
  {
    mutation {
      createUser (
        name: "Victor",
        email: "victorreinor@gmail.com"
      ) {
        name
      }
    }
  }
```
Especificamos que é uma **mutation** e o nome da mutation, logo em seguida passamos os campos que serão inseridos.
No último parametro passamos **name** isso fara que quando a requisição for bem sucedida retornará somente o campo.

**[Exemplo 3]** JSON retornado para o front-end.
```javascript
  {
    "data": {
      "createUser": {
        "name": "Tyrion"
      }
    }
  }
```
Neste exemplo mostramos o exemplo após a inserção de dados do exemplo 2.

### Subscriptions
----
Permitem nos **"inscrever"** no servidor para receber alteração em tempo real (Web Sockets).

**[Exemplo 1]** Definição da Subscription.
```javascript
  type Subscription {
    Message(
      mutation_in: [
        MutationType!
      ]
    ): Message!
  }
```
Criamos a subscription **Message** e no parametro **mutation_in** passamos o parâmetro de como queremos ouvir essa subscription, podemos ouvir essa subscription na hora que a informação for criada/deletada/alterada.


**[Exemplo 2]** Requisição do client.
```javascript
  {
    subscription {
      Message (
        mutation_in: [CREATED]
      ) {
        title
        sender {
          name
        }
      }
    }
  }
```
Parecido com os outros exemplos, passamos como informação subscription, suscription que quer ser escutada e o momento que quer ser escutada, no exemplo acima passamos para escutar na criação

**[Exemplo 3]** JSON retornado para o front-end.
```javascript
  {
    "data": {
      "Message": {
        "title": "Hello GraphQL",
        "sender": {
          "name": "Victor Reinor"
        }
      }
    }
  }
```

Por fim o retorno de quando for disparado a subscription.

Observação: esse retorno sempre atualizará quando for disparado o evento

### Schema
----
Engloba nossas queries, mutations, subscriptions e etc...

**[Exemplo 1]** Definição do schema.
```javascript
  type Schema {
    query: Query
    mutation: Mutation
    subscription: Subscription
  }
```
