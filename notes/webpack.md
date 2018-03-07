[toc]
# 杂项
npm  ls  –g  --depth=1 2>/dev/null | grep generator-
列出npm全局安装的包   
npm包一般会依赖别的包所以是按照树状来显示的。    
depth 限制往下一层目录，后面是过滤错误信息。 

---
.gitignore  
以斜杠“/”开头表示目录

----------
**babel-core**    
如果某些代码需要调用Babel的API进行转码，就要使用babel-core模块    
**babel-cli**   
在命令行执行babel命令

# Yeoman  
npm install yo  
生成项目文件，代码结构，自动将最佳实践和工具整合进来  
yo --version 

# bower
npm install bower    
web网站组成：框架，库，公共部分，  
bower用来跟踪管理   
bower install jquery

# grunt  
npm install grunt-cli(command-line interface)  
自动化，压缩，编译，单元测试，代码1（）.校验  

# webpack  
npm install webpack -g    
非全局安装 使用命令 node_modules/.bin/webpack  
--webpack-dev-server --content-base app/(自定义根目录)，默认以当前目录  

---
在不是根路由的情况下刷新页面，可能会不能获取到打包的js文件，这时就要配置publicPath

---
使用html-webpack-plugin插件时获取参数只能用htmlWebpackPlugin  

---
**热更新** 

热更新的处理逻辑webpack已经封装好了，只要在应用的入口文件中添加以下代码  
```javascript
if (module.hot) {  
  module.hot.accept();
}
```

---
**支持的模块化语法**   
1. CommonJs，同步require   
该方案的核心思想就是允许模块通过require方案同步加载依赖的其他模块，通过exports或module.exports来暴露出需要的接口。  
nodejs就是参照commonJS规范实现的。  
2. AMD，异步require。
require([moudle],callback)
3. 该方案最大的特点就是静态化，静态化的优势在于可以在编译的时候确定模块的依赖关系以及输入输出的变量。上面提到的CommonJs和AMD都只能在运行时确定这些东西。  
import "jquery";  
export function doStuff() {}

