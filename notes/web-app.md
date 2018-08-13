[toc]
# 移动端处理方式
- ios8 以下不支持sessionStorage

- input button 标签有：outline

- 下载app方式 a标签地址
    1. ios: 'itms-apps://itunes.apple.com/cn/app/%E5%87%AF%E5%8A%B1%E7%A8%8B/id840880551?mt=8'
    2. android： 直接下载地址

- 打开app
    1. 查询app的URL Scheme(如微信的为weixin) <a href="weixin://" >打开微信</a> 

- 禁止识别手机号
    1. < meta name="format-detection" content="telephone=no">

- 去掉ios长按时的阴影
    1. *{-webkit-tap-highlight-color: transparent;} 

- 兼容iPhoneX 
    1. env()替代constant() constant 从iOS11.2 Beta开始会被弃用
    2. 设置可视窗口大小 viewport-fit=cover|contain|auto

- ios的 input 有默认的 padding和 margin  以及一些Android会默认有白色背景 

- 设置border0.5px  Android 会处理为1px ios 会处理为0.5px

- 防止滑动穿透(例：阻止 touchmove 的default事件)

- 调用原生app提供的方法时应该用try catch 来防止报错后整个H5应用崩溃 **注意向前兼容老版本没有app提供的方法**

- 设置或者获取滚动条位置
```js
document.documentElement.scrollTop // 其它
document.body.scrollTop = height // ios
```

- 设置了元素overflow：auto 在 ios 中滚动不流畅，设置-webkit-overflow-scrolling: touch