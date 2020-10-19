## Redux
在 Redux 中，状态存储在store中

状态复杂时，状态中的不同内容将被保存为store对象的不同字段


store的状态通过 actions改变。 Action 是对象，它至少有一个字段确定操作的类型。 例如
```
{
  type: 'INCREMENT'
}
```

Action 对应用程序状态的影响是通过使用一个 reducer() 函数来定义的。
reducer 以当前状态和 action 为参数, 并返回一个新的状态。

```
  const counterReducer = (state = 0, action) => {
    switch (action.type) {
      case 'INCREMENT':
        return state + 1
      case 'DECREMENT':
        return state - 1
      case 'ZERO':
        return 0
      default: // if none of the above matches, code comes here
      return state
    }
  }
```

Reducer 不能直接从应用程序中调用。 Reducer 只作为 createStore( )的参数

store 通过 dispatch() 把action分派 reducer中。
```
  store.dispatch({type: 'INCREMENT'})
```

store.getState() 可用于读取store的状态


store的第三个重要方法是subscribe()，创建回调函数。这些回调函数在store状态改变时被调用
```
store.subscribe(() => {
  const storeNow = store.getState()
  console.log(storeNow)
})
```

## Action creators
```
addNote = (event) => {
  event.preventDefault()
  const content = event.target.note.value
  event.target.note.value = ''
  store.dispatch({
    type: 'NEW_NOTE',
    data: {
      content,
      important: false,
      id: generateId()
    }
  })
}
```
App 组件不再需要知道任何关于 action 的内部表示，它只需要调用 creator-函数就可以获得正确的操作
```
const App = () => {
  const addNote = (event) => {
    event.preventDefault()
    const content = event.target.note.value
    event.target.note.value = ''
    store.dispatch(createNote(content))
    
  }
```


## Test
Instlldeep-freeze库 ，它可以用来确保 reducer 被正确定义为不可变函数。
```
npm install --save-dev deep-freeze
```
如果 reducer 使用 push 命令来操作state，那么测试将fail
