- koa-static

当设置的目录下有index.html, 访问根路径时，会默认渲染index.html

---

- koa-bodyparser 解析上传的json(基本)

---

-  ctx的 headers 和 header 属性皆可获取： ctx.header.origin

# koa-router 
- /page/:path  利用 ctx.params.path 获取

# request

- 当没有默认导出时要用 * 防止报错  import * as api from './controllers/api'

- ctx.request.query：获取query string参数 以{ key:value } 形式返回