# js设计模式

https://juejin.im/entry/58c280b1da2f600d8725b887

常见问题可重用解决方案，编程模板

使代码更易理解，维护

## 工厂模式

目的是为了创建对象,定义用于创建对象的接口

简单工厂模式：创建同一类对象，解决相似问题(创建的对象数量较少，对象的创建逻辑不复杂时使用)
```js
function simpleFactory({name:name='hew', score:score=123} = {}) {
    const obj = {}
    obj.name = name
    obj.score = score
    obj.fn = function () {
        console.log(`${this.name}:${this.score}`);
    }

    return obj
}

console.log(simpleFactory().fn()) 
```

工厂方法模式 对象实例化推迟到子类中
```js
class Factory {
    constructor({ name: name = 'hew', subject: subject='chinese' } = {}) {
        this.name = name
        this.subject = subject

        if(new.target === Factory) {
            throw new Error('抽象类不能实例化');
        }
    }
}

class Child extends Factory {
    constructor(params, score){
        super(params)
        this.score = score
    }

    create(type) {
        switch(type) {
            case 1: return new Child({name: 'hee'}, 333); break;
            default: return new Child({name: 'trump'}, 444)
        }
    }
}
const child = new Child()
console.log(child.create(2))
```

抽象工厂模式 对象实例化推迟到子类中
```JS
class Factory {
    constructor({ name: name = 'hew', subject: subject='chinese' } = {}) {
        this.name = name
        this.subject = subject

        if(new.target === Factory) {
            throw new Error('抽象类不能实例化');
        }
    }
}

class ChildOne extends Factory {
    constructor(params, score){
        super(params)
        this.score = score
    }

    execut() {
        console.log('excute1');
    }
}

class ChildTwo extends Factory {
    constructor(params, score){
        super(params)
        this.score = score
    }

    execut() {
        console.log('excute2');
    }
}

function switchFactory(type) {
    switch(type) {
        case 1: return new ChildOne({name: 'hee'}, 333); break;
        default: return new ChildTwo({name: 'trump'}, 444)
    }
}
console.log(switchFactory(2))
````

构造函数模式
```js
class Factory {
    constructor({ name: name = 'hew', subject: subject='chinese', score:score = 100 }) {
        this.name = name
        this.subject = subject
        this.score = score
    }

    add() {
        return  `${this.name} : ${this.subject} - ${this.score}`
    }
}

console.log(new Factory({name:'hew'}));
console.log(new Factory({name:'trump'}).add());
```

## 单例模式
只需要一个的对象(如浏览器中的window等), 只有一个实例，全局访问

惰性单例（点击或需要使用时才创建）

应用场景：管理模块；命名空间，减少全局变量数量

export default 也满足单例模式

 <button id="btn">打开弹窗</button>
    <script>

        function Single(name) {
            this.name = name
        }

        const execute = (function ()  {
            let once = null

            return function(param) {
                if (!once) {
                    once = new Single(param)
                }

                return once
            }
        })()

        const a = execute('hew')
        const b = execute('trump')
        console.log(a === b)  // true
        // 传入的参数 trump 无任何作用


        // 实现单体模式弹窗
// var createWindow = (function(){
//     var div;
//     return function(){
//         if(!div) {
//             div = document.createElement("div");
//             div.innerHTML = "我是弹窗内容";
//             div.style.display = 'none';
//             document.body.appendChild(div);
//         }
//         return div;
//     }
// })();
// document.getElementById("btn").onclick = function(){
//     // 点击后先创建一个div元素
//     var win = createWindow();
//     win.style.display = "block";
// }

        // 弹窗实例
        const createEle = (function() {
            let once = null
            return function() {
                if (!once) {
                    const div = document.createElement('div')
                    div.innerHTML = '我是弹窗'
                    div.addEventListener('click', function() {
                        this.setAttribute('style', 'display:none')
                    })

                    document.body.append(div)
                    once = div
                }
                return once
            }
        })()

        document.getElementById('btn').addEventListener('click', function() {
            const div = createEle()
            div.setAttribute('style', 'display:block')
        })
    </script>

> 交流 [Github blog issues](https://github.com/NameHewei/blog/issues)