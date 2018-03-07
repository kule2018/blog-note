[toc]

## Tips
1. 基于ECharts4.0

    1. 移动平台优选 SVG
    2. 图表个数很多时优选 SVG
    3. 导出小文件高清晰时使用 SVG
    4. 数据量特别大时推荐使用 Canvas 渲染

# canvas
- 在设置canvas标签的宽高时，要直接在标签上给设置（width=“100px”）
- getContext() 方法返回一个用于在画布上绘图的环境；现在只有“2d”;
- 渐变的效果发生在所规定的坐标之间，之外的就会用相应的纯色填充。
- .save()和.restore()之间定义的方法或定义只作用于他们之间
- 用drawImage的时候要注意图片是不是已经加载了
    参数形式可以是：
    1.（imgObj，相对画布x位置，相对画布y位置）；
    2.（imgObj, 相对画布x位置，相对画布y位置,图宽，图高）；
    3.（imgObj, 图像x位置，图像y位置,裁切图的宽度，裁切图的高度,
    相对画布x位置，相对画布y位置,被裁图宽，被裁图高
    ）

# svg

# fetch
```
fetch('http://localhost:1025/121', {
        credentials(凭证):'include',
        headers: { 'Content-Type': 'image/jpeg|application/json' }, 
        method: 'get',
        mode: "cors",
    }).then(function (res) {
        return res.text()||json();
    }).then(function (data) {
        console.log(data);
    })
```
//包含cookie:"omit"（默认）,"same-origin"以及"include"


# HTML4

---

DOM树里包含了所有HTML标签，包括display:none隐藏，还有用JS动态添加的元素等

render tree不包含隐藏的节点 (比如display:none的节点，还有head节点)，因为这些节点不会用于呈现，而且不会影响呈现的，所以就不会包含到 render tree中

重绘：render tree中的一些元素需要更新属性，而这些属性只是影响元素的外观，风格，而不会影响布局的，比如background-color

回流：render tree中的一部分(或全部)因为元素的规模尺寸，布局，隐藏等改变而需要重新构建

---

disabled='disabled' 可用于option标签和input标签,该元素不可用。

readonly='readonly'用于input标签，不能修改的。仍然可以使用 tab 键切换到该字段，还可以选中或拷贝其文本。

---

< p>中不能放块级元素,内联元素中不能放块级元素;

---

是用img来加载图片还是用背景图片：

网页会先加载页面的标签结构，再加载样式，如果img中的图片过大，会影响后面的内容的加载；如果用背景来加载图片的话，就不会影响到页面的显示效果；如果图片比较重要就用img；alt属性有利于seo（搜索引擎优化）；更好的有利于seo用< a>加css的背景；

---

# requestAnimationFrame

window.requestAnimationFrame（callback）：这个方法是用来在页面重绘之前，通知浏览器调用一个指定的函数，以满足开发者操作动画的需求。这个方法接受一个函数为参，该函数会在重绘前调用。

大部分的浏览器的显示频率是16.7ms，当用setTime时设置的时间小于这个值时就会出现帧丢失的情况，而requestAnimationFrame是不用设置时间的，设备的时间绘制间隔是好久，它就是好久。

回调函数：有一个参数，就是触发该函数的时间

requestID = window.requestAnimationFrame(callback);// Firefox 23 / IE10 / Chrome / Safari 7 (incl. iOS)

requestID = window.mozRequestAnimationFrame(callback);// Firefox <  23

requestID = window.webkitRequestAnimationFrame(callback);// Older versions Chrome/Webkit

用window.cancelAnimationFrame(requestID)来取消这个回调函数；

CancelAnimationFrame  // Webkit中此取消方法的名字变了

CancelRequestAnimationFrame

---

requestAnimationFrame(callback)

function callback(){
    requestAnimationFrame(callback)
}

---

&nbsp占位符 



# 标签

< abbr title='people's republic of china'>PRC< /abbr>

为浏览器拼写和检查和搜索引擎提供有用的信息。新增的结构标签：（由DIV派生出来）

section:页面中的一个内容区块（不用来布局，只用来划分网页）

article：定义页面独立的区域

aside：侧边栏内容

header：

hgroup：对网页或是区块（section）的标题进行整合

footer：定义section或是文档的页脚

nav：导航

figure：独立的流内容，图片等

mark:标记

progress：进度条（支持性不好）

time：定义公历的时间（24 小时制）或日期，时间和时区偏移是可选的。它的标注是给搜索引擎用的，方便搜索引擎生成更智能的的搜索结果。

(属性datetime='2013-10-18T09：00Z'，pubdate 告诉搜索引擎这是该文档或是文章的创建时间。)

T是分隔符Z表示UTC格式；

detais:点击显示具体内容

< details>< summary>总结< /summary>< p>kkk< /p>< /details>

datalist: < input id='myCar' list='car'/>< datalist id='car'>

< option value='12'>< /option>< /datalist>

用于输入时，提示预先存储的值。

pre: 定义预格式化的文本（保留文本中的空格和换行符）；通常用来包含代码。

---
video和audio

---

# 属性

< html manifest= 'XX X.X X X'>缓存网页

---


脚本的加载顺序：先下载，再执行，再下载下一个，再执行；

< script defer>:下载好将本后，不执行，页面加载完才执行；

< script async>：下载好脚本后立即执行，但是不影响加载下面的文档，仅对外部文件；

---


< link rel='icon'  type='images/png'sizes='16\*16' href='images/delete.png'/>

图像通常可以使用任何被浏览器支持的图像格式

size:还可以为32\*32的；

type:gif,png,ico(image/vnd.microsoft.icon);

rel:shortcut icon

< link rel='shortcut icon' href='http://www.baidu.com/favicon.ico' mce\_href='http://www.baidu.com/favicon.ico' type='image/x-icon'>

---
< link rel='dns-prefetch' href='//g.tbcdn.cn'>

在加载网页时对网页中的域名进行解析缓存，这样在你单击当前网页中的连接时就无需进行DNS的解析

---
< base href = 'http ://www.w3school.com.cn/i/' />

< base target='_blank' />

会在所有的URL（img link a...）前面加上base的href内容，并且跳转方式会用base的target值


---
< ol reversed(倒序) start='5' (从5开始) type='1，a，A，i，I'>;

---
< input type='file' multiple(多选文件)/>;元素的files属性则是一个FileList对象，
该对象是一个类数组对象，files[0] (表示第一个文件),files[1].........等，一个file对象就是一个Blob。有name，type，size（files[0].name）是火狐的标准+谷歌也可以。
当没有加multiple时 只有一个文件也是用files[0]来获取

Filereader对象，图片预览等

返回的值在 r.target.result中

---
全局属性：

data-*：自定义属性;

hidden='hidden'隐藏元素;

spellcheck='true/false'检查有无拼写错误；

tableindex='1'设置按tab键的时候跳转顺序；

contentEditable=true用contentEditable来让元素的内容可以编辑，还提供了一个javascript方法，window.document.designMode='on/off'让所有的内容是否可以修改。

---
打电话
< a href='tel:1234565'>

# meta

**全屏和禁止电话号码**
< meta name="apple-mobile-web-app-capable" content="yes" > 

如果content设置为yes，Web应用会以全屏模式运行，反之，则不会。你可以通过只读属性window.navigator.standalone来确定网页是否以全屏模式显示。

兼容性： iOS 2.1 +

< meta name='apple-mobile-web-app-status-bar-style' content='blank'>

除非你先使用apple-mobile-web-app-capable指定全屏模式，否则这个meta标签不会起任何作用。

如果content设置为default，则状态栏正常显示。如果设置为blank，则状态栏会有一个黑色的背景。如果设置为blank-translucent，则状态栏显示为黑色半透明。如果设置为default或blank，则页面显示在状态栏的下方，即状态栏占据上方部分，页面占据下方部分，二者没有遮挡对方或被遮挡。如果设置为blank-translucent，则页面会充满屏幕，其中页面顶部会被状态栏遮盖住（会覆盖页面20px高度，而iphone4和itouch4的Retina屏幕为40px）。默认值default。

兼容性:iOS 2.1 +
< meta name='format-detection' content='telephone=no'>

默认情况下，设备会自动识别任何可能是电话号码的字符串。设置telephone=no可以禁用这项功能。

兼容性:iOS 1.0 +

---

< meta http-equiv='Pragma'content='no-cache'>

禁止浏览器从本地计算机的缓存中访问该页面

---
< meta charset="UTF-8">
大小写都可以

---
< meta http-equiv="refresh" content="3;url="http://ww.baidu.com">

---
< meta name="viewport" content="width=device-width, initial-scale=1 user-scalable=no" >

---

< meta http-equiv='X-UA-Compatible' content='IE=edge,chrome=1' />  
IE=edge告诉IE使用最新的引擎渲染网页，chrome=1则可以激活Chrome Frame ；

所以使用X-UA-Compatible标签强制IE8采用低版本方式渲染。 有些因素会自动触发兼容性文档视图，这个时候设置X-UA-Compatible就可以防止这个自动触发的行为。

---

# embed

AllowScriptAccess:naver/aways    参数可以防止从一个域中承载的 SWF文件访问来自另一个域的 HTML页面中的脚本。

allowNetworking:

all: SWF 文件中允许使用所有网络API;

internal: SWF 文件可能不调用浏览器导航或浏览器交互API，但是它会调用任何其它网络API.

none: SWF 文件可能不调用浏览器导航或浏览器交互API，并且它无法使用任何SWF 到 SWF 通信 API

---

# localStorage

本地存储是一个window的属性：window.localStorage

同一个目录下的页面的localStorage会存在一起

任何格式存储的时候都会被自动转为字符串

Storage事件（未完）；

Key()方法：

for(var i=0;i< localStorage.length;i++){

alert(localStorage.getItem(localStorage.key(i)));

}

sessionStorage.getItem(key):获取指定key本地存储的值

sessionStorage.setItem(key,value)：将value存储到key字段

sessionStorage.removeItem(key):删除指定key本地存储的值

sessionStorage.length是sessionStorage的项目数

sessionStorage.clear();清除所有

localStorage与上面相同。

localStorage.a = 3;
localStorage['a'] = 'sfsf';
var a1 = localStorage['a'];

var a2 = localStorage.a;

---


# Html5 消息通知

Notification（首字母大写） 或 刷新title

谷歌测试时不要用 [file://的方式访问，要用服务器的方式]

Notification.requestPermission(function(permission){}),方法要用onclick等用户操作方法来调用。

在手机上只有火狐的实现了

# history API
**主要是实现无刷新改变地址栏**

注意地址栏是queryString 请求要用path 地址栏的地址只是显示用不与请求接口一致

1. history.pushState(state,title(页面标题),url);
    - state：一个与指定网址相关的状态对象，popstate事件触发时，该对象会传入回调函数。如果不需要这个对象，此处可以填null。
    - title：新页面的标题，但是所有浏览器目前都忽略这个值，因此这里可以填null。
    - url：新的网址，必须与当前页面处在同一个域。浏览器的地址栏将显示这个网址。

2. history.replaceState();





