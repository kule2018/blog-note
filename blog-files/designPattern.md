# js设计模式及实例

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

工厂方法模式
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

抽象工厂模式
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

// 简单模式
console.log(new Factory({name:'hew'}));
console.log(new Factory({name:'trump'}).add());
```

复杂模式：对象实例化推迟到子类中

> 交流 [Github blog issues](https://github.com/NameHewei/blog/issues)