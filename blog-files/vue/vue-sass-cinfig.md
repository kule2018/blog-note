# vue配置sass

### 版本
- webpack 3.6.0
- vue 2.5.2
- sass-loader 6.0.6
- node-sass 4.7.2

### 安装
- npm | cnpm install node-sass --save-dev
- npm | cnpm install sass-loader --save-dev

### webpack.base.config.js
不用修改任何配置

### vue文件中使用


```html
<script>
 //直接用js引入样式文件  
 import 'url...';
 </script>
```
```html
<style type="text/scss" lang="scss">
	如果要引入文件
   @import 'url...';**注意分号必须要加**
</style>
```