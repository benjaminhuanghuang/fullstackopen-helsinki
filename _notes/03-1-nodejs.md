## Node.js + Express

```
npm install express

npm install --save-dev nodemon
```

^4.17.1 前面的插入符号表示，当项目的依赖项更新时，安装的 express 版本至少为 4.17.1。 但是，所安装的 express 版本也可以具有较大的patch 号(最后一个数字)或较大的minor 号(中间的数字)的版本。 第一个major 号表示库的主版本必须相同。


Add script
```
"scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js",
  },
```

## The Visual Studio Code REST client
在project的根目录创建requests 目录。 将所有 REST request保存为以 .rest结尾的文件

```
```

## middleware
中间件是可用于处理请求和响应对象的函数。

比如 json-parser 从请求对象中存储的请求中获取原始数据，将其解析为一个 JavaScript 对象，并将其作为一个新的属性、body 分配给请求对象。

有多个middleware的时候，将按照他们被使用的顺序，一个接一个地执行。

```
const requestLogger = (request, response, next) => {
  console.log('Method:', request.method)
  console.log('Path:  ', request.path)
  console.log('Body:  ', request.body)
  console.log('---')
  next()
}
```

中间件是这样使用的:
```
app.use(requestLogger)
```
注意，json-parser 要在 requestLogger 之前使用的，否则在执行requestLogger时， request.body 还不存在


## CORS
可以从浏览器和Postman访问后端，没有任何问题

默认情况下，运行在浏览器应用的 JavaScript 代码只能与相同 源的服务器通信。

因为我们的服务器位于本地主机端口3001，而我们的前端位于本地主机端口3000，所以它们不具有相同的源。

请记住，同源策略和 CORS 并不是特定于 React 或 Node 的。 它们实际上是 web 应用操作的通用原则。

可以通过使用 Node 的cors 中间件来允许来自其他源的请求。

Install cors
```
  npm install cors
```
使用中间件并允许来自所有来源的请求:
```
  const cors = require('cors')

  app.use(cors())
```

## Deploy to Heroku
向项目的根目录添加一个名为 Procfile的文件，告诉 Heroku 如何启动应用。
```
  web: npm start
```

更改应用在index.js 文件底部使用的端口:
```
const PORT = process.env.PORT || 3001
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`)
})
```
Heroku 会在环境变量的基础上配置应用端口。

Deploy
```
  heroku create   # 创建一个 Heroku 应用
  git push Heroku master  # 将代码提交到仓库并将其推送到Heroku

  heroku logs
```


## Deploy front end

将 build 目录复制到后端project的根目录，并配置后端以显示前端的 main page ( build/index.html)作为其主页。
```
  cp -r build ../../backend
```
为了让 express 显示 static content、 页面 index.html 和它用来fetch的 JavaScript 等等，我们需要一个来自 express 的内置中间件，称为static。
```
  app.use(express.static('build'))
```
每当 express 收到一个 HTTP GET 请求时，它都会首先检查build 目录是否包含与请求地址对应的文件。 如果找到正确的文件，express 将返回该文件。

此时，前端和后端都在同一个地址，所以我们可以声明 baseUrl 为relative URL。 意味着可以省略声明服务器的部分。
```
import axios from 'axios'
const baseUrl = '/api/notes'     // relative URL    
```

为了在没有额外手工工作的情况下创建前端的新的生产构建，在后端存储库的package.json 中添加一些 npm-scripts:
```
{
  "scripts": {
    "build:ui": "rm -rf build && cd ../../front-end && npm run build --prod && cp -r build ../../backend/",
    "deploy": "git push heroku master",
    "deploy:full": "npm run build:ui && git add . && git commit -m uibuild && npm run deploy",    
    "logs:prod": "heroku logs --tail"
  }
}
```
由于在front end使用了relative URL  
```
  const baseUrl = '/api/notes'     // relative URL 
```
将导致不能再在开发模式下工作(当使用命令 npm start 启动时) ，
前端位于地址localhost: 3000，所以对后端的请求会发送到错误的地址localhost:3000/api/notes。 而后端位于localhost: 3001

如果这个项目是用 create-react-app 创建的，那么这个问题很容易解决。 将如下声明添加到前端仓库的package.json 文件中就足够了。

{
  "dependencies": {
    // ...
  },
  "scripts": {
    // ...
  },
  "proxy": "http://localhost:3001"
}
在重新启动之后，React 开发环境将作为一个代理工作。
如果 React 代码对服务器地址http://localhost:3000发出了一个 HTTP 请求，而不是 React 应用本身管理的地址(即当请求不是为了获取应用的 CSS 或 JavaScript) ，那么该请求将被重定向到 HTTP://localhost:3001 的服务器。


## Github
https://github.com/fullstack-hy2020/part3-notes-backend/tree/part3-3
https://github.com/fullstack-hy2020/part2-notes/tree/part3-1


## Debug node.js
- Method 1 :Visual Studio Code
可以配置你的 launch.json 文件来开始debug

- Method 2: Chrome dev tools

利用 Chrome 开发者控制台，通过如下命令启动应用，也可以进行调试:
```
  node --inspect index.js
```

