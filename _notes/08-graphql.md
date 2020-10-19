 
 RESR 是基于资源的。 
 每个资源(例如user, blog)都有自己的URL来标识，例如/users/10。 
 对资源所做的所有操作都是通过对其 URL 的 HTTP 请求来完成的。 操作取决于所使用的 http method


 REST API，可能必须从浏览器执行多个 http 请求。 这些请求还会返回大量不必要的数据，而且浏览器上的代码可能会相当复杂。

 Graphql 的主要原理是，浏览器上的代码形成一个query，描述需要的数据，并通过 HTTP POST 请求将其发送给 API。 
 与 REST 不同，所有 GraphQL 查询都发送到相同的地址，它们的类型是 POST。


 所有 GraphQL 应用的核心是一个schema ，它描述了客户端和服务器之间发送的数据