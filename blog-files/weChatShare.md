# 最新版微信分享API(移动web端)
> create-at 2019-02-16

引入微信JS-SDK http://res.wx.qq.com/open/js/jweixin-1.4.0.js (当前最新版本)

js 相关代码 (移动端实测有效)
```js
function weChatShare(title,desc) {
    var link = window.location.href;
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
                'updateTimelineShareData'
            ]
        });

        // config 验证后会执行ready方法
        wx.ready(function () { });

        wx.error(function (res) {
            // config信息验证失败
            console.log(res);
        });

        // 分享到朋友和QQ好友
        wx.updateAppMessageShareData({
            // 分享标题
            title: title,
            // 分享描述
            desc: desc,
            // 分享链接，该链接域名或路径必须与当前页面对应的公众号JS安全域名一致
            link: link,
            // 分享图标
            imgUrl: imgUrl,
            success: function () {
                // 设置成功
            }
        })

        // 分享到朋友圈，QQ空间
        wx.updateTimelineShareData({
            title: title,
            link: link,
            imgUrl: imgUrl,
            success: function () {
                // 设置成功
            }
        });
    }

    ajaxFn()
}

weChatShare('tit', 'des')
```

本篇文章只是做了方法整合，详见 https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1445241432

> 交流 [Github blog issues](https://github.com/NameHewei/blog/issues)