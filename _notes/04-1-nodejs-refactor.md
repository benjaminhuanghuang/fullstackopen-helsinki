## Node.js project structure best practices 

```
  ├── index.js
  ├── app.js
  ├── build
  │   └── ...
  ├── controllers
  │   └── notes.js
  ├── models
  │   └── note.js
  ├── package-lock.json
  ├── package.json
  ├── utils
  │   ├── config.js
  │   ├── logger.js
  │   └── middleware.js  
```

## Router
old version
```
  app.delete('/api/notes/:id', (request, response) => {
```
new version with router
```
  notesRouter.delete('/:id', (request, response) => {
```
A router object is an isolated instance of middleware and routes. 
You can think of it as a "mini-application," capable only of performing middleware and routing functions. 
Every Express application has a built-in app router.
路由实际上是一个中间件，可用于在某个位置定义“相关路由” ，通常放置在单独的模块中。

app.js 是一个创建实际应用的文件，对路由对象使用use方法，按如下方式使用:
```
  const notesRouter = require('./controllers/notes')
  app.use('/api/notes', notesRouter)
```
如果请求的 URL 以 /api/notes开头，则会使用之前定义的路由。 因此，notesRouter 只定义路由的相对部分，即空路径/或仅仅定义参数/:id


