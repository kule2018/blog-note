[toc]

# vue
> 更新时间： 2018-09-21
## vue cli 3
1. 选择 Manually select feature
2. 选中 CSS Pre-processors
3. 选择 scss/sass
4. 其它选项按项目需要配置

引用方式与老版本脚手架搭建的项目一致，如下

## 老版本的脚手架搭建的项目
### 版本
- webpack 3.6.0
- vue 2.5.2
- sass-loader 6.0.6
- node-sass 4.7.2

### 安装
- npm | cnpm install node-sass --save-dev
- npm | cnpm install sass-loader --save-dev

### 不用修改任何配置

### vue文件中使用

```html
<style type="text/scss" lang="scss">
   如果要引入文件
   @import 'url...';**注意分号必须要加**
</style>
```