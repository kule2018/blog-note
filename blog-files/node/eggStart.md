[toc]

# egg 自学入门demo分享

> 2018-08，本文适用于对egg有兴趣想要了解的同学

> 完整项目代码：[https://github.com/NameHewei/node-egg](https://github.com/NameHewei/node-egg)

项目主要文件目录结构
```
|—— app
    |—— controller
        |—— cook.js
    |—— model
        |—— cook.js
    |—— router.js
|—— config
    |—— config.default.js
    |—— plugin.js
|—— package.json
|—— README.md
```

# 安装
官网： https://eggjs.org/zh-cn/

1. npm i egg-init -g
2. egg-init egg-example --type=simple
3. cd egg-example
4. npm i

启动项目
- npm run dev

# 项目

本文主要是以搭建一个连接mongoDB的后端，以提供api接口

## 连接数据库
1. 引入数据库插件,在plugin.js文件中添加如下代码
```js
exports.mongoose = {
    enable: true,
    package: 'egg-mongoose',
};
```

2. 在config.default.js中添加如下配置
```js
config.mongoose = {
    client: {
        url: 'mongodb://127.0.0.1:27017/database-name',
    },
}
```

## 编写model
在model文件下添加，cook.js 文件
```js
module.exports = app => {
    const mongoose = app.mongoose;
    const Schema = mongoose.Schema;

    const CookeSchema = new Schema({
        _id: { type: Schema.Types.ObjectId },
        name: { type: String  },
        img: { type: String  },
        step: { type: String  }
    }, { 
        versionKey: false
    });

    return mongoose.model('cooks', CookeSchema);
}
```

注意如果使用mongoDB中的_id时type的类型，以及如何去掉__v 版本锁字段。

## 编写controller
在controller文件夹下添加，cook.js文件
```js
const Controller = require('egg').Controller;

class HomeController extends Controller {
  async list() {
    this.ctx.response.body = {
      result: await this.ctx.model.Cook.find({}, {'_id': 0})
    };
  }

  async listOne() {
    const { id } = this.ctx.params
    this.ctx.body = {
      result: await this.ctx.model.Cook.find({ '_id': id }, {'_id': 0})
    };
  }
}

module.exports = HomeController;
```
这里用于获取数据库中的数据

## 添加路由
```js
module.exports = app => {
  const { router, controller } = app;
  router.get('/cook/', controller.cook.list);
  router.get('/cook/:id', controller.cook.listOne);
};
```

确保数据库能连接成功后，便可以启动项目。

本文只是辅助介绍快速搭建一个基本的egg项目，具体内容请参考：https://eggjs.org/

> 欢迎交流 [Github](https://github.com/NameHewei/blog-note)