[toc]

# koa2图片上传成功后返回服务器地址,实时显示服务器图片

> 版本：node(8.5.0); koa(2.4.1); koa-router(7.3.0); koa-body(2.5.0); koa-static(4.0.2);

## 代码实现
```js
const fs = require('fs')
const app = new Koa()
const router = new Router()
const serve = require('koa-static')
const koaBody = require('koa-body')

app
    .use(serve(__dirname + '/files')) // files文件夹用于保存上传的文件,也是静态资源地址
    .use(router.routes())

// 前端使用formData方式组装数据
router.post('/api/upload-files', koaBody({ jsonLimit: '2mb', multipart: true }), async (ctx) => {
    const data = ctx.request.body.files.data;
    const savePath = path.join(`./files`, data.name)
    const reader = fs.createReadStream(data.path)
    const writer = fs.createWriteStream(savePath)

    const pro = new Promise( (resolve, reject) => {
        var stream = reader.pipe(writer);

        stream.on('finish', function () {
            resolve(`http://当前服务器地址${data.name}`);
        });
    })
    
    ctx.response.body =  await pro
    
})
```