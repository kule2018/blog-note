[toc]

# Javascript

---

动静态语言： 声明的变量是否可以存储不同类型的值，在编译阶段会检测类型

强弱类型语言： 其产物是，是否允许不同类型值之间进行计算

js(动态弱类型语言)

c|c++ 编译型语言 将程序编译成机器语言

java python 解释型语言（java 将程序编译成字节码：理解为一种中间语言，再由JVM将字节码再翻译成机器语言）

**节点操作**
- 当把获取到的节点添加到DOM中的另外一个地方时，原位置的节点没有了，移动到文档片段也是同理；相当于移动节点位置

---

**document.createDocumentFragment()**
- 创建新的文档片段
- DocumentFragments 是属于DOM节点的

---

**垃圾回收**
- 当没有变量指向某一内存 a={b:1}; a={c:2}; 存贮{b:1} 会被回收
- 函数调用完后，内部所有变量将被回收

---

zepto.min.js 加载新的模块  直接在 https://github.com/madrobby/zepto/tree/master/src 将需要的模块拷贝到min.js中

---

**try catch**

如果catch和finally中再抛出异常需要外部再添加try-catch

finally 如果返回了值 将作为整个try-catch-finally块的返回值,外层如果还有try-catch将无法捕获异常，且外层要包裹函数，作为函数返回值。
```js
try{

} catch (error) {

} finally {
    // 无论是否有异常，finally中的语句都会执行
}
```

**throw 方法：**

用此方法抛出错误，后续的代码将不会执行，错误会被catch捕获，如果没有catch将其捕获，程序将终止

new Error([message[, fileName[, lineNumber]]])
- chrome 不支持后两个参数
- 用new和不用，输出的结果一样
- 还有其它类型错误：ReferenceError（引用错误）,TypeError(类型错误)，RangeError(范围错误) 等


---
**setTimeout | setInterval**

- setInterval 一定要确认清除
- 第三个及之后的参数都作为回调函数的参数

**requestAnimationFrame**
> 示例：https://codepen.io/Hewitt/pen/VgZapr
- 回调函数在重绘前调用
- 浏览器频率是16.7ms(1s/60)，setTime设置时间小于这个值时会出现帧丢失的情况
- 而requestAnimationFrame是不用设置时间的，设备的时间绘制间隔是好久，它就是好久
- 当页面没有激活的时候，它会被停止调用，而 setTimeOut 不会
- 回调函数：有一个参数，就是触发该函数的当前时间，可以打印出来

---
**复制内容**

```
<input type="text" id="text">
<button onclick="copy()">获取焦点</button>

function copy() {
  document.getElementById('text').select() // 先select()选中(只有textarea和input有select方法)
  document.execCommand("copy");
}

// 还有新的方法如createRange()等
```

---
**表达式** 
> 是由运算元和运算符(可选)构成，并产生运算结果的语法结构(了解即可，不必纠结).
- 所有的表达式都有返回值(没有返回undefined)
- 函数调用是表达式
- this, null, arguments,变量，字面量（仅包括数字、布尔值、字符串、正则字面量） 


**语句**
- 典型的有循环语句和if语句，
- 使某事发生的指令，没有返回值
- 也可以是由大括号括起来的复合语句

---
**阻止a标签默认事件**
- a href="javascript:void(0);" onclick="js-method()"  最周全的方法，onclick方法负责执行js函数，而void是一个操作符，void(0)返回undefined，地址不发生跳转。
- a href="javascript:;" onclick="js_method()" 同上，只是执行了空代码。


---
 **ready与onload的区别**
 $(document).ready()是在DOM结构载入完后执行的，而window.onload是在所有文件都加载完后执行的。
 ```js
 // 原生实现ready
if(document.addEventListener) {
    document.addEventListener('DOMContentLoaded', handler, false);
    document.addEventListener('readystatechange', handler, false); //IE9+
    window.addEventListener('load', handler, false);
}else if(document.attachEvent) {
    document.attachEvent('onreadystatechange', handler);
    window.attachEvent('onload', handler);
}

function handler() {
    //注销事件, 避免反复触发
    document.removeEventListener('DOMContentLoaded',arguments.callee, false);
}
 ```


---
**正序遍历与反序遍历**

反序更快 for(var i＝item.length; i--; ) *注意最后的分号,该方法会从length-1开始*  
 

 ---
 **continue | break | return  区分**
 - break,continue是一起的，return 是函数返回语句，但是返回的同时也将函数停止。  
 - break和continue这两个应用的范围是退出循环或者switch语句，在其他地方使用会导致错误.    
 - continue(跳出本次循环)语句只能用在while语句、do/while语句、for语句、或者for/in语句的循环体内，在其它地方使用都会引起错误！
 
 - return 后面必须紧跟语句，不能换行
 - return 只能出现在函数体内 语法为：return 表达式。
 - 无函数结果，语法为：return，把控制权返回给页面
 - return false的作用一般是用来取消默认动作的，例如,默认情况下点击一个< a>元素。

---

## 滑动条与元素位置
1. element.scrollIntoView({ behavior: "smooth"});//js原生，让元素滚动到可见区域

2. js中是 element.scrollTop=100（scrollLeft）来设置或获取滑动条的位置;

3. 谷歌的页面滚动是用的body，火狐是用的html；

4. 谷歌:当scrollTop的值小于1时会直接返回0，所以用y=1除以a的x次方指数函数来趋近0来由快到慢的滑动。

5. window 没有 scrollTop 等方法，有 scrollX 等


## 元素的高度问题  
返回元素相对于父元素的位置的对象{left,top}  

element.position().left/top，对应 js 中的 offsetLeft 和 offsetTop，用了position更精确。

## cookie
1. document.cookie='name=hew;path=/;expires=UTCstring;max-age=秒'  //设置和获取  

---
var ojb=JSON.parse('[{"a":"0","b":"1"}]')  
//数字可以不加引号,并且可以是数组与对象的多重结合，也可以只有对象，里面只能用双引号  
```js
var ojb=JSON.parse('{"hew":"yes"}',function(key,value){  
    if(key=='hew'){
        return 'hew'+value;
    }  
    else{  
        return value;  
    }
});
console.log(ojb) // {hew: "hewyes"}
```
---
**stringify:**

syntax:JSON.stringify(value[, replacer[, space]]) **巴科斯范式(BNF)**
- value:数组与对象的结合;
- replacer:函数或是数组；一般设为null；
- space：缩进 | 空格 | 换行 （数字或\t 等）；大于 10，则文本缩进 10 个空格；一般设为4

---

## 正则表达式(regular expression)

两种创建方式：  
```js
const regexp1 = new RegExp('12','g');  
const regexp2 = /12/g;  //不适用于要用到变量，但是适用于有转义的，主要因为字符不加引号。  
```
- g:全局匹配  。查找所有的匹配而非在找到第一个匹配后就停止；  
- i:不分大小写；  
- m:多行匹配；

---
- 用选择'或'|时 ，要用（）分组将所有的内容括起来；
- \$ 符号表示这个字符串的结束,并不是从字符最后面开始匹配.  
/^1\d{1}$/ 表示匹配以1开始的任意两位数(因为匹配完一位数字后,就表示要匹配的字符串结束了),而不是123这种还要从后面来匹配一次。

- \u4e00-\u9fa5表示在unicode表中的第一个汉字和最后一个汉字  
\un:匹配n，其中n是一个用四个十六进制数字表示的Unicode字符。例如，\u00A9匹配版权符号（©）。

- 多种字符的匹配或：[0-9a-zA-Z]。  
[025]:表示匹配数字0，2，5。

- {} {n} 匹配n次；{n,} 最少匹配n次；{n,m} 最少 n次 最多 m次

- \s: 匹配任何空白字符，包括空格、制表符、换页符等等; \S: 非空白字符

---
var str = 'a123'
- /a(?:1)/.exec(str) 匹配返回的结果是：a1
- /a(?=1)/.exec(str) 匹配返回的结果是：a
- /a(?!2)/.exec(str) 匹配返回的结果是：a

- /(?<=1)2/.exec(str) 匹配返回的结果是：2
- /a(?<!a)2/.exec(str) 匹配返回的结果是：2

都为非捕获

---
- \b:匹配单词边界
- \d：匹配数字。  
- .：表示匹配单个字符，除了换行和结束。  
- \s：表示匹配空格

---
RegExpObject.exec(字符串)：  

没有匹配值返回null，并把lastIndex（属于RegExpObject）置为0； 

当没有用到分组时，返回的数组只有匹配到的第一个字符串，若分组再依次返回分组。

当使用了RegExpObject匹配了一次，必须把RegExpObject的lastIndex重新 

置为0，不然它会从新的字符串的lastIndex位开始匹配；（全局模式下）  

非全局模式下，与match()方法返回结果一样；  

exec()还会返回两个属性，index（匹配字符的起始下标），input（被匹配的
字符串）  

全局模式下用循环只要返回的不是null就一直循环匹配；这种方法获取的信息是最全的，因为每一个匹配值的位置等都有，但match()只返回一个数组；  

RegExp.test()    检测到有就返回true

---

## Object

```javascript
let {keys,values,entries}=Object;//返回的都是数组
let obj = { a: 1, b: 2, c: 3 };
for(let [key,value] of entries(obj){
    console.log([key, value]);
} // ['a', 1], ['b', 2], ['c', 3];
```

### call() || apply() || bind()
前两者用法一样，除了传参方式  

用法如下：
```javascript
// 1.子构造函数调用父构造函数的方法
function Fn(name, age) {
	this.name = name;
    this.age = age;
}
function F1(name, age, num) {
    //让Fn内部的this指向F1的实例对象,由于执行了Fn(),所以给实例对象也绑定了Fn中的属性
    Fn.call(this, name, age); 
    this.num = num;
}

var f1 = new F1(1, 2, 3)

console.log(f1.name, f1.age, f1.num); // 1，2，3

// 2.调用函数并指定上下文‘this’
var obj={name:1,age:2};
function f2(){
	console.log('other',this.name,this.age);
}
f2.call(obj); // other 1 2

// 3.使用apply和内置函数
Math.min.apply(null,[100,2,3])  // 返回 2
Math.max.apply(null|Math,[1,2,3]) // 返回3

Array.prototype.push.apply(array1, array2);
```

**bind(Object,args,args…)**  
> 会创建一个新函数，第一个参数将作为它运行时的this。

bind 是返回对应函数，便于之后调用；apply 、call 则是立即调用 。

```javascript
var module = { x: 81,getX: function(a,b) { return this.x+a+b; }};
retrieveX=function(a,b){ return this.x+a+b; }
var boundGetX = retrieveX.bind(module,8,1);
boundGetX();  //90
```

### 继承
```javascript
function Fn(name){
	this.name=name;
	this.type='test'
}
Fn.prototype.do=function(some){
	console.log('do:'+some);
}

function F1(name){
	Fn.call(this,name);//不会继承原型方法
}
F1.prototype=Object.create(Fn.prototype)||new Fn(); // 用原型即可以不用重复声明函数
F1.prototype.way=function(way){
	console.log(way)
}

var f1=new F1('koko');
console.log(f1.name);
f1.do('what')
f1.way('what way');
```

### 面向对象的实现方式
```javascript
// 链式方法 
function Name() { }
Name.prototype = { f1: function (){console.log('f1'); return this; }, f2: function () {console.log('f2');return this;}}
var n = new Name();
n.f1().f2()
//还可以用构造函数的方式


//工厂模式
function createBlog(name, url) {
  var o = {};
  o.name = name;
  o.url = url;
  return o;
}

//构造模式
function Blog(name, url) {
  this.name = name;
  this.url = url;
}

//原型模式
function Blog() {}
Blog.prototype.name = 'wuyuchang';//只能这样创建
Blog.prototype.url = 'http://tools.jb51.net/';
Blog.prototype.friend = ['fr1', 'fr2', 'fr3', 'fr4'];
```
---
navigate.appName/userAgent/appVersion/platform  
IE:trident(-ms-);  
Firefox:gecko(-moz-);  
Chrome:webkit(-webkit-)  
Opera:presto(-o-)  
window.top.document.compatMode;返回模式（标准和怪异）

---
location.reload():当参数为false（默认）如果文档没有改变就从缓存中去取，如果改变就在此下载该文档；当参数为true，直接从服务器重新下载该文档。

---
 **三个方法将非数值转换为数值**  
Number(参数);参数可以是(如new Date()或new Boolean());Number('123')//123  
parseInt(被解析字符串【该参数会被强制转化为字符串】【注意科学计数法】,进制默认10进制)  
parseInt(0.0000008) === 8  //true

parseFloat(一个参数);  
NumberObject.toFixed(n);n为0到20之间值(用Number(参数)来创建数值对象，不推荐用new Number())    
Number(15.265124).toFixed(2) //15.27 四舍五入  

---
document.documentElement:获取HTML元素对象  
document.body:获取body节点对象  
document.doctype获取< !DOCTYPE>    
document.title='name'获取或更改title标签值  
document.URL获取URL  
document.domain获取域名（服务器端）  
document.referrer获取上一个URL(服务器端)  
document.forms  返回文档中的所有Form对象引用  
document.domain  获取域名不带端口

HTML DOM location对象的search属性可以设置或是返回当前URL的？及之后的字符串。  
设置或是获取URL：window.location.href;//设置即会跳转页面  
设置或是获取与URL关联的端口号:window.location.port  
设置或是获取与URL的协议部分:window.location.protocol  
设置或是获取与URL的#号后面的分段: window.location.hash  
设置或获取hostname 和 port 号码：window.location.host/hostname(不包含端口)  //与 获取值一样

获取url中的参数:
``` javascript
function getURLParameter(url,name){
        var regexp=new RegExp('(^|&amp;)'+name+'=([^&amp;]\*)(&amp;|$)','i');
        return url.substr(1).match(regexp)[2];
}
getURLParameter('?name=b&amp;password=d','password')
```

---
- 要判断的值 instanceof Array|String   返回true或false
- typeof 'a'=="string"  返回true或false  
 [1,2] instanceof Array

---
option标签在谷歌和ie低版本上是没有click事件的，一般对select都是用change事件；  
获取option的value和text用  
selectObj=document.getElementById('select');  
selectObj.value;  selectObj.options[selectObj.selectedIndex].text;
1. 可以直接获取到select对象执行以上操作；  
2. 事件中用this替代selectObj 即可；  
3. $(selectID).find("option:selected").text()  

---
火狐中是没有innerText，可以用textContent来代替（DOM3的标准）其它的浏览器也可以支持。

---
null:没有对象  
undefined:表示缺少值（声明了变量但没有被赋值；调用函数时，应该提供的参数没有提  供，该参数返回undefined；对象没有赋值的属性；函数没有返回值时；）

---

### Math对象
Math.abs(X):返回X的绝对值；  
Math.ceil(X):上舍入；  
Math.floor(X):下舍入；  
Math.round(X):四舍五入；  
Math.pow(X，y):x的y次方；  
Math.random():返回0到1之间的随机数  
Math.sin(以弧度表示的角度)：（2*PI/360）度数，就是弧度

### Date对象
- UTC 世界同一时间 || GMT 格林尼治标准时间 ：返回值相同。GMT 是一个时区，而 UTC 是一个时间标准。  
- Date()方法:不接受参数，  
  alert(Date())返回当前日期和时间字符串；  
- 创建Date对象的方法:new Date() 返回当前日期和时间  

new Date(毫秒数) 可以带毫秒数的参数，返回日期；这个毫秒数是1970年1月1日到返回日期之间的毫秒时间；  
new Date(‘October 13, 1975 11:13:00’)；  
new Date(‘2016-05-13T11:13:00’)；  
new Date(‘2016-05-13 11:13:00’);//在ios系统中可能报错    
new Date(‘2016/05/13 11:13:00’)；  
new Date(year, month, day, hours, minutes, seconds, milliseconds)  
参数可以不写全，但是最好是后面的参数不写全；也可以是放Date对象的字符串形式。 

- var d=new Date();返回的是对象  
d.getTime();指定的日期和时间距 1970 年 1 月 1 日午夜（GMT 时间）之间的毫秒数    

Date.parse(‘October 13, 1975 11:13:00’)||(d);   
 
这里可以用d当作参数的原因是d会自执行一下返回一个 datestring  

是Date对象的静态方法，不需要用dateObject(就是new出来的d).parse来调用     
    
var d=new Date() d.toISOString()。//2017-01-09T06:19:11.004Z     

- new Date(+new Date()+8*3600*1000).toISOString()  返回正确的时区时间，valueOf() 方法返回一个 Date 对象的原始值，等同于getTime() 。+操作是将该元素转换为number类型，转换不了就返回NaN。

- 时间大小比较（采用如下的js中的方法获取毫秒数来比较，不要直接比较，直接比较为错误方法）

```js
var d = new Date('2018-04-03T16:40:00'); 
console.log(d.getTime())
console.log(d.valueOf())
console.log(Date.parse('date string'))
console.log(Date.now())
console.log(Date.UTC(2018, 3, 3, 8, 40, 0))
// 当给定的时间一样，返回值相同
```


## 循环
---
```
for(var 变量 in 对象名 ){  
    alert(变量) //返回对象键值对中的属性名  
    alert(对象名[变量])  //返回该变量对应的属性值  
}  
for(var 变量 in 数组名 ){  //不推荐
    alert(变量) //返回数组下标  
    alert(数组名[变量])  //返回对应下标的数组值  
}  
for...in 遍历（当前对象及其原型上的）每一个属性名称,而 for...of遍历（当前对象上的）每一个属性值  

for...of  不可以遍历对象{a:1,b:2} 因为原生对象不具有 Iterator 接口
```
---
in 的用法  
判断数组是否有该索引  
alert(1 in array)  //这里的1表示下标  
判断某一属性是否在该对象中  
alert('name' in  Object)   //'name'表示属性名称  

---
**switch**  
- 用命令对象来替换switch
```javascript
function swichFn(n){
    let tempObject={
        '1':function(){alert(1)}
    }
    if(typeof tempObject[n] !== 'function' ) return false ;
    return tempObject[n]();
}

swichFn('1');
```

- 用查表法来替代switch
```javascript
let result=[0,1,2,3,4]
return result[value]
```

## 事件
### 事件说明
- oninput:在 < input> 或 < textarea> 元素的值发生变化时立即触发。  

- onchange:值有改变时，在元素失去焦点时触发。  

- onblur:只要失去焦点就触发。

- 支持onload的标签 < body>, < frame>, < frameset>, < iframe>, < img>, < input type="image">, < link>, < script>, < style>

- onscroll 事件 对div window都兼容; document，document.body,  document.documentElement 存在兼容问题 http://www.w3help.org/zh-cn/causes/SD9013

- '< div onclick="fn(\''+ param +'\')"></ div>' 内联事件传字符串需加引号并转义

### 事件移除
document.getElementById('id').removeEventListener('click',fn,false);  
这里必须写成fn的函数调用，因为要与添加事件时的函数为同一个函数。  
document.getElementById('id').onclick=function(){};  
document.getElementById('id').onclick=null;  
$('#').unbind('事件名称');参数可选

### JS鼠标事件获取坐标
clientX/Y:  
触发点相对浏览器可视区域左上角距离，不随页面滚动而改变;浏览器都支持;  
pageX/Y:  
触发点相对文档区域左上角距离，不会随着页面滚动而改变,除IE6/7/8不支持外，其余浏览器均支持;  
offsetX/Y,layerX/Y  
firefox的event不支持offsetX(新版的是支持的)（相对于元素的内边距）属性，但是提供了layerX(相对于元素的外边距),如果设置了position为相对/绝对定位就相等。
IE所有版本，chrome，Safari均完美支持，Firefox不支持最新版支持
IE6/7/8不支持，opera不支持，IE9/10和Chrome、Safari均支持
screenX/Y  
触发点相对显示器屏幕左上角的距离，不随页面滚动而改变  
所有浏览器均支持;  
Event.x/y相对于css中的绝对定位的位置，不会随滚动条的改变而改变。火狐不支持但有等效的pageX。

### querySelector
querySelectorAll 返回的是一个 Static Node List(是一次对文档的快照，若是该快照下对文档有什么更改不会影响本次操作);  
document.querySelectorAll('选择符')：返回匹配元素集合。  
document.querySelector ('选择符')：返回匹配第一个元素。  
而 getElementsBy 系列的返回的是一个 Live Node List：  
var ul = document.getElementsByTagName('ul')[0],  
     lis = ul.getElementsByTagName("li");  
for(var i = 0; i < lis.length ; i++){   //这里就是lis.length在一直变化  
    ul.appendChild(document.createElement("li"));  
}  
每一次调用lis都会去遍历一下文档，最终会无限循环。  

HTMLCollection 和 NodeList 十分相似，都是一个动态的元素集合，每次访问都需要重新对文档进行查询。两者的本质上差别在于，HTMLCollection 是属于 Document Object Model HTML 规范，而 NodeList 属于 Document Object Model Core 规范。
所以在现代浏览器中，querySelectorAll 的返回值是一个静态的 NodeList 对象，而 getElementsBy 系列的返回值实际上是一个 HTMLCollection 对象 。

---
onunload和onbeforeunload事件  
最好body上添加事件  
onunload和一般的事件一样  
onbeforeunload:  
function a(){  
   return '返回文字'  
}  
< body onbeforeunload="return a()">  
Window||document.body.onbeforeunload=function(e){  
    e.returnValue='返回文字'  
}  
或是用addEventListener同样用returnValue

---

### window.onerror
 function(message, source(文件), lineno(行), colno(列), error) { ... }

## Array
**伪数组**

Javascript中存在一种名为伪数组的对象结构。比较特别的是 arguments 对象，还有像调用 getElementsByTagName ,document.childNodes之类的，它们返回NodeList对象都属于伪数组。不能应用 Array下的 push , pop 等方法。

**Array.prototype.slice.call(arguments) || [].slice.call(arguments)**
```js
const obj={length:2,0:'first',1:'second'};
Array.prototype.slice.call(obj);//  ["first", "second"]
```

---

### filter/map/forEach/some/every/find/findIndex
- filter返回新的数组
- map会返回新数组  
- console.log(arr.forEach(function(v){console.log('v',v)}));//返回undefind
- map 和 set 有 forEach 方法可以用

- some 有返回值， some 的回调函数有一个返回 true，则返回true, 有true返回则结束循环
- every 有返回值， some 的回调函数每一个返回 true，则返回true, 有false返回则结束循环

- find 返回第一个符合的值
- findIndex 返回第一个符合的值的数组下标 与 indexOf 区别为传入的参数，前者为函数

- includes: [].includes('some value') // return true/false ,与indexOf相比，可以避免返回的0，判断时的错误

### 数组去重
https://gist.github.com/NameHewei/b4cc79f09be425097a994fae4d9ed22e

---
a[i++];先执行a[i]，再i++

---
$.inArray(值，数组，从数组哪里开始);判断该值在数组中是否存在，返回索引值，无就返回-1；

---
splice(x,y,z1,z2,z3,z4....):会直接对当前数组进行修改；  
取出从下标为x（下标从0开始）开始的y个数组值，进行修改；  
z参数不加：就删除数组中的这几个数；相当于用空来替换这些数  
y参数为0：在x前面插入z； 
y参数为1：将x替换为z；  
该方法返回被删的数组值；

---
slice(start,end)(字符串也有这个方法，用法相同):会返回一个新的数组；不对原数组进行修改;

start||end=-1表示最后一个元素。  
'abcdef'.slice(0,-2)      //'abcde'  
'abcdef'.slice(-2,-1)    
start和end都为下标（下标从0开始）；返回包含下标start但不包含下标end的数组；

---
array.join('!');将数组的每个元素放到一个字符串中，不传参就用逗号隔开(此时与toString()方法一样),传就用该符号。  
array.push(参数);末尾压栈，返回数组长度；通过索引值来添加比push方法更快  
array.pop();末尾出栈，返回去掉的值；  
array.shift(),对头出栈，返回去掉的值；  
array.unshift(),对头入栈，返回数组长度；

array.reverse();逆向排序的数组  

``` javascript
const arr = [1,55,6,2]
function compare(a,b) { 
    // 这里是从大到小排列
    if (a > b) {
        return -1; 
    }else if(a < b) {
        return 1; 
    }else{
        return 0;
    }
}
// compare(a,b) 重点关注返回值即刻
// 返回0 位置不变
// 返回-1 a放到b之前（这里输入a，b参数不代表a就在b之前）
// 返回1 a放到b之后
arr.sort(compare);
// 默认小到大排列（即没有compare函数）按照数组元素对应的字符串的 Unicode 从小到大进行排序。  

// 比较数字可以简单的使用(升序)
function compareNumber(a,b) { 
    return a - b
}
```

**reverse和sort都不返回新数组，且都是对数组才能操作**

arrayA.concat(arrayB);返回拼接后的数组

var newArray = [].concat(arr1,arr2,arr3)

---

## Function

- 一般的函数调用都是同步
```js
function ss() {
	var i=0;
	while(i<10000000000){
		i++
	}
	console.log(12)
}
function bb() {
    console.log(34)
}
ss()
bb()
// 先返回12，再返回34
```

- 异步编程
  1. 函数回调
  2. 事件监听
  3. Promises
  4. generator(ES6)
  5. async/await(ES7)
  6. 发布/订阅, 将订阅的回调函数，循环的去执行

---
### 高阶函数
满足：接收函数作为参数或输出一个函数

---
- Function()构造函数   
函数实际上是功能完整的对象 。Function类可以表示开发者定义的任何函数。用Function类直接创建函数的语法如下：   
var function_name = new Function(arg1, arg2, ..., argN, function_body)   
参数必须是字符串,最后一个参数是函数主体（要执行的代码）

---
- 变量提升
1. 变量提升，很简单，就是把变量提升提到函数的top的地方  
    (function(){  
        alert(a);  // undefind  
        var a=12;  
    })()   
2. 函数提升，把整个函数都提到前面去，只用声明函数可以提升，表达式函数不能   
  function a() {  b();  //可以执行  function b(){} }
3. let 不会变量提升；作用域是块级；不允许同一域重复声明；
---

自执行函数  
（function（）{}（））和（function（）{}）（）  
(()=&gt;{})() 只有这一种  
闭包  
销毁 函数名=null

!function(){}()  
感叹号将函数变为了函数表达式，也可用+-||等代

---
构造：
``` javascript
function A(){
   var a1=1;//私有属性
   this.a2=2;//公有属性
   this.aaa=function(){
    alert(a1);//在实例化中是可以访问该私有属性的
	}
}
```
A.a3=3;//静态属性，在构造实例的时候，实例是不能访问的，只有用访问构造函数的该属性才可以，实例名.constructor.属性名。  

**this指向**
- this指的是调用函数的对象。  
- 在函数中用this设置的属性只有在实例化后才能调用。但是在外部用prototype设置的属性可以用prototype来调用。  
- 当构造函数没有返回对象时，会默认返回this,当返回了其它的除变量外，也会默认返回当前构造函数的this。  
- 当参数是匿名函数时，属于全局调用，所以调用对象是window，如setTimeout（function（）{}，1000）。


## String
字符串存储的大小：理论最大长度是2^53-1

数字 Number 的最大最小范围：Number.MAX_VALUE Number.MIN_VALUE

Number类型统一按浮点数处理，64位存储，整数是按最大54位来算最大最小数的，否则会丧失精度；某些操作（如数组索引还有位操作）按32位处理

- 字符串之间不能用三元运算符来拼接
```js
var str = '<div class="d-p-people">'+n===1?n:2+'</div>'  
```

- substring(start,end)  
若end比start小，会先交换这两个参数，若有负数变为0。 

- "Hello world!".charAt(1)  //e 

---
当字符数少，且连接数量小于1000时就可以用"+"来连接字符串即可，若是过大，就用数组的join方式来连接，主要是考虑到老浏览器的速度比较慢；

---
toLocaleLowerCase()和toLowerCase()区别主要是前者会根据地区的语言环境来进行编码。toUpperCase()

---
字符串中可以用正则表达式的方法：  
1. str.match();  
不设置全局，只返回第一个匹配值,并且返回子表达式的值。和属性index,input。  
设置全局，只返回所有的匹配值，不返回子表达式的值。  
var str='name=hew;a=c;name=hi';  
console.log(str.match(/name=([^;]+)(;|$)/g))  
//返回 ["name=hew;", "name=hi"]  

2. str.search();  //返回匹配字符开始的位置，没有返回-1  
3. str.replace(字符|正则，替换值|函数);  函数返回值为替代值，当用字符时  
不是全局替换，函数第一个参数为匹配结果字符，然后依次是子表达式值…,出  
现位置，被匹配字符串。  
4. str.split();   //以传入的字符或正则匹配的字符分割成数组，并删除改字符  
5. substr

## 其它
### 浏览器窗口尺寸
1. 对于Internet Explorer、Chrome、Firefox、Opera 以及 Safari：  
window.innerHeight | innerWidth - 浏览器窗口的内部高度  
2. 对于 Internet Explorer 8、7、6、5：  
document.documentElement.clientHeight | clientWidth 或者 document.body.clientHeight | clientWidth

### iframe
- 在chrome中window.parent.document 要在服务器上才能使用。
- window.parent.document.getElementById();
- 获取当前的内嵌页面url,就直接在该页面使用window.location.href即可。
- 父页面查找子页面的元素：
- document.getElementById('iframeId').contentWindow.document||document.body||document.getElementById('子页面ID')；
- 子页面查找父页面元素。
- 不同域可以在两个页面都设置document.domain='主域名'。
- html5新方法，在父窗口使用document.getElementById('iframeId').contentWindow.postmessage('')在iframe中使用
- window.onmessage=function(e){e.data}

# es6

## 字符串

${${}}  //能嵌套

**字符串方法**

>repeat(n):字符串重复次数
- n.123 //取整
- -1<你<0  //取0
- n=NaN  //取0
- n=字符串  //转换为数字
- n=负数（-1等）或Infinity  //报错

---
includes(), startsWith(), endsWith()  //都返回boolean值

---
padStart(字符串长度，用来补齐的字符串：默认用空格)，padEnd() ：字符串补齐

---
trim():去掉换行

### 标签模板
```js
const str = `a${12}b${34}`
const fn = () => {}
// 函数方式调用
fn`str` 
// 相当于fn(['a','b',''], 12, 34)
```

## class

类的所有方法都是定义在类的prototype上

在方法前加 static  只能通过类来调用 不能被子类继承（静态方法）,静态方法中的this指向类而非实例

### 继承
super ：表示父类的构造函数，用来新建父类的this对象

子类必须在 constructor 方法中调用super方法，否则新建实例时会报错。这是因为子类没有自己的this对象，而是继承父类的this对象，然后对其进行加工。如果不调用super方法，子类就得不到this对象。constructor 中this指向实例

ES6 的继承机制，先创造父类的实例对象this（所以必须先调用super方法），然后再用子类的构造函数修改this

## Promise
> 一种异步编程解决方案，语法上是一个对象。

1. 三种状态Pending，Resolve，Rejected   
2. var promise=new Promise(function(resolve,reject){})。   
resolve和reject由js引擎提供。    
resolve将Promise对象的状态从“未完成”变为“成功”    
reject将Promise对象的状态从“未完成”变为“失败”  

3. promise.then(function(value){//success}), function(value){//failure});   
then()方法作用是：为Promise实例添加状态改变时的回调函数，分别为resolve和reject指定回掉方法。   
Promise.prototype.then()。  
then()中返回的值将会被作为参数传递给下一个then(),**如果上一个then返回的是一个Promise对象**，这时后一个回调函数(即then)，会等待该Promise的状态改变来调用回调函数。
4. catch()  
Promise对象的错误具有冒泡性质，会一直向后传递，直到被捕获为止。     
一般来说，不要在then中定义使用Reject状态的回调函数，而是用catch。

---
对象方法简写  
{  
a(){}   //等同于a:function(){}，而非箭头函数  
}

---
Set: 和数组类似但是，但是成员唯一。  
var set=new Set(参数)   //这里的参数可以是数组或类似数组的对象{0:'a',1:'b',2:'c'}。  
在set内部两个NAN是相等的，两个对象总是不等的。  
四个方法：  
add(value): 添加值               //返回set结构本身  
delete(value): 删除值             //返回布尔值，表示是否成功  
has(value):检测是否为set成员     //返回布尔值  
clear():清除所有成员             //没有返回值  
还有一个weakset与之类似  
Map:也是键值对的形式的，但是键的形式不只是字符。  
同样有一个weakmap。

---
let 是块作用域，一个函数或一个for或if语句中； 
const 常量索引 只可以在声明的时候赋值 变量名在内存中的指针不会变，但是指向这个变量的值可以变  

---
## 函数

---
函数式编程
1. 不用var
2. 没有for循环（filter map reduce）
3. 简化if，三元运算（抽离逻辑放到函数中）
4. 不用switch
5. 不再担心this

---
function a(b,c=1){}

- 定义了默认值的参数，应该是函数的尾参数,非尾部的参数设置默认值，实际上这个参数是没法省略的,除非用undefined代替，以触发该参数等于默认值。
- 设置了参数的默认值，函数进行声明初始化时，参数会形成一个单独的作用域（context）。初始化结束，作用域消失。不设置参数默认值时，不会出现的。

---
(param,..)=>{}  
- 不支持new方法。  
- 不会改变指向对象（例如call，apply方法）  
- 箭头函数没有它自己的this值，它内部的this继承自外层作用域(箭头函数绑定父级上下文)，但是function函数是无论你需不需要都会自动接收一个this，  
- 在定义对象方法的时候必须用非箭头函数定义，这些函数会从调用者的作用域获取一个有意义的this
- 内部的this 总是指向函数定义生效时所在的对象，而不是指向运行时所在的作用域。  

a={  
    name:()=&gt;{this}  //这里的this指window，类似匿名函数  
}

## …相关
展开运算符  
多个参数（用于函数调用）或者多个元素（用于数组字面量(直接使用的数据值如1,2)）或者多个变量（用于解构赋值）。  
(  
var args=[1,2,3]  
var fn=function(){};  
fn(…args);  
)  
(  
a=[1,2,3];  
arr[0,…a,4]  
var arr1 = [0, 1, 2];  
var arr2 = [3, 4, 5];  
arr1.push(...arr2);  
)  

---
解构  
数组解构  
var [foo, [[bar], baz]] = [1, [[2], 3]];  
var [,,third] = ["foo", "bar", "baz"];  
对象解构  
把属性值赋给某个变量  
var { foo:*foos*, bar:*bar* } = { foo: "lorem", bar: "ipsum" };//斜体为变量  
console.log(foos) //lorem   
当变量名和后面属性名一致时可以简化  
var { foo, bar } = { foo: "lorem", bar: "ipsum" };

{...Object1,...Object2}:后一个对象的属性会覆盖前一个对象的相同属性  
详见es6 Object.assign() 用法

---
剩余操作符（the rest operator）  
var [a,…b]=[1,2,3,4];  
console.log(a)  //1  
console.log(b)  //[2,3,4] 

---
用...[1,2,3]替代apply方法来给函数传参
```js
function f(x,y,z){
    console.log(`${x}-${y}-${z}`);
}
let ar=[1,2,3];
f.apply(null,ar);
f(...ar);
```

---

## 模块功能
ES6 的模块自动采用严格模式，不管你有没有在模块头部加上"use strict";。  
- es6 模块不是对象  而是通过export输出的代码
- es6 模块是在编译时加载
- export var m=1 ;export function f(){};(正确);  
  var m=1;export m;(错误)  
  注意与内部变量建立一一对应关系.  
  推荐用法 export {m,f};  
  var n = 1;  
  export {n as m};  
- export 命名可以出现在任何位置，必须是模块顶层。

- 引入的同一个模块，如果不做拷贝，当修改其原始值时，会影响所有引用该模块的地方

---
export 与 export default 的区别在于import的时候是不是需要用{}，后者不用。

---
- import '模块名' // 表示引入并执行该模块，多次重复调用只执行一次
- import 后的文件位置的.js可以省略
- 由于import是静态执行，所以不能使用表达式和变量，这些只有在运行时才能得到结果的语法结构。

---
整体加载
- import * as **obj** from 'somefile';(被引入文件是输出多个export，通过该方法集合为一个对象)
- 是可以静态分析的，所以不允许运行时改变
- 允许 obj= 'hello';

---
export default
 - 因为多了个default  所以可以理解为将default与模块内部的变量进行了对应 。
 - 正确写法 ：var m=9；export default m;
    错误写法：export default var m=9;
- function add(x, y) {  
  return x * y;  
}  
export {add as default};  
// 等同于  
// export default add;     
引用  
import { default as xxx } from 'modules';  
// 等同于  
// import xxx from 'modules';

---
在 export 文件中有如下

export default function() {}

export const each =function() {}

在 import 文件中

import 同时引入： import a, { each } from 'export文件';

---

扩展运算符内部调用的是数据结构的 Iterator 接口，因此只要具有 Iterator 接口的对象，都可以使用扩展运算符

---

## 函数扩展
1. 尾递归（只存在一个帧调用，所以效率高，不会出现栈溢出的情况）

## 数组的扩展
1. 扩展运算符与函数参数结合
2. 当参数是数组时不再依赖apply拆分数组为参数
3. 任何 Iterator 接口的对象，都可以通过...扩展运算符转为真正的数组

## Proxy defineProperty defineProperties
'拦截'对目标对象的访问

> Proxy(target,handler)

target：要拦截的对象

handler：值为对象，拦截行为

Proxy 是针对Proxy实例的，并不针对目标对象(target)

如果handler不设拦截，访问proxy就等同与 target

```js
const target = {
    name: 'hew'
}
const handler = {
    // 三个参数，receiver表示操作行为所针对的对象，一般就是proxy实例
    get(target,key,receiver){
        if(key in target) {
            return target[key]
        } else {
            throw new ReferenceError(`${key}, does not exist`)
        }
    },
    // 严格模式下，如果没有返回true会报错
    // 如果目标对象的属性为writadble，那相对于该属性，set方法失效
    set(target, key, value) {
        if (key === 'age') {
            if(!Number.isInteger(value)) throw new TypeError('is not integer')
            if(value>10) throw new RangeError('need less than 10')
        }

        target[key] = value
    },

    // 拦截函数的调用，call，apply操作
    apply(target, ctx, args) {
        return args
    },

    deleteProperty(target, key) {
        console.log('delete', key);
        delete target[key]
        return true
    }
}

const proxy = new Proxy(target, handler)
console.log(proxy);
```

Object.create(proto, [propertiesObject])

# Object.create(proto, [propertiesObject])

proto: 新对象的__proto__

propertiesObject：可选参数，添加到原型上的枚举属性，以及这些属性的描述，名称等，且对应Object.defineProperties()的第二个参数

返回值：指定了原型对象和属性的新对象
```js
const a = Object.create({
    name: 'hew'
}, {
    age: {
        set(value){
            console.log("can't set", value);
            return value
        },
        get() {
            return 250
        }
    }
})
a.age=12
console.log(a.age);
```

```js
Object.defineProperty(obj, 属性名称, descriptor),在现有对象上新建一个属性，或修改现有属性，并返回这个对象
Object.defineProperties(obj, props)
props: {
    property: descriptor
}
descriptor: {
    configurable: 默认false；表示属性是否能删除，以及除writeable以外的属性可否被修改；
    writable: 默认true；属性值可否被修改
    enumerable: 默认true 属性是否可以被for...in和Object.keys()获取
    value: 属性值
    get() {}
    set() {}  当设置了get或set后不能设置value或writeable
}
```

Proxy 与 Object.defineProperty 对比

Object.defineProperty

- 只能对属性进行数据劫持，所以需要深度遍历整个对象

- 对于数组不能监听到数据的变化

---

# ES7-ES8

## es7

- includes：参考上文

- 求幂 Math.pow() 的简洁写法 ** 
Math.pow(3, 3) === 3 ** 3

## es8
- String.prototype.padStart(总长度, 被填充字符串) // 返回新的字符串 
'789'.padStart(10, '123')  // "1231231789"

- String.prototype.padEnd(总长度, 被填充字符串)
'123'.padEnd(5, '789')  // "12378"

- Object.entries()
Object.entries({ a: 1, b: 2 }) // [['a', 1], ['b', 2]]

- Object.values()

- 异步函数 async/await 

- Object.getOwnPropertyDescriptors

## es2019

- 展平数组

flat(展平层级:数字(默认1)或Infinity)  会过滤数组中的空值 返回新数组

flatMap(() => {}): 对原数组执行一个map操作，然后再执行flat 只能展开一层数组  返回新数组

- Object.fromEntries() 将键值对数组转换为对象

```js
Object.fromEntries([['name', 'hew']])

Object.fromEntries(new Map([['name', 'hew'], ['scope', '12']]))  // {name: 'hew', scope: '12'}

Object.fromEntries(new URLSearchParams('name=hew&scope=12')) // {name: 'hew', scope: '12'}
```

- 删除字符串开头的空格

' abcdefg'.trimStart() 同 trimLeft()

'abcdefg  '.trimEnd() 同 trimRight()


- try catch 中 catch的参数可以省略

- Symble 加了一个description的只读属性 返回描述

