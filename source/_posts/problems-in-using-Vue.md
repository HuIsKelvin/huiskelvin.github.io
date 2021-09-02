---
title: 使用Vue开发项目中遇到的坑
date: 2019-03-08 08:06:09
tags: Vue
description: 记录在使用Vue的过程中遇到的问题
---

最近在使用 Vue-cli 3 开发项目，于是记录下开发过程中遇到的坑。便于下次遇到相同坑时，能快速找到解决方法。

# 问题

## npm run build 后，部署网页到服务器，出现404错误

### 描述

### 原因

因为 vue-cli-3 默认打包后的项目放在域名的根目录，使用绝对路径来引用资源，则在index.html中引用资源的目录的`src`开头都为`"/"`.

vue-cli-3 官方文档在 [publicPath](https://cli.vuejs.org/zh/config/#publicpath) 的说明：
>默认情况下，Vue CLI 会假设你的应用是被部署在一个域名的根路径上，例如 `https://www.my-app.com/`。如果应用被部署在一个子路径上，你就需要用这个选项指定这个子路径。例如，如果你的应用被部署在 `https://www.my-app.com/my-app/`，则设置 publicPath 为 `/my-app/`。
这个值也可以被设置为空字符串 ('') 或是相对路径 ('./')，这样所有的资源都会被链接为相对路径，这样打出来的包可以被部署在任意路径

### 解决

在 vue.config.js 中，修改以下语句，

```js
module.exports = {
  // 使用相对路径引用 js、css 等资源
  publicPath: "./"
}
```

## 本地开发跨域问题

在本地开发请求后端服务器接口的时候，一般都需要跨域。如果用vue-cli3搭建的项目，可以在根目录的 `vue.config.js` 文件中，修改 `proxy` 或 `proxyTable` 属性。

```js
// vue.config.js
module.exports = {
    devServer: {
        proxy: {
            '/api': {
                target: 'http://yoururl.com',  // 填入你实际的后端服务器接口
                ws: true,  
                changeOrigin: true,
                pathRewrite: {
                    '^/api': ''
                }
            },
        }
    },
};
```

在请求时，就会将 `/api/posts/1` 请求代理到 `http://yoururl.com/posts/1`。

## 在360浏览器上，不能正常使用URLSearchParams

### 描述

开发的网页中，有一个检索框，输入检索词并按回车后，就会将检索词传回后端进行检索。然而在360浏览器中，按回车后没反应，报错显示`URLSearchParams() is not defined`.

输入检索词后，按回车就会调用`search_query()`方法。在`search_query()`方法中，会使用`URLSearchParams`处理query，然后用`axios`的`post()`发送，然后query传给后端，再跳转到检索结果页面。

### 原因

`URLSearchParams`在特定浏览器（如360浏览器）中不被兼容。

### 解决

在项目中安装 url-search-params-polyfill，在main.js中引入URLSearchParams 的类，之后可以按照正常操作使用 URLSearchParams。

```
npm i --save url-search-params-polyfill
……

import "url-search-params-polyfill"
```

## 待更新...