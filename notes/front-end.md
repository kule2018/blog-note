[toc]
# 内核
ie **trident** || chrome，Safari **webkit** || firefox **gecko** || Opera **presto**  
chrome Opera 现在： Blink(基于webkit，Google与Opera Software共同开发)

# 兼容性
1. < !--[if IE]> 所有的IE可识别 <![endif]-- >   
    < !--[if lt IE 9]> IE9以下版本可识别 <![endif]-->   
	**ie10及以上无效**

# 行内元素
宽高无效 。margin,padding上下无效

# 清除浮动
- div style="clear:both;"//左侧和右侧  
- parent:after{ content:"."; height:0; visibility:hidden;display:block;
clear:both;}
- 给包含浮动元素的父标签添加css属性 overflow:auto; zoom:1; zoom:1用于兼容IE6。

# undefined || not defined || null
var x; // 声明 x     
console.log(x); //output: undefined  
console.log(z); // 抛出异常: ReferenceError: z is not defined

---
typeof null //object  
null是一个表示"无"的对象，转为数值时为0；undefined是一个表示"无"的原始值，转为数值时为NaN。  
var a; Number(a); //NaN  
5 + undefined ;//NaN  
基本是同义的，null表示"没有对象"，即该处不应该有值。  
null 表示一个值被定义了，定义为“空值”；  
undefined 表示根本不存在定义。  
所以设置一个值为 null 是合理的，如  
objA.valueA = null;  
但设置一个值为 undefined 是不合理的  

# 事件
>任意事件触发后三个阶段：捕获，目标，冒泡。addeventListener(,,false默认(冒泡阶段执行)||true)

>attachEvent('onclick',function(){}) //兼容ie8   
addeventListener('click',function(){},false) //w3c

# event对象
1. event.stopPropagation传播():阻止事件传递(相同)，不管是冒泡还是捕获；IE8以及以下版本用event.cancelBubble冒泡 =true;
2. event.target   返回触发此事件的元素(可用于事件委托),IE下是event.srcElement;
3. 添加的事件函数中用return false来实现stopPropagation()和preventDefault()的功能。

# 事件委托优缺点
1. 节省内存，减少事件注册。
2. 子对象动态绑定。
3. 若把所有事件用代理方式容易出现误判。

# cookie
删除 同名加max-age=0

# 提升用户体验
**ajax** ：表单验证时的实时验证，局部的dom改写。  
**字体** ：不同的字体会影响用户对站点权威性的信赖程度  
**加载速度**  ：  
1. 如今大多数浏览器在下载css/js时是并行的，但是单线程运行js的，这也就意味着一个js文件在被解析的同时浏览器不能对任何事件做出响应，直到浏览器弄明白这个js是干什么的才会转向下一个js文件；所以将js文件放尾部，优先下载了html/css等文件，这样会给用户一些错觉，认为网站已经加载。加载js时候会阻塞浏览器的渲染操作。window的onload方法里面执行添加script标签。
2. 保证代码的规范性避免404页面，保证每个资源能够正常加载。
3. 一个页面中如果频繁出现向其他域名请求数据，而且使用的是域名，则会出现频繁的DNS解析。
4. 公共库cdn资源，当其他网站也，使得很多访客的缓存中已经存在这些公共库的资源。第二张页面时，如果使用的是同一个外部css/js文件

**页面解构设计**
**细节**

# 内存泄漏
1. 全局变量不会被回收（除了退出浏览器），函数运行完之后，运行函数的内存区被回收。
2. 闭包。
3. DOM被删除或清空时，事件未清除导致的内存泄漏。
避免使用全局变量和函数  
var myvar = 0; // 336ms window.myvar = 0; // 2383ms  
var myfunc = function(){} // 3515ms window.myfunc = function(){} // 10151ms  
避免用new创建函数和数组；  
用对象方式比数组方式更快一点  
a[i] = value; // 1270ms obj[property] = value; // 960ms  

# 算法题
