# 获取微信用户信息
> create-at 2019-04-02

[官方文档](https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1421140842)

总共4步：

1. 第一步：用户同意授权，获取code
2. 第二步：通过code换取网页授权access_token
3. 第三步：刷新access_token（如果需要）
4. 第四步：拉取用户信息(需scope为 snsapi_userinfo)

**这里只对前端需要做的工作进行说明**

前端需要做的只有**第一步**，因为出于安全考虑，敏感信息不能传给客户端；即便强行用前端来处理整个过程，微信那边也有检测，不会将敏感信息返回。

前端部分：

- (1) 获取appid：这个由自己公司后端人员提供接口获取
- (2) 调用如下接口：参数一定要按顺序；redirect_uri可以带上参数一起转码，转码用encodeURIComponent;实测是用location.href访问的该接口,没有异常
```
https://open.weixin.qq.com/connect/oauth2/authorize?appid=APPID&redirect_uri=REDIRECT_URI&response_type=code&scope=SCOPE&state=STATE#wechat_redirect
具体参数的意义请参考上方官方文档
```
- (3) 获取code：跳转到重定向的页面后code会跟在url链接上，如果重定向的地址也带有参数，code会拼接在其后边
- (4) 将code传给后端，返回用户信息

本篇文章只是做了整个流程说明与坑点，详见上方官方文档

> 交流 [Github blog issues](https://github.com/NameHewei/blog/issues)
