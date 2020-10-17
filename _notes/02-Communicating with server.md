
## local json server
install
```
npm install json-server --save-dev
```
Add npm script
```
"server": "json-server -p3001 --watch db.json"
```


## get data from server
- 所有现代浏览器都提供基于promise的fetch函数从服务器中获取数据

- axios
```
   npm install axios
```

Get-Create-Upate
```
import axios from 'axios'
const baseUrl = 'http://localhost:3001/notes'

const getAll = () => {
  const request = axios.get(baseUrl)
  return request.then(response => response.data)
}

const create = newObject => {
  const request = axios.post(baseUrl, newObject)
  return request.then(response => response.data)
}

const update = (id, newObject) => {
  const request = axios.put(`${baseUrl}/${id}`, newObject)
  return request.then(response => response.data)
}

export default { 
  getAll, 
  create, 
  update 
}
```

## Effect-hooks

```
  const hook = () => {
    axios
      .get('http://localhost:3001/notes')
      .then(response => {
        setNotes(response.data)
      })
  }

  useEffect(hook, [])
```
React 的 effect在渲染完成后会立即执行

useEffect的第二个参数用于指定effect运行的频率。 如果第二个参数是一个空数组 []，那么这个effect只在组件的第一次渲染时运行。

## use API key as environment variable
使用npx create-react-app ...创建了应用，并且想要为环境变量使用其他名称，则环境变量必须以REACT_APP_开头。

在项目中创建一个名为.env的文件并添加以下内容来使用'.env' 文件
```
# .env

REACT_APP_API_KEY=t0p53cr3t4p1k3yv4lu3
```
or add config to npm start script
```
REACT_APP_API_KEY='t0p53cr3t4p1k3yv4lu3' npm start 
```

Use config
```
const api_key = process.env.REACT_APP_API_KEY
```

