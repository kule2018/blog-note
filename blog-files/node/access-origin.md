[toc]

# nodeJs 跨域 

## 原生跨域
```js
var http=require('http');

var server = http.createServer(function (req,res) {
    res.setHeader('Access-Control-Allow-Origin', req.headers.origin)
    res.end("success")
});

server.listen(1200);
console.log('listen on 1200');
```


## express跨域
```js
const express = require('express');
const app = express();

// 注意all方法要先于其它方法执行
app.all('*', function(req, res, next) {
    res.setHeader('Access-Control-Allow-Origin', req.headers.origin)
    next()
})

app.get('/', function (req, res) {
    res.send('success');
});


app.listen(1200, function () {
  console.log('listen on 1200');
});
```

## koa2跨域
```js
const Koa = require('koa')
const Router = require('koa-router')
const cors = require('koa2-cors')
const app = new Koa()
const router = new Router()

app
    .use(cors({
        origin: function (ctx) {
            // 这里用 headers 和 header 属性皆可
            return ctx.header.origin;
        }
    }))

router.get('/', (ctx) => {
    ctx.response.body = 'success'
})

app.listen(1200, () => {
    console.log('listen on 1200');
});
```

## eggJs跨域
- 安装egg-cors包
```js
// 编辑 config/plugin.js
exports.cors = {
  enable: true,
  package: 'egg-cors',
};

// 编辑config/config.default.js
exports.cors = {
    enable: true,
    package: 'egg-cors',
};
```
> 详见[egg-cord](https://github.com/eggjs/egg-cors)


