
## Setup graphql server project
```
npm init

npm install apollo-server graphql
```

代码的核心是一个 ApolloServer
```
const server = new ApolloServer({
  typeDefs,
  resolvers,
})
```
第一个参数 typeDefs 包含 GraphQL 模式。

第二个参数是一个对象，它包含服务器的解析器

解析器定义了GraphQL 查询的响应方式:
```
const resolvers = {
  Query: {
    personCount: () => persons.length,
    allPersons: () => persons,
    findPerson: (root, args) =>
      persons.find(p => p.name === args.name)
  }
}
```
解析器对应于模式中描述的查询。
```
type Query {
  personCount: Int!
  allPersons: [Person!]!
  findPerson(name: String!): Person
}
```

## GraphQL-playground

当 Apollo-server 在开发模式(node filename.js)下运行时，
启动一个GraphQL-playground at http://localhost:4000/graphql

query
```
query {
  findPerson(name: "Arto Hellas") {
    phone 
    city 
    street
  }
}
```