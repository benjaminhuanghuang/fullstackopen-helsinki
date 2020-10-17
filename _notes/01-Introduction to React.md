
## Array
push() method add a new item was added to the array

When using React, techniques from functional programming are often used. One characteristic of the functional programming paradigm is the use of immutable data structures.

```
const t = [1, -1, 3]

t.push(5)

const t2 = t.concat(5)
```

## Destructuring assignment
```
  const t = [1, 2, 3, 4, 5]

  const [first, second, ...rest] = t

  console.log(first, second)  // 1, 2 is printed
  console.log(rest)          // [3, 4 ,5] is printed

```
The variables first and second will receive the first two integers of the array as their values. 
The remaining integers are "collected" into an array of their own which is then assigned to the variable rest.


## this
```
const arto = {
  name: 'Arto Hellas',
  age: 35,
  education: 'PhD',
  greet: function() {
    console.log('hello, my name is ' + this.name)
  },
  doAddition: function(a, b) {
    console.log(a + b)
  },
}

arto.greet()       // "hello, my name is Arto Hellas" gets printed

const referenceToGreet = arto.greet
referenceToGreet() // prints "hello, my name is undefined"
```

有几种机制可以保留这种原始的 this 。 其中一个是使用bind方法:
```
setTimeout(arto.greet.bind(arto), 1000)
```
调用 arto.greet.bind(arto) 创建了一个新函数，它将 this 绑定指向到了 Arto，这与方法的调用位置和方式无关。

## page re-render
```
const refresh = () => {
  ReactDOM.render(<App counter={counter} />, 
  document.getElementById('root'))
}

setInterval(() => {
  refresh()
  counter += 1
}, 1000)
```
ReactDOM.render() 并不是re-render组件的推荐方法, 只是为了展示内部机制

## useState
```
const App = () => {
  const [ counter, setCounter ] = useState(0)

  setTimeout(
    () => setCounter(counter + 1),
    1000
  )

  console.log('rendering...', counter)

  return (
    <div>{counter}</div>
  )
}
```
每次 setCounter 修改状态时，它都会导致组件重新渲染。 状态的值将在一秒钟后再次递增，并且在应用运行期间循环往复。

! 不能从循环、条件表达式或任何不是定义组件的函数的地方调用 useState 

## React 中状态不可直接修改的原则
Bad:
```
const handleLeftClick = () => {
  clicks.left++             // X
  setClicks(clicks)     

  allClicks.push('L')       // X
  setAll(allClicks)
}
```
Good:
```
  const handleLeftClick = () => {
    setClicks({ ...clicks, left: clicks.left + 1 })
    setAll(allClicks.concat('L'))
  }
```


## Component
不要在其他组件内部定义组件。 这种方法没有任何好处，而且会导致许多不愉快的问题。最大的问题是React 在每次渲染时，会将内部的组件当作一个新的组件。这回导致React 无法去优化组件。
```
const App = props => {
  // Do not define components inside another component
  const Display = props => <div>{props.value}</div>

  return (
    <div>
      <Display value={value} />
    </div>
  )
}
```


