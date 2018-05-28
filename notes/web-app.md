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