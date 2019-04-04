# 最新版微信分享API(移动web端)
> create-at 2019-02-16

引入微信JS-SDK http://res.wx.qq.com/open/js/jweixin-1.4.0.js (当前最新版本)

js 相关代码 (移动端实测有效)
```js
function weChatShare(title,desc) {
    var link = window.location.href; // 这里如果采用的并非当前页可能会出错，具体原因有待查找
    var serverUrl = encodeURIComponent(link);
    var imgUrl = '分享显示的小图'; //80*80 实测可以使用其它比列，最好使用小尺寸正方形,域名也要在安全域名之下

    // 数据请求，根据项目需求更改
    function ajaxFn() {
        var xhr = new XMLHttpRequest()

        xhr.open('get', '这是请求配置项的接口?url=' + serverUrl, true)
        xhr.onreadystatechange = function () {
            if (xhr.readyState == 4 && xhr.status == 200 || xhr.status == 304) {
                wxConfig(JSON.parse(xhr.responseText))
            }
        }
        xhr.send()
    }

    function wxConfig(res) {
        wx.config({
            // 是否开启调试（会返回一些错误原因）
            debug: true,
            // 公众号的唯一标识
            appId: res.appId,
            // 签名的时间戳
            timestamp: res.timestamp,
            // 签名的随机串
            nonceStr: res.nonceStr,
            // 签名
            signature: res.signature,
            // 需要调用的JS接口
            jsApiList: [
                'updateAppMessageShareData',
                'updateTimelineShareData',
                'onMenuShareAppMessage',
                'onMenuShareTimeline'
            ]
        });

        // config 验证后会执行ready方法
        wx.ready(function () {
            var shareConfig = {
                title: title,
                desc: desc,
                link: link,
                imgUrl: imgUrl
            };

            // 目前新版方法存在问题，所以如果有老方法，优先选择老方法
            if(wx.onMenuShareAppMessage){
                wx.onMenuShareAppMessage(shareConfig);
                wx.onMenuShareTimeline(shareConfig);
            } else {
                // 自定义“分享给朋友”及“分享到QQ”按钮的分享内容
                wx.updateAppMessageShareData(shareConfig);
                // 朋友圈
                wx.updateTimelineShareData(shareConfig);
            }
        });

        wx.error(function (res) {
            // config信息验证失败
            console.log(res);
        });
    }

    ajaxFn()
}

weChatShare('tit', 'des')
```

本篇文章只是做了方法整合，详见 https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1445241432

> 欢迎交流 [Github](https://github.com/NameHewei/blog-note)