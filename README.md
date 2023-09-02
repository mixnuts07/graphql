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

- Query...クライアントがサーバーに対して行うデータの要求。必要なデータだけを指定する。クライアント側で定義。

```graphql
例：IDが1のユーザのname, emailフィールドのみを要求する

query {
  user(id: 1) {
    name
    email
  }
}
```

- Fragment...クエリ内で再利用可能な単位。クエリの短縮・簡略化。クライアント側で定義。

```graphql
fragment userData on User {
  id
  name
  email
}

query {
  user1: user(id: 1) {
    ...userData
  }
  user2: user(id: 2) {
    ...userData
  }
}
```

- Directive..クエリやフィールド、型などに対して特別な操作を加える指示を表す。 **＠** マークで始まる。

```graphql
query(@includeEmail: Boolean!) {
  user(id: 1) {
    id
    name
    email @include(if: @includeEmail)
  }
}
```

- Schema...サーバーが提供する型とそのデータに対する操作（クエリとミューテーション）を定義する。サーバー側で定義。
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

- Resolver...具体的なデータソース（DB,API,キャッシュ etc）からデータを取得するための関数。スキーマの型に従ってデータを解消する。サーバー側で定義。
