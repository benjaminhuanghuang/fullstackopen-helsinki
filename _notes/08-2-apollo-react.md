## Postman

GraphQl的工作原理是向 http://localhost:4000/graphql 发送 POST 请求

query是一个字符串
```
{
  "query": "query {allPerson{name} }"
}
```


## Client 
理论上可以使用 Axios 来处理 React-app 和 GraphQl 之间的通信。

Facebook 的 Relay 和 Apollo Client 提供了更好的功能。

```
npm install @apollo/client graphql
```

