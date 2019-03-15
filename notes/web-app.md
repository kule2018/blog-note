[toc]
# 移动端遇到的问题及处理方式

- ios8 以下不支持sessionStorage
---

- input button 标签有：outline

---

- 下载app方式 a标签地址
    1. ios: 'itms-apps://itunes.apple.com/cn/app/%E5%87%AF%E5%8A%B1%E7%A8%8B/id840880551?mt=8'
    2. android： 直接下载地址
---

- 打开app
    1. 查询app的URL Scheme(如微信的为weixin) <a href="weixin://" >打开微信</a> 
---

- 禁止识别手机号
    1. < meta name="format-detection" content="telephone=no">
---

- 去掉ios长按时的阴影
    1. *{-webkit-tap-highlight-color: transparent;} 

---

- 兼容iPhoneX 
    1. env()替代constant() constant 从iOS11.2 Beta开始会被弃用
    2. 设置可视窗口大小 viewport-fit=cover|contain|auto
```
<meta name="viewport" content="viewport-fit=cover"> 只能设置cover
body {
  padding-bottom: constant(safe-area-inset-bottom);
  padding-bottom: env(safe-area-inset-bottom);
}
// env() 跟 constant() 需要同时存在，而且顺序不能换
```

---
- ios的 input 有默认的 padding和 margin  以及一些Android会默认有白色背景 

---

- 页面有滑动时 在 ios 中，底部的白色或黑色的背景被拉上来，没有回弹，是原生框架问题

---

- 设置border0.5px  Android 会处理为1px ios 会处理为0.5px

---

- 防止滑动穿透(例：阻止 touchmove 的default事件)
```js
ele.addEventListener('touchmove', (e) => { e.preventDefault(); }, false)
```

---

- 调用原生app提供的方法时应该用try catch 来防止报错后整个H5应用崩溃 **注意向前兼容老版本没有app提供的方法**

---

- 设置或者获取滚动条位置
```js
document.documentElement.scrollTop // 其它
document.body.scrollTop = height // ios
```
---

- 设置了元素overflow：auto 在 ios 中滚动不流畅，设置-webkit-overflow-scrolling: touch

---

- 1px  用scale缩放0.5  达到0.5像素效果

---

- 多行文本溢出 box-orient：vertical；line-clamp：2

---

- ios 弹性滚动 over-scroll：touch

---

- click 300ms 延迟
- tap 300ms延迟导致 底层的元素的cklic事件被触发  所以底层最好也用tap事件

---

- window.location.reload() 在部分Android机型无法指行

```js
// 兼容做法
window.location.reload()
setTimeout(() => {
    // 这里用 replace 是为了生成新 url，注意不同项目做法会不同
    window.location.href = window.location.href.replace(/#.*/g,'');
}, 300);
```
---

- ios 在弹出层中双击任意元素，底部页面自动上滑

当弹出层出现时，将body(也可能是其它元素)设置如下css，隐藏时置空
```css
overflow:hidden;width:100%;position: fixed; height: 100%;//移动端如果只设置overflow:hidden会无效
```

---

- 与app交互传递参数时，为保证 ios与 Android都可行，传字符串

---

# 移动端相关说明
 
- 移动端 兼容所有h5
- 基于webview
- 基于webkit
- 定高  宽度百分比   flex  媒体查询

```css
 @media 媒体类型(screen,print) and 媒体特性（max-width）{
     css
 }
 ```

 <link rel="stylesheet" href="" media="screen and (max-width:320px)">

 rem ios6+ android 2.1+

 document.documentElement.clientWidth || document.body.clientWidth; 


 padding会增加宽度
 box-sizing：border-box

 px :css pixels 逻辑像素，浏览器使用的抽象单位
 dp,pt: device independent pixels 设备独立像素 物理像素
 dpr：设备像素缩放比(若为2：等同于页面扩大了一倍，要用initial-scale：0.5变回来) js 用 window.devicePixelRatio 来获取
 设备像素比(dpr) ＝ 物理像素 / 设备独立像素
 CSS中，可以通过-webkit-device-pixel-ratio，-webkit-min-device-pixel-ratio和 -webkit-max-device-pixel-ratio进行媒体查询，对不同dpr的设备做适配

平面上 1px = dpr * dpr * dp 
维度上 1px = dpr * dp

flex 4.4以上


