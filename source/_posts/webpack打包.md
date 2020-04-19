---
title: webpack打包
date: 2020-04-19 12:21:16
tags:
  - webpack
  - 浏览器兼容
---

# webpack

webpack 是一个打包工具，可以通过 npm 下载安装：`npm install -g webpack`来安装。

### 原因

我们在构建网站时，在 `<script>` 或者`<link>`标签中会引入静态资源文件。

### 常见的静态资源

1. .js .jsx .coffee .ts(typescript)
2. css
3. images
4. 字体文件
5. 模板文件

这些静态文件是我们经常需要引用的，但是浏览器解析渲染时，如果静态资源太多，会加载变慢。还有许多依赖关系也会影响。
解决问题就是：

- 合并，压缩
- 图片的 base64 编码
- 使用 requireJS,也可用 webpack 解决依赖关系
- Gulp 是基于 task 的解决方案
- webpack 是基于项目的解决方案

## 初次使用 webpack

html 的隔行变色
首先是构建一个项目目录：

- dist （webpack 打包后的文件目录）
- src （html,css,js 文件）
- node_modules（npm 引入的库文件）
- package.json （npm init）

先建立 index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=/, initial-scale=1.0" />
    <title>Document</title>
    <!--下面的script标签是在webpack打包之后引入的文件-->
    <script src="../dist/main.js"></script>
  </head>
  <body>
    <ul>
      <li>我是一个标签</li>
      <li>我是一个标签</li>
      <li>我是一个标签</li>
      <li>我是一个标签</li>
      <li>我是一个标签</li>
      <li>我是一个标签</li>
      <li>我是一个标签</li>
      <li>我是一个标签</li>
      <li>我是一个标签</li>
      <li>我是一个标签</li>
    </ul>
  </body>
</html>
```

src>main.js

```javascript
import $ from 'jquery'
$(function () {
  $('li:odd').css('backgroundColor', 'lightblue')
  $('li:even').css('backgroundColor', 'lightyellow')
})
```

先在 dist 目录下创建 main.js 文件
接着在项目目录下面执行`webpack ./src/main.js ./dist/main.js` 就会生成 main.js 文件，运行～，成功！

具体可见[webpack 官网](http://webpackjs.com)

后续再补充！
