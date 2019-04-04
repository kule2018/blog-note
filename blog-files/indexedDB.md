[toc]
# indexedDB添加，删除，获取，修改
> 在chrome(版本 70.0.3538.110)测试正常
> 编写涉及：css, html, js

[在线演示codepen](https://codepen.io/Hewitt/pen/vQMxPe)

# html代码
```html
<h1>indexedDB</h1>
<h2>在 DevTools 的 Application 中查看数据库信息</h2>

<button onclick="addDBData()">添加数据</button>
<div>
    <button onclick="getDBData()">获取数据</button>
    <input type="text" id="getID" placeholder="请输入ID">
</div>
<div>
    <button onclick="delDBData()">删除数据</button>
    <input type="text" id="delID" placeholder="请输入ID">
</div>
<div>
    <button onclick="updateDBData()">更新数据</button>
    <input type="text" id="updateID" placeholder="请输入ID">
</div>
<div id="display"></div>
```

# css代码
```css
button {
    margin: 10px 0;
    padding: 8px 10px;
    border: 0;
    color: #fff;
    background-color: rgb(7, 196, 230);
}
input{
    padding: 8px 5px;
    border: rgb(7, 196, 230) solid 1px
}
```

# JavaScript代码

```js      
window.indexedDB = window.indexedDB || window.mozIndexedDB || window.webkitIndexedDB || window.msIndexedDB;
if (!window.indexedDB) {
    alert('不支持indexDB')
}

const DATA_BASE = 'TEST_DB'
let db = {}

/**
    1. 不存在当前数据库时，即为创建
    2. open参数：数据库名称，版本号（整数）
*/
const request = window.indexedDB.open(DATA_BASE, 1) 

request.onerror = function (e) {
    console.error('error', e)
}

/**
    1. 数据库已存在，打开成功
*/
request.onsuccess = function (event) {
    db = event.target.result
    console.log('execute onsuccess');
};

/**
    1. 当数据库不存在时，创建数据库会触发 onupgradeneeded 事件
    2. 当指定的版本号高于当前时会直接触发 onupgradeneeded 事件
    3. 唯一可以修改数据库结构的事件
*/
request.onupgradeneeded = function (event) {
    /**
        1. 保存 IDBDataBase 接口（数据库）
    */
    db = event.target.result
    console.log('execute onupgradeneeded');

    /**
        1.使用键生成器,测试时，去除注释即可
    */
    // const objectStore = db.createObjectStore('users', { autoIncrement : true })
    // objectStore.add({name: '123'});
    // objectStore.add('123');

    /**
        1. 为当前数据库创建对象仓库（表） 
        2. 这里的keyPath 相当于主键
        3. createIndex(indexName, keyPath, {unique | multiEntry | locale})
    */
    const objectStore = db.createObjectStore('users', { keyPath: 'id' })
    objectStore.createIndex('name', 'name', { unique: false })
    objectStore.createIndex('age', 'age', { unique: false })

    /**
        1. 确保初始化数据的时候，对象仓库已经创建完毕
    */
    objectStore.transaction.oncomplete = function(event) {
        const transaction = db.transaction(['users'], 'readwrite')
        const objStore = transaction.objectStore('users')
        objStore.add({
            id: 12, 
            name: `hew-${Math.random()}` ,
            age: parseInt( Math.random() * 100, 10)
        })
    }
}

/**
    1. 所有数据库操作都基于事务
    2. 事务三种模式：readonly，readwrite，versionchange
    3. 修改数据库模式或结构——包括新建或删除对象仓库或索引，只能用 versionchange 模式
*/
function addDBData() {
    const transaction = db.transaction(['users'], 'readwrite')
    const objectStore = transaction.objectStore('users')
    const request = objectStore.add({ 
        id: Math.random() * 10, 
        name: `hew-${Math.random()}` ,
        age: parseInt( Math.random() * 100, 10)
    })

    transaction.oncomplete = function (event) {
        console.log('transaction add complete')
    }

    transaction.onerror = function (error) {
        console.error('add error', error)
    }

    request.onsuccess = function (event) {
        console.log('add complete')
    }
}

function getDBData() {
    const id = parseFloat(document.getElementById('getID').value)
    const transaction = db.transaction(['users'], 'readwrite')
    const objectStore = transaction.objectStore('users')

    /**
        1. 注意数据类型
    */
    const request = objectStore.get(id)

    request.onsuccess = function (event) {
        console.log('get complete', event.target.result)
        document.getElementById('display').innerHTML = JSON.stringify(request.result)
    }

    request.onerror = function (err) {
        console.error('get error', err)
    }
}

function updateDBData() {
    const id = parseFloat(document.getElementById('updateID').value)
    const transaction = db.transaction(['users'], 'readwrite')
    const objectStore = transaction.objectStore('users')
    const request = objectStore.get(id)

    request.onsuccess = function (event) {
        const d = event.target.result
        d.name = 'name name'
        const objectStoreUpdate = objectStore.put(d)
        objectStoreUpdate.onsuccess = function (e) {
            console.log('update success')
        }
        
        document.getElementById('display').innerHTML = 'update success'
    }

    request.onerror = function (err) {
        console.error('get error', err)
    }
        
}

function delDBData() {
    const id = parseFloat(document.getElementById('delID').value)
    const request = db.transaction(['users'], 'readwrite').objectStore('users').delete(id)

    request.onsuccess = function() {
        console.log('delete complete', id);
    }
}
```

> [参考](https://developer.mozilla.org/zh-CN/docs/Web/API/IndexedDB_API/Using_IndexedDB)

> 欢迎交流 [Github](https://github.com/NameHewei/blog-note)