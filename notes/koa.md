# 跨域

- 方法一
```
app.use(async function(ctx, next) {
    ctx.set("Access-Control-Allow-Origin", ctx.request.header.origin)
    await next()
})
```
- 方法二

```
const cors = require('koa2-cors')
app.use(cors({
    origin: function (ctx) {
        return 'http://localhost:1111';
    },
    exposeHeaders: ['WWW-Authenticate', 'Server-Authorization'],
    maxAge: 5,
    credentials: true,
    allowMethods: ['GET', 'PUT', 'POST', 'PATCH', 'DELETE', 'HEAD', 'OPTIONS'],
    allowHeaders: ['Content-Type', 'Authorization', 'Accept'],
}));
```