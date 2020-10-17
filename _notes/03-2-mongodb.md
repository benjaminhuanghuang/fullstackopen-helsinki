## Create db
MongoDB Atlas -> Create a Starter Cluster

使用database access 为数据库创建 user
Security -> Database Access -> Add New Database User -> give username and password -> give User Privileges "Read and write to any database"


定义允许访问数据库的 IP 地址
Security -> Network Access -> Allow access from anywhere


Get connect strings
Clusters -> Connect -> Connect your application

```
mongodb+srv://fullstack:<password>@cluster0.49erl.mongodb.net/<dbname>?retryWrites=true&w=majority
```

Change Database Name
通过修改 URI，将<dbname>更改为note-app:
```
  mongodb+srv://fullstack:<password>@cluster0.49erl.mongodb.net/note-app?retryWrites=true&w=majority
```


## Mongoose

Mongoose is object document mapper (ODM) ，helpful to convert JavaScript object to  Mongo Document

```
npm install mongoose
```
Mongoose 对象的 id 属性看起来像一个字符串，但实际上它是一个对象

## schema
```
  const noteSchema = new mongoose.Schema({
    content: String,
    date: Date,
    important: Boolean,
  })

  const Note = mongoose.model('Note', noteSchema)
```