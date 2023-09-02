## GraphQL を Nest.js で実装する

```
nest new Graphql
pnpm i @nestjs/graphql @nestjs/apollo @apollo/server graphql
```

## GraphQL の参考記事などなど

- [Nest.js GraphQL 公式](https://docs.nestjs.com/graphql/quick-start)
- [GraphQL 公式](https://graphql.org/)
- [APOLLO 公式](https://www.apollographql.com/)
- [GraphQL VS REST](https://www.apollographql.com/blog/graphql/basics/graphql-vs-rest/)
- [GraphQL とは何でしょうか。](https://hasura.io/learn/ja/graphql/intro-graphql/what-is-graphql/)

## GraphQL の用語集

- Query...クライアントがサーバーに対して行うデータの要求。必要なデータだけを指定する。

```graphql
例：IDが1のユーザのname, emailフィールドのみを要求する

query {
  user(id: 1) {
    name
    email
  }
}
```

- Schema...サーバーが提供する型とそのデータに対する操作（クエリとミューテーション）を定義する。
  - Schema の要素
    - Types:データの型
    - Queries:読み取り操作。何をリクエストできるか指定する。
    - Mutations:書き込み操作。データの追加、更新、削除など。
    - Subscriptions:データのリアルタイム更新を受け取るための操作。

```graphql
例：User型に対してのQueryとMutationができること。
type User {
  id: ID!
  name: String!
  email: String!
}
type Query {
  user(id: ID): User
}
type Mutation {
  createUser(name: String!, email: String!): User
}
```

- Resolver...
