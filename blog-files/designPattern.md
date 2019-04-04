# js设计模式

https://juejin.im/entry/58c280b1da2f600d8725b887

常见问题可重用解决方案，编程模板

使代码更易理解，维护

1. 工厂模式
2. 单例模式
3. 模块模式
4. 代理模式

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

应用场景：管理模块；命名空间，减少全局变量数量

export default 也满足单例模式

利用类和闭包来实现
```js
class SingleConstruct {
    constructor(name) {
        this.name = name
    }

    getName() {
        return this.name
    }
}
const Single = (function() {
    let once = null
    return function(name) {
        if(!once) {
            once = new SingleConstruct(name)
        }
        return once
    }          
})()
const a = new Single('hew')
// 传入的参数 trump 无任何作用
const b = new Single('trump')
console.log(a === b)  // true
```

弹窗实例（惰性单例实现）惰性单例：点击或需要使用时才创建

```html
 <button id="btn">打开弹窗</button>
```

```js
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
    // 每次点击都是操作的同一个div
    const div = createEle()
    div.setAttribute('style', 'display:block')
})
```

## 模块模式

对象字面量方式

```js
const moduleObject = {
    name: 'modeule',
    config: {
        version: 'v0.0.0'
    },

    getName: function() {
        console.log('function getName');
    }
}

console.log(moduleObject.name);
console.log(moduleObject.getName());
```

匿名函数形式
```js
const modulePattern = (function() {
    const privateCount = 1122
    const privateFn =  function() {
        console.log('private funnction');
    }

    return {
        variable: 'var',
        method1: function(){
            console.log(privateCount);
        },
        method2: function() {
            console.log('method2');
        }
    }
})()

console.log(modulePattern.privateCount); //undefined
console.log(modulePattern.method1()); // 1122
```

## 代理模式

提供一个代理对象，可以访问某个对象中的方法

简单示例
```js
// 老板找人替自己板砖
class Staff{
    constructor(name) {
        this.staff = name
    }
}

class Boss{
    constructor() {
        this.boss = 'Hew'
    }
    liftingBrick(who) {
        console.log(`${who.staff} help boss ${this.boss} lifting brick`);
    }
}

class ProxyLiftingBrick{
    liftingBrick(staff){
        new Boss().liftingBrick(staff)
    }
}

const plb = new ProxyLiftingBrick()
plb.liftingBrick(new Staff('Trump'))
```

// 图片加载
```js
// 创建img标签元素
const createImgEle = (function() {
    const img = document.createElement('img')
    document.body.appendChild(img)

    return {
        setSrc: function(url) {
            img.src = url
        }
    }
})()

// 代理加载图片
const proxyLoadImg = (function() {
    const imgObj = new Image()
    imgObj.onload = function() {
        setTimeout(() => {
            createImgEle.setSrc(this.src)
        }, 2000);
    }
    return {
        setSrc: function(url) {
            // 默认图
            createImgEle.setSrc('http://img2.imgtn.bdimg.com/it/u=3806557979,3233516071&fm=26&gp=0.jpg')
            imgObj.src = url
        }
    }
})()        

proxyLoadImg.setSrc('http://pic.58pic.com/58pic/15/68/59/71X58PICNjx_1024.jpg')
```

> 欢迎交流 [Github](https://github.com/NameHewei/blog-note)