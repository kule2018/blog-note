# 微信分享(移动web端)
> create-at 2019-02-16

引入微信JS-SDK http://res.wx.qq.com/open/js/jweixin-1.4.0.js (当前最新版本)

js 相关代码 (移动端实测, 需做老版本兼容)
```js
function weChatShare() {
    // 数据请求，根据项目需求更改
    function ajaxFn() {
        var xhr = new XMLHttpRequest()

        xhr.open('get', '这是请求配置项的接口?url=' + location.href, true)
        xhr.onreadystatechange = function () {
            if (xhr.readyState == 4 && xhr.status == 200 || xhr.status == 304) {
                wxConfig(JSON.parse(xhr.responseText))
            }
        }
        xhr.send()
    }

    function wxConfig(res) {
        var title = '标题';
        var desc = '描述';
        var link = location.href;
        var imgUrl = "分享显示的小图"; //80*80 实测可以使用其它比列，最好上使用小尺寸正方形

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

        //  老版本 分享给朋友 即将废弃
        wx.onMenuShareAppMessage({
            title: title,
            desc: desc,
            imgUrl: imgUrl,
            link: link,
            type: 'link', // 分享类型,music、video 或 link，不填默认为link
            dataUrl: '', // 如果 type 是 music 或 video，则要提供数据链接，默认为空
            trigger: function (res) {
            },
            success: function (res) {
                console.log('分享朋友')
            },
            cancel: function (res) {
            },
            fail: function (res) {
            }
        });

        // 老版本 分享到朋友圈 即将废弃
        wx.onMenuShareTimeline({
            title: title, // 分享标题
            link: link, // 分享链接，该链接域名或路径必须与当前页面对应的公众号JS安全域名一致
            imgUrl: '', // 分享图标
            success: function () {
                // 用户点击了分享后执行的回调函数
            }
        })
    }
    ajaxFn()
}
```

本篇文章只是做了方法整合，详见 https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1445241432

> 交流 [Github blog issues](https://github.com/NameHewei/blog/issues)