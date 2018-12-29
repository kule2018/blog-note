[toc]

# 命令
## linux  
创建目录：mkdir name  
删除目录：  
* rm  删除文件 -r 递归删除，可删除子目录及文件  -f 强制删除  
* rmdir 删除空目录  

显示：  
ls 显示文件或目录 -l 列出文件详细信息l(list)；  -a  列出当前目录下所有文件及目录，包括隐藏的a(all)

---
# npm

**npm-shrinkwrap.json和package-lock.json区别**
- shrinkwrap 向后兼容npm版本2,3和4
- package-lock 只能被npm 5+识别
- 可以通过运行npm shrinkwrap package-lock.json将现有的package-lock.json转换为npm-shrinkwrap.json
- shrinkwrap应该用于库来保证安装程序包的每个人都获得完全相同的所有依赖项版本
- package-lock允许安装程序包的人使用与package.json指定的版本范围兼容的任何版本的依赖项
- npm install 操作会自动生成package-lock文件 并且更新该文件
- 如果是用的cnpm安装的包 注意要npm install操作一次 更新package-lock文件

---
**package.json中：**  

devdependencies表示开发过程中依赖的包

dependencies表示项目在生产环境中依赖的包    

包版本号前面的尖括号表示只限制版本号（比入^0.1.1,如果有小于1.0.0的版本都可自动

更新，超过就保持0.9.9），波浪号表示只监控最小版本号的更新（如~0.1.2,当有大于改版本号且小于0.2.0才更新）  
  “engines”:{  
  “node”:”>=0.10.0”  
} //便是node版本需求  
“script”:{
  “test”:”grunt test”    
}  
当运行npm test   实际执行是grunt test  
npm start || npm test  可以直接用。  
其它用npm run 名称   
可以直接使用npm 运行的脚本命令

---
--save 放在dependences中  
--save-dev 放在devDependences中  
npm install 默认两个下的都安装，--production 只安装dependences的 

# node

## 报错信息
- 502： bad gateway 错误的网关
- throw er; // Unhandled 'error' event ：请检测是否为端口被占用
- EADDRINUSE : 给定的地址已经被使用

## windows安装
> 如果不是安装在c盘需要设置环境变量

## 模块的分类
1. 一．核心模块
2. 二．文件模块
3. 三．第三方模块

## 基础信息

Node里面没有全局命名空间的概念

用require('path')来导入模块

Module.exports=add和exports.add=add推荐使用后者;除非模块的对象类型，传统的模块实例修改为其它的

用exports.add将某个模块暴露出来;

url.parse('http://www.imooc.com/video/6710')

protocol:'http:',表示底层的协议

slashes:true,有没有协议后面的双斜线;

host:ip地址或是域名;

port:端口

hostname:主机名;

还可以加传两个参数

第二个参数:默认false，设置为true，就会用queryString来解析query的字符串，会将query的值解析为对象模式;

第三个参数:默认false,设置为true,就会对没有明确协议的url进行正确解析;

url.format({});生成一个url地址;

url.resolve('http://baidu.com'，'/a/b/c');

[http://baidu.com/a/b/c](http://baidu.com/a/b/c)

HTTP:

浏览器搜索自身DNS缓存，如果有就看有没有过期如果过期就结束，就开始搜索操作系统的DNS缓存，若也没有就读去本地Host文件，若也没有浏览器就会发起一个DNS系统调用（一般是运营商的），运营商服务器会产看自身的缓存，一直逐层请求解析DNS

About:DNS

chrome://net-internals/#dns

---

用nodejs打开js文件，先进入到放js文件的目录然后用命令（node js文件名）就可。

This表示函数的拥有者。

node的全局对象global   相当于浏览器中的window

---

call

object1.function.call(object2,参数,参数....)

将对象object1中调用的函数中的this换为指向object2(即盗用了object2域中的属性)，参数是object1中调用的函数需要的参数。

继承中的用法

冒充对象的作用域

函数名（f1）：call（对象名，f1的参数,...）:这句话写在需要继承别的构造函数的域的构造函数中

f1是构造函数

当后面的对象为this时，表示调用前面函数的对象；

性能测试：Apache ab

---

cheerio是nodejs的抓取页面模块，为服务器特别定制的，快速、灵活、实施的jQuery核心实现。适合各种Web爬虫程序。

---

官方建议对一个事件不要设置超过十个监听器。太多的话可能会导致内存泄露（内存空间使用后没有收回）。

var eventsEmitter=require('events').EventEmitter;

var life=new eventsEmitter();

life.on('e1',function(w){
    console.log('事件1是:'+w);
});

life.emit('e1',11);

更改监听数量

life.setMaxListeners(数量);

查看是否被监听过

life.emit()会返回一个布尔boolean值;如果监听返回true；移除某个事件

life.removeListener('事件名'，具名函数名f)

life.on(事件名，函数名f);

批量移除

life.removeAllListeners(事件名);

某个事件的个数;

life.listeners(事件名).length或

eventsEmitter.listenerCount(life（实例化）,事件名)

---

在http的api中知道get是对request的封装

---

Access-Control-Allow-Origin与跨域

在某域名下使用Ajax向另一个域名下的页面请求数据，会遇到跨域问题。另一个域名必须在response中添加 Access-Control-Allow-Origin 的header，才能让前者成功拿到数据。只有当目标页面的response中，包含了 Access-Control-Allow-Origin 这个header，并且它的值里有我们自己的域名时，浏览器才允许我们拿到它页面的数据进行下一步处理

res.writeHead(200, {'Access-Control-Allow-Origin':'*'});

如果它的值设为 * ，则表示谁都可以用。

---
__dirname nodejs的全局变量，指向当前执行脚本所在目录。

---

node在调其它文件的时候需要用require('./地址')

css中引用url时只需用（/image---）

render('name/name/docs')

---
module.exports=与exports=的区别

module.exports=exports={}//是按照这个方式赋值

当先设置了module.exports,exports.属性 将失效

require()返回的是module.exports

把一个对象封装到模块当中

module.exports=function(){  
     this.name='hew';  
} //用require获取到的是一个函数方法

多个模块

exports.login=function(){}  //用require获取到的是一个对象

如{  
    name:function{},login:function(){}  
}

---
exports是模块公开的接口

require用于从外部获取一个模块接口及获取模块的exports对象

---
### 常见的Content-Type

application/x-www-form-urlebcoded 常见的form提交

multipart/form-data 不对字符编码在对文件上传时必须使用该值

application/json json格式数据提交

text/xml  提交xml格式数据

### Request Method 

> GET, HEAD, POST, PUT, PATCH, DELETE, OPTIONS, TRACE

- OPTIONS: 询问服务器支持的方法。当浏览器发现，是一个非简单请求，就自动发出一个"预检"请求，"预检"请求用的请求方法是OPTIONS

- 当header 的content-type 类型是以下类型时不触发options
  - application/x-www-form-urlencoded
  - multipart/form-data
  - text/plain



## 定时器
[参考](http://www.ruanyifeng.com/blog/2018/02/node-event-loop.html)

setTimeout()

setInterval()

setImmediate()

process.nextTick() 是在本轮循环执行的，所有异步任务里最先执行的

1. 同步任务比异步任务早执行
2. 异步任务  
   - 本轮循环（event loop，js处理异步任务的方式）
   - 次轮循环
   - 本轮循环早于次轮循环

process.nextTick()和Promise()的回掉函数追加在本轮循环，即同步任务一旦执行完，就开始执行。

setTimeout，setInterval，setImmediate追加在次轮循环

### 微任务

promise的回掉会进入异步任务的“微任务”队列

微任务队列追加在process.nextTick队列之后，也是属于本轮循环

> 只有前一个队列执行完了之后才能执行下一个队列

### 事件循环

[https://yuchengkai.cn/docs/zh/frontend/browser.html#node-%E4%B8%AD%E7%9A%84-event-loop](https://yuchengkai.cn/docs/zh/frontend/browser.html#node-%E4%B8%AD%E7%9A%84-event-loop)

事件初始化，会先完成下面事情：

同步任务

发出异步请求

规划定时器生效的时间

执行process.nextTick()等等

---
事件循环会无限次地执行，只有异步任务的回调函数队列清空了，才停止。

每一轮六个阶段依次执行

1. timers:
  执行setTimeout 和setInterval,他们设置的时间并不是准确的执行时间，而是到了事件后，尽快的执行，因为系统可能因为其它而被耽误
  范围[1, 2147483647]，不在设为1

2. I/O callbacks:
  执行除了 close 事件，定时器和 setImmediate 的回调

3. idle, prepare:
  idle, prepare 阶段内部实现

4. poll

5. check

6. close callbacks

---


# express

var express=require(express);

var app=express();启动一个web服务器，将实例赋值给一个变量叫app

express()是express模块导出的一个入口函数。

---

# koa

- koa-static 当设置的目录下有index.html, 访问根路径时，会默认渲染index.html
- koa-multer 处理上传的文件
- koa-bodyparser 解析上传的json(基本)
- 使用koa2-cors时 要把app.use(cors())放在最前面


## graphql 实现
- 安装 apollo-server-koa 和 koa，看提示再安装graphql

### 学习
- 是一个用于 API 的查询语言，通过定义类型和类型上的字段来创建的，然后给每个类型上的每个字段提供解析函数


## 跨域

- 方法一
```
app.use(async function(ctx, next) {
    ctx.set("Access-Control-Allow-Origin", ctx.request.header.origin)
    await next()
})
```
- 方法二

```
const cors = require('koa2-cors')
app.use(cors({
    origin: function (ctx) {
        return 'http://localhost:1111';
    },
    exposeHeaders: ['WWW-Authenticate', 'Server-Authorization'],
    maxAge: 5,
    credentials: true,
    allowMethods: ['GET', 'PUT', 'POST', 'PATCH', 'DELETE', 'HEAD', 'OPTIONS'],
    allowHeaders: ['Content-Type', 'Authorization', 'Accept'],
}));
```

---

-  ctx的 headers 和 header 属性皆可获取： ctx.header.origin

## koa-router 
- /page/:path  利用 ctx.params.path 获取

## request

- 当没有默认导出时要用 * 防止报错  import * as api from './controllers/api'

- ctx.request.query：获取query string参数 以{ key:value } 形式返回



