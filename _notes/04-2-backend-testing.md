## Node.js project structure best practices 

```
 npm install --save-dev jest  
```

npm script
```
{
  "scripts": {
    ...
    "test": "jest --verbose"
  },
}
```
-t 选项可用于运行具有特定名称的测试:
```
npm test -- -t 'a specific note is within the returned notes'
```

jest.config.js

For backend testing, Jest 需要指定执行环境为 Node
```
  module.exports = {
    testEnvironment: 'node',
};
```

## Test environment
Node project 使用 NODE_ENV 环境变量定义应用的执行模式
当backend project在 Heroku 运行时，它处于 production 模式

修改package.json，在运行测试时，传入NODE_ENV
```
  "scripts": {
    ...
    "start": "NODE_ENV=production node index.js",
    "dev": "NODE_ENV=development nodemon index.js",
    "test": "NODE_ENV=test jest --verbose --runInBand"
  },
```
runInBand选项防止 Jest 并行运行测试; 用于测试数据库

在脚本中指定应用模式的方式不能在 Windows 上工作。 
可以通过如下命令安装cross-env作为一个开发依赖包，来纠正这个问题:
```
  npm install --save-dev cross-env
```
在package.json npm 脚本中使用跨平台兼容性的 cross-env
```
{
  // ...
  "scripts": {
    "start": "cross-env NODE_ENV=production node index.js",
    "dev": "cross-env NODE_ENV=development nodemon index.js",
    // ...
    "test": "cross-env NODE_ENV=test jest --verbose --runInBand",
  },
  // ...
}
```

## 针对不同的环境使用不同的database
在多人开发同一个应用的情况下, 最好使用安装并运行在开发人员本地机器上的数据库来运行我们的测试。 
最佳的解决方案是让每个测试用例执行时使用自己独立的数据库。 
通过运行内存中的 Mongo或使用Docker容器来实现。 
此处继续使用 MongoDB Atlas 数据库

在 .env 文件中，为开发和测试数据库的数据库地址分别设置变量

在代码中根据环境变量使用不同的database
```
if (process.env.NODE_ENV === 'test') {
  MONGODB_URI = process.env.TEST_MONGODB_URI
}
```

## supertest for API test
```
npm install --save-dev supertest
```
