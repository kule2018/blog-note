[toc]
# React

Facebook开发

---


1. 复杂场景下的高性能。
2. 重用组件库，组件组合。

---
当input设置了value，但是没有设置onChange时会报错，可设置defaultValue或把onChange事件加上

---


jsx和babel的区别在于babel可以将按es6语法写的语句改写为es5兼容浏览器，而jsx只能用es5的语法。

---
**引用的文件**

 react.js是react的核心库，react-dom是提供与dom相关的功能，browser是将jsx语法转换为javascript语法；

---


ReactDOM.render(&lt;div&gt;当要添加多个标签时要用div包含在内&lt;/div&gt;,容器元素对象)

---
jsx中写js的代码用{}括起来；之外可以正常用；

不能用if else  但是可以用三元运算符 a==b?trueTodo:falseTodu;

react推荐使用内联样式

注释放在花括号中

---
1. function component  
function Welcome(props) {  
  return < h1>Hello, { props.name}< /h1>;  
}
2. 不用es6语法  
var Name= React.createClass({render:function(){  
    return < span>niao< /span>;  
}})
3. es6语法  
class Welcome extends React.Component {  
  render() {  
    return < h1>Hello, {this.props.name}< /h1>;  
  }}

组件类名必须大写，且只能包含一个顶层标签  
通过this.props.属性名，来获取参数  
属性名class要用className，for要用htmlFor  
复合组件要用div标签包含起来  
this.props的属性与组件的属性一一对应，但是this.props.children例外，它表示组件的所有子节点，它会返回undefind，object，array类型的值，所以react提供了一个方法React.Children来处理它可以用React.Children.map()，来遍历就不用担心返回的是什么类型的值。

---
**ref和findDOMNode**
- 在节点上设置ref属性，然后用this.refs.属性名即可获取到真实的节点
- ref添加到Compoennt上获取的是Compoennt实例，添加到原生HTML上获取的是DOM
- ReactDOM.findDOMNode，当参数是DOM，返回值就是该DOM（这个没啥卵用）；当参数是Component获取的是该Component render方法中的DOM，返回的都是DOM


---
**对于表单value**
不能用this.props来获取，只能用event.target.value获取

---

**组件的生命周期**
mounting：已插入真实的DOM  
updating：正在被重新渲染  
unmounting：已移除真实的DOM  
will:函数在进入状态之前，did：函数在进入状态之后  
componentWillMount()  
componentDidMount()  
componentWillUpdate(object nextProps, object nextState)  
componentDidUpdate(object prevProps, object prevState)  
componentWillUnmount()  
Mounted：组件被render解析，生成对应DOM节点并被插入浏览器DOM结构的过程。  
Update：mounted的组件被重新render的过程。  
Unmounted：组件对应的DOM节点被从DOM结构中移除的过程。  
每一个状态都封装了相应的hook（钩子）函数  

---
**状态state**  
初始状态用getInitialState对象赋值  
getInitialState:function(return {状态名:值})  
该对象可以用this.state获取  
用this.setState修改该对象，每次修改都会重新调用this.render方法重新渲染  
在渲染是修改了state或props会陷入死循环。

---
**props和state**  
props是不可以改变的  
用getDefaultProps()为props赋初值  
getDefaultProps:function(){  
        return {  
        name:'hew'  
}}

---
组件的属性类型判断，验证props  
设置propTypes:{  
        属性名:React.PropTypes.string|array|bool|func|object|  number.isRequired  
}

# Redux
## redux杂项
Action 发出以后，Reducer 立即算出 State，这叫做同步；Action 发出以后，过一段时间再执行 Reducer，这就是异步。

---
 react-router 和react-router-dom 只要引用一个就行了，不同之处就是后者比前者多出了 < Link> < BrowserRouter> 这样的 DOM 类组件。  
因此我们只需引用 react-router-dom 这个包就行了。当然，如果搭配 redux ，你还需要使用 react-router-redux。

---
## 基本概念
store  
保存数据的地方，可看成一个容器，整个应用只能有一个store  
redux提供了createStore函数接收一个函数参数，返回新的store对象

---
state  
store对象包含了所有数据，如果想得到某个时点的数据就要对store生成快照，这种时点的数据结合就叫state  
当前时刻的state可以用store.getState()获得一个state对应一个view

---
action  
state的变化会导致view的变化，但是用户只能看到view，所以state的变化是view导致的，  action就是view发出的通知，告知state要变了  
action是一个对象，type属性是必须的，其它的随意  
store.dispatch()是view发出action的唯一方法，可接受一个action对象作为参数。

---
reducer  
store接收到action后，必须给出一个新的state，view才会变化，这就是reducer过程。  
reducer函数接收state和action参数，返回一个新的state。  
store.dispatch()方法会触发reducer的自执行

---
subscribe  
可以用subscribe函数监听store，一旦state发生变化就自动执行这个函数，该方法返回一个函数，调用这个函数就可以接触监听。

# Vue
Mustache（大胡子）：{{}}  
缩写：v-bind：href（：href）；v-on：click（@click）

---
export defaule 后的东西默认为new Vue()的参数  

---
1. 无论何时，绑定的数据对象上 message 属性发生了改变，插值处的内容都会更新;通过使用 v-once 指令，你也能执行一次性地插值，当数据改变时，插值处的内容不会更新。
2. 过滤器函数总接受表达式的值作为第一个参数。
3. 模板表达式都被放在沙盒中，只能访问全局变量的一个白名单，如 Math 和 Date 。你不应该在模板表达式中试图访问用户定义的全局变量。
4. Vue 2.x 中，过滤器只能在 mustache 绑定和 v-bind 表达式（从 2.1.0 开始支持）中使用，因为过滤器设计目的就是用于文本转换。为了在其他指令中实现更复杂的数据变换，你应该使用计算属性。
5. 然而，不同的是计算属性是基于它们的依赖进行缓存的，计算属性只有在它的相关依赖发生改变时才会重新求值。这就意味着只要 message 还没有发生改变，多次访问 reversedMessage 计算属性会立即返回之前的计算结果，而不必再次执行函数。
6. 计算属性默认只有 getter ，不过在需要时你也可以提供一个 setter 
7. 在 v-bind 用于 class 和 style 时， Vue.js 专门增强了它。
8. v-else 元素必须紧跟在 v-if 或者 v-else-if 元素的后面——否则它将不会被识别。类似于 v-else，v-else-if 必须紧跟在 v-if 或者 v-else-if 元素之后。
9. 非常频繁地切换，则使用 v-show 较好；如果在运行时条件不太可能改变，则使用 v-if 较好。
10. 有时也需要在内联语句处理器中访问原生 DOM 事件。可以用特殊变量 $event 把它传入方法

