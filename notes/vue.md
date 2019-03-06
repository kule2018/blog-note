[toc]

---

- axios 可以自动判断上传的数据是否是formdata，从而修改content-type

---

# Vue

## 注意项

### 概述

- Mustache（大胡子）：{{}}  

---
- export defaule 后的东西默认为new Vue()的参数  

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

11. v-model后不能跟表达式

## 生命周期 
- destroyed ： 如果有定时器，在该钩子函数中务必清除
https://www.jianshu.com/p/a20f2023c78a


## 组件基础
1. data 选项必须是一个函数，因为可以返回对对象的独立拷贝，避免相互影响
2. 每个组件必须只有一个根元素
3. 
    ```
    利用 $emit(n ame, value) 来向父组件传参，父组利用v-on:ud-event="a=$event"
    
    这里$event为传的value值，赋值给了a变量，如果这里事件后跟的不是表达式而是方法，则方法第一个参数为value值
    ```
4. 在input标签上的v-model等价于value与input事件的结合，在自定义组件类似，使用￥emit('input', $event.target.value)

## 自定义事件
1. 自定义事件名，会被转换为全小写；camelCase 或 PascalCase 与 kebab-case，永远不会相同；推荐使用 kebab-case 命名


## vue-loader

- 深度作用域 
```
.a >>> .b 
.a /deep/ .b
```

## vue-cli
- assets 目录一般主要放样式代码 会被webpack编译
- 当打包后的代码不是放到域名的根目录，导致css中的背景图片路径不正确，可以将图片放到此目录，然后在build/utils.js 中修改ExtractTextPlugin 的 publicPath
- 最好用相对路径

## cue-cli-3
- 图片资源放到assets，不要放到public中否则打包出来的图片会是两份
- 其它的js资源可以放到public中

- vue inspect > output.js 仅仅用于审查

## keep-alive
1. include 包含的是组件的name属性值
2. 通过同一个router-view 进入的路由间切换, keep-alive 都有效,都会缓存页面。
3. 只要通过keep-alive下的路由(前提是要包含在include中) 都会触发activated, 只有第一次进入会触发mounted（切换过router-view入口 再进入也会触发mounted）
4. 注意include 如果用字符串值，后面名称与逗号之间不要有空格
 
### 处理保存页面状态
- 最好一个模块有一个单独的 router-view 
- 在 activated 中请求需要实时更新的数据 
- 在 beforeRouteLeave 中处理和当前需要保存状态页面走同一个 router-view 的页面，否则在这些页面间切换，页面的状态也会被保留（data中的数据）

## 深入响应式原理
 - 非侵入性的响应式系统
 - 数据模型为js对象，对其修改时，视图更新

### 如何追踪变化

- vue将接收的data全部用Object.defineProperty把属性转为getter/setter(导致不支持ie8以及一下)

- 属性被访问和修改时通知变化

- 每个组件实例都有对应的watcher实例对象（它会在组件渲染的过程中把属性记录为依赖，当依赖的setter被调用时，会通知watcher重新计算，从而使相关组件更新）

### 检测变化的注意事项

- 只有在data对象上的属性才是响应式的

- 改变对象和数组的一些情况不会被检测到更新

- 要用到的状态，提前在data对象中声明

### 异步更新队列


# vuex

commit 触发 mutation store.commit('name')

dispatch 触发 action store.dispatch('increment')

# api once-over

## 计算属性
computed 不能传参

默认只有getter
```js
computed: {
    testComputed: {
        get() {
            return this.name // name变动时调用 getter
        },

        set(v) {
            this.name = v
        }
    }
}

this.testComputed = 'new name' // 触发setter
```

