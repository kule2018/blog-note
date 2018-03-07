[toc]

>*：ie6，ie7可识别；_和-ie6可识别；

>-webkit-appearance: none; 去掉type=number的默认样式

>initial(设置为默认效果); inherit：继承父元素的该属性；

>@media(max-width:300px){.className{};//屏幕小于300px}//min 小到大;max 大到小

>border-width: 5px 10px 20px 0;(上右下左)

> < hr style='height:1px;background:black;border:0'> 实现一条横线

> 当为行内元素进行定位时，position:**absolute**，position:fixed。都会使原先的行内元素变为块级元素。

# 选择器
> :nth-child(n|odd|even),选择属于父元素的第几个子元素，后两个为奇数和偶数；

> ~:
.a(元素1)~.b(元素2),同一个父元素下的兄弟元素,不必是挨着的但是必须是元素1之后的。
\[ attribute~=value \]:属性包含某个值的元素

> .a+.b 如果.a元素后紧跟的是.b即可选中。  
.a>.b选中.a的子一级的所有.b元素不包含孙一级。

> a:link {color: #FF0000} *未访问时的状态*  
a:visited {color: #00FF00} *已访问过的状态*  
a:hover {color: #FF00FF} *鼠标移动到链接上时的状态*   
a:active {color: #0000FF} *鼠标按下去时的状态*

> :checked  可以作用于radio checkbox option


# font
1. font：normal bold 12px/50px(行高可以写在这里) arial,sans-serif；合并写必须要有size和family
2. @font-face{ font-family: name; src: url()}
3. line-height:10% 基于当前字体尺寸的百分比行间距

# background
filter:blur(90px) //高斯模糊,ie不支持,其它都可，注意前缀。  

---
background:hsl(色调hue，饱和度saturation，亮度luminance)  
- 色调：0-360  红 黄 绿 青 蓝 洋   //循环 
- 饱和度：0-100%    //灰度到全包和
- 亮度：0-100%      //暗到亮
- 还有hsla()     //多了一个透明度

# 布局
1. margin,padding用百分比时:都是相对于父元素的宽;  
2. left,top:百分比相对宽,高
3. ul,ol都有一个padding和margin;li前面的样式不会占用宽度，它是占用ul的padding,但是只针对outside而言,对于inside要占用宽度


## flex布局
> 子元素的float，clear，vertical-aline属性将失效。

> 容器设置display:flex;(任何元素都可以设置，行内用display:inline-flex设置之后该容器将不会再占用一行);

### 父容器的6个属性：

1. flex-direction(弯曲方向):row | row-reverse(反向) | column | column-reverse
2. flex-wrap:nowrap(内部元素不换行且会改变元素宽度)|wrap(内部元素换行)|wrap-reverse(换行且第一行在下面)
3. flex-flow:flex-direction||flex-wrap(默认row nowrap)
4. justify-content:调整内部元素在主轴上的对齐方式
  flex-start(左对齐默认)|  
  flex-end(右对齐)  
  center(居中)  
  space-between(两端对齐，边距为0)  
  space-around(每个元素件的间隔相同，是与边距的两倍)  
5. aline-items:设置项目在纵轴(交叉轴)上的位置
  stretch(默认，项目被拉伸，适应容器)；  
  center(项目被放在纵轴中心)  
  flex-start  
  flex-end  
  baseline(位于容器的基线上，第一行文字的基线对齐)  
6. align-content(各项没有占用所有的容器空间，垂直方向上)  
stretch(占满，从上往下，顶部没有边距，往下项目间距相同)  
flex-start(上对齐默认)|  
flex-end(下对齐)  
center(居中)  
space-between(两端对齐，边距为0)  
space-around(每个元素件的间隔相同，是与边距的两倍)  

### 子容器的6个属性
1. order:<number>；默认0，越小越靠前；
2. flex-grow:<number>;默认0，项目的放大比例，当都设置为1时就等分，当有一个是2时该项目将会是其它的两倍。
3. flex-shrink:<number>;默认1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。
4. flex-basis:auto|px|%;设置宽度。
5. flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。
6. align-self:属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。除了auto，其他都与align-items属性完全一致。

---

box-shadow:水平阴影位置可为负必须，垂直阴影位置可为负必须，模糊距离值越大边沿越模糊，阴影扩展半径(就是元素外面的阴影的宽度值)值越大阴影面积越大为负值时阴影缩小，阴影颜色，将inset改为outset;  

阴影的大小和被设置的元素大小一样；

box-shadow:可以用逗号隔开来设置不同的边的阴影，但是要注意设置水平和垂直位置。（不能分开写多个box-shadow来设置）

box-shadow:  
-10px 0 10px red, *左边阴影*  
10px 0 10px yellow, *右边阴影*    
0 -10px 10px blue, *顶部阴影*  
0 0 10px 10px green; *底边阴影*  

如果只要一边阴影，就把扩展阴影设为负值。

## 居中

vertical-aline:是依赖当前元素是inline-block才会有效果；该属性定义行内元素的基线相对于该元素所在行的基线的垂直对齐。  
图片垂直居中：设置了高和行高，再加vertical-aline：middle；  
当在设置verticla-aline:middle相当于强行的把父元素的行高(就等于设置vertical-aline的元素的高度,这个高度可以不定)给设置了（基线的底部就是行的底部）；后面再有元素设置verticla-aline:middle，就会把自身的垂直中点与中线对齐。

---
将文字放在底部:  
在元素中多加一个标签，父元素为relative，子元素absolute，把子元素设置bottom：0；

---
margin:0 auto;居中  
该元素不必有确定的px值也可以是%比,，并且不能是绝对定位。且该元素必须为块级元素。

---
被居中元素固定宽高垂直水平居中：  
绝对定位的元素;  
设置left:50%;right:50%;margin-left:-width/2;margin-top:-height/2;  
或是用transform:translateX(%)这样就会相对于元素本身来缩进，就可以不用设置元素的固定的宽高。

---
垂直居中：
1. 装有显示文字的父元素设置display:table; width:100%;height: 100px;
装有显示文字的元素：display:table-cell; vertical-align:middle;
该方法适用于多行文本。
2. 将元素高度和line-height设置为相同值；如果元素没有设置高度，也可以直接设置line-height来实现。
3. 用padding：10px 0；来实现，高度就不定了。
4. 用  
< div style="height:20px;">  
    < div>内容< /div>  
< /div>  
在外部div上设置高度和用:before(在使用的元素的内部内容之前添加内容);会在内部div之前加上一个元素（content:.）;设置行高line-height，然后在父元素上设置font-size：0（让点不可见和消除元素之间的换行），再将内容的div元素设置为inline-block和加上vertical-aline:middle;或者是两个都设置vertical-aline:middle,就可以不用设置line-height；但要设置before的高度；

---
## 行内块级
label:为行内元素

---
inline-block(可设置宽高并可在同一行):元素有input select  
当使用行内元素时注意html中是否有换行或是空格，会被显示在页面上。

---
img input 可以定义宽高；

---
inline:水平方向padding margin有效

---
## 宽高
宽高设置为百分比，会是根据父元素是否已确定了高度，如果是即可以用；  
当涉及到body为父元素时，要把body和html的宽高都设置为100%，单设一个不起作用。  
但是当设置了position：absolute/fixed的是会起作用的；

---
## Img
谷歌是不管有没有src属性，设置了宽高就会有一个边框显示，只能用一个小的透明图片占位去除边框;    
火狐是只要src没有值或设置了alt值为空就不会占位，没有任何效果；

---
在页面上加载过一次该图片后，无论你是在当前页面再次使用该图片还是在该站点的其它页面使用，都会调用缓存。

---
## 换行
word-break:break-all;只对英文起作用，以字母作为换行依据  
word-wrap:break-word; 只对英文起作用，以单词作为换行依据  
white-space:pre-wrap; 只对中文起作用，强制换行  
white-space:nowrap; 强制不换行，都起作用(对inner-block的标签也起作用) (文本不换行直到遇到< br/>;标签) +overflow:hidden和text-overflow:ellipsis来实现:aaaaa...

---
word-spacing:10px    定义单词间的间距  
letter-spacing:10px  定义每个字间的间距（还可与text-indent联用）

## 滑动条

overflow:hidden;auto（只会出现宽或高的滑动条）;scroll(会出现宽和高的滑动条)前提是要有宽高；  

text-overflow:ellipsis;（不换行超出部分隐藏且以省略号形式出现）；clip(修剪文本)；

---
ie设置滑动条的样式

//SCROLLBAR-FACE-COLOR: #f892cc;           *滚动条凸出部分的颜色*

//SCROLLBAR-HIGHLIGHT-COLOR: white;      *滚动条空白部分的颜色*

//SCROLLBAR-SHADOW-COLOR: #fd76c2;         *立体滚动条阴影的颜色*

//SCROLLBAR-3DLIGHT-COLOR: #fd76c2;      *滚动条亮边的颜色*

//SCROLLBAR-ARROW-COLOR: #fd76c2;        *上下按钮上三角箭头的颜色*

//SCROLLBAR-TRACK-COLOR: #fd76c2;        *滚动条的背景颜色*

//SCROLLBAR-DARKSHADOW-COLOR: #f629b9;   *滚动条强阴影的颜色*

//SCROLLBAR-BASE-COLOR: #e9cfe0;           *滚动条的基本颜色*

---
webkit内核

*滚动条的宽度*  
::-webkit-scrollbar {  
    width: 14px;  
    height: 14px;  
}

*垂直方向的下方按钮*  
::-webkit-scrollbar-button:vertical:increment {  
    background:#D6F0FF url(/FronWeb/Images/x1204.png) no-repeat 0px 0px;  
    height:15px;  
}

*横向的右边按钮*  
::-webkit-scrollbar-button:horizontal:increment {  
    background:#D6F0FF url(/FronWeb/Images/y1204.png) no-repeat 2px 0px;  
    width:14px;  
}

*垂直方向的上按钮*    
::-webkit-scrollbar-button:vertical:decrement {  
    background:#D6F0FF url(/FronWeb/Images/s1204.png) no-repeat 1px -2px;  
    height:14px;  
}

*横向的左按钮*  
::-webkit-scrollbar-button:horizontal:decrement {  
    background:#D6F0FF url(/FronWeb/Images/z1204.png) no-repeat 1px 0px;  
    width:14px;  
}

*滚动槽的颜色*  
::-webkit-scrollbar-track-piece {  
    background-color:#d6f0ff;  
}

*滑轮的颜色*  
::-webkit-scrollbar-thumb:vertical {  
    height: 50px;  
    background-color: #9cdbff;  
    border:1px solid #7bcfff;  
    border-radius:10px;  
}  
::-webkit-scrollbar-thumb:horizontal{  
    height: 50px;    
    background-color: #9cdbff;  
    border:1px solid #7bcfff;  
    border-radius:10px;  
}

---

## Background
Background：color image repeat fixed position/size  
注意当有合并（没写的就是默认）有分开写的时候，会有后面覆盖前面的问题，  
Background-size:  
Cover：图片不会按比例缩放来覆盖当前元素背景；  
Contain：图片会按比例缩放直到宽或高达到当前元素的宽或高；  
Background-origin:border/ /content-box;背景图片放在哪里；  
Background-clip:border/padding/content-box;背景从border/padding/content开始，背景图片最多从padding开始。  
Background-attachment:scroll默认|fixed滚动轴背景图片不会移动
多重背景，写在前的在上面；

---
## 动画
> 坐标系: x(向右为正向),y(向下为正向),z(垂直界面向外为正向);视角都是从正方向往负方向看,顺时针为正度数;

animation:时间要带单位，合并写的时候顺序可以不一致。  
延迟时间要在后面；  
(@keyframes 持续时间 延迟时间 速度曲线 播放次数 是否反响播放)  
@keyframes mymove  
{  
	from {top:0px;}  
	to {top:200px;}  //该元素会从top0的位置移动到top200px位置  
} 

s或m; 

ease逐渐变慢,linear匀速,ease-in慢快,ease-out快慢,ease-in-out慢快慢,  
cubic-bezier(x,x,x,x)快慢看斜率；  

次数或infinite;  

normal或alternate；  

jQuery Easing 插件是实现缓动函数最简单的方法

$(selector).animate(styles,speed,easing(缓动),callback)

---

transition: transition-property(设置过渡效果的 CSS 属性的名称默认all)    transition-duration(s/ms)  transition-timing-function(速度曲线)    transition-delay(定义过渡效果何时开始)  

只有safari要加-webkit-其他的不加或不支持。

---
transform:
>当旋转时坐标轴会一起转，之一rotate与translate语句的前后顺序

正度数：顺时针；负度数：逆时针；默认原点为对象旋转中心；

rotate(1deg)       二维的沿xy;

rotate3d(1deg)     按（0，0，0）与（x，y，z）组成的单位向量轴转；

rotateX/Y/Z（1deg）三维的沿X/Y/Z轴转;

---
transform-style:preserve-3d;子元素将保留其3d位置

---
transform-origin：x y z;改变元素的原点位置，默认是在中心

---
translate()移动

当使用的是百分比的时候会是按照当前元素的内容区和padding和边框的宽高来计算；

translate(x,y)沿xy方向的偏移量；

translate3d(x,y,z)

---
webkit-perspective-origin:x y  //只有webkit内核支持

定义3D元素所基于的X轴和Y轴的改变改变3D元素的底部位置,改变的就是视点的位置;

---
perspective:(景深和视距)
指定观察者距离「z=0」平面的距离，为元素及其内容应用透视变换。  
不允许负值; 但针对它的子元素，不是本身,当子元素在它的内部区域的不同地方时，从同一个视角，显示的效果也会不同；

---
backface-visibility:visible|hidden  
控制当前元素旋转到背面对着我们的视角时是否显示

# sass
先安装ruby  
sass：采用的是空格缩进(文件为.sass后缀)  
h1  
  color:red  
scss: 采用花括号方式(文件为.scss后缀)  
h1{  
  color:red  
}  
安装了sass后，进入文件夹用sass-convert 被替换文件名 要得到文件名  
gem是ruby写的应用程序，用来管理安装各种包，等同于node的npm  
Ruby 安装sass源更换  
gem sources –l         查看当前的源  
gem sources --remove   [https://rubygems.org/](https://rubygems.org/)这里的是双横线 或直接 -r  
gem sources –a   [https://ruby.taobao.org/](https://ruby.taobao.org/)  
当系统不支持https的时候就换成 [http://gems.ruby-china.org/]    (http://gems.ruby-china.org/)  
gem install sass

## 语法
用@import 引入其它的scss文件 (可以是用逗号隔开的对各文件连续引用)  
css原生中也有@import语法  但是不利于性能而且要放在代码最前面，所以一般不用，但在sass中可以用。  
使用css原生规则来引入文件（出现以下情况时）：  
1. 当@import引入的文件以点.css结尾；  
2. 当@import引入的文件是http://开头的时候；
3. 当@import引入的文件后面跟的是url（"地址"）的时候；
4. 当@import引入的文件后带有media queries（@import tv）

---
**变量 $**  
$fontSize:12px  
body{ font-size:$fontSize; }

---
@charset “UTF-8”和css一样   可以不写

---
**嵌套**
```css
/*选择器嵌套*/
#top_nav{
  line-height: 40px;
  li{
    float:left;
  }
  a{
    display: block;
    &:hover{      //父选择符
      color:#ddd;
    }
  }
}
/*属性嵌套*/
.fakeshadow {
  border: {
    style: solid; 
    left: {
      width: 4px;
    }
    right: {
      width: 2px;
    }
  }
}
```

计算可以带单位例如，px

---

@function 来声明函数   一般很少用

---
当只用来继承的样式不想输出到css  可以用%名称{}和@extend %名称来使用。  
```css
%ir{
  color: transparent;
}
#header{
    @extend %ir;
    width:300px;
}
```
---
@at-root{
      .cla{}
}   用于将嵌套再某个类下面的类.cla渲染到css的根下而不是跟在某个类之后。

---
**混合 mixin**
```css
@mixin horizontal-line($border:1px dashed #ccc, $padding:10px){
    border-bottom:$border;
    padding-top:$padding;
    padding-bottom:$padding;  
}
.imgtext-h li{
    @include horizontal-line(1px solid #ccc);
}
.imgtext-h--product li{
    @include horizontal-line($padding:15px);
}
//多组值传参
@mixin box-shadow($shadow...) {
  box-shadow:$shadow;
}
.box{
  @include box-shadow(0 2px 2px rgba(0,0,0,.3),0 3px 3px rgba(0,0,0,.3),0 4px 4px rgba(0,0,0,.3));
}

```

---
**继承**
```css
//@extend 不能继承选择器序列   比如@extend .content .inner
h1{
  border: 4px solid #ff9aa9;
}
.speaker{
  @extend h1;
  border-width: 2px;
}
```

---
单行注释会被省略。

块注释会被输出。

---
config.rb文件

output_style   //expanded(为默认)||nested对应嵌套来缩进||compact  等等。

# compass

gem install compass

创建一个初始化的文件目录

compass create lean-compass-init(名称)

进入文件，然后就可以用compass watch   //监听

compass compile     //在项目根目录下运行  会将sass文件下的scss文件编译为css文件放到config.rb文件配置的css-dir对应的文件下

---
核心模块

@import compass/reset

@import compass/layout

@import compass  //默认包含五大模块  不包含以上两个模块

css3 helpers typography utilities browser

---
插件引用在config.rb文件中配置。

例：require &#39;compass-normalize&#39;

在要引用的scss文件中用@import &#39;normalize&#39;

reset模块是compass内置的

单独引用某个模块要引用import &#39;normalize-version&#39;

---
强制引入两次，@import &#39;filename！&#39;

压缩输出注释不被删除



