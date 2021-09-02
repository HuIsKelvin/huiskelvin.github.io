---
title: JavaScript-简介
date: 2019-03-24 19:50:37
tags: JavaScript
description: JavaScript概要
---

# Javascript 简史

早期的网页，表单验证必须把表单数据发送到服务器端，才能确定用户是否没有填写某个必填域，是否输入了无效的值。当年的网速很慢，为完成简单的表单验证而频繁地与服务器交换数据，只会加重用户的负担。

由此诞生了JavaScript，它主要目的是处理以前由服务器端语言（如 Perl）负责的一些输入验证操作。JavaScript的最初名字叫 LiveScript，Netscape 公司为了搭上媒体热炒Java的顺风车，临时把 LiveScript 改名为 JavaScript。

# Javascript 实现

虽然 JavaScript 和 ECMAScript 通常都被人们用来表达相同的含义，但 JavaScript 的含义却比 ECMA-262 中规定的要多得多。

一个完整的 Javascript 由以下**三部分组成**：
- 核心(ECMAScript)
- 文档对象模型(DOM)
- 浏览器对象模型(BOM)

## ECMAScript

由 ECMA-262 定义的ECMAScript与 Web浏览器没有依赖关系。ECMA-262 定义的只是这门语言的基础，而在此基础之上可以构建更完善的脚本语言。我们常见的 Web 浏览器只是 ECMAScript 实现可能的**宿主环境之一**，其他宿主环境包括 Node（一种服务端 JavaScript平台）和 Adobe Flash。

宿主环境不仅提供基本的 ECMAScript 实现，同时也会提供该语言的扩展，以便语言与环境之间对接交互。而这些扩展——如 DOM，则利用 ECMAScript的核心类型和语法提供更多更具体的功能，以便实现针对环境的操作。

ECMA-262 标准规定了这门语言的下列组成部分：
- 语法 
- 类型 
- 语句 
- 关键字 
- 保留字 
- 操作符 
- 对象

## DOM

文档对象模型（DOM，Document Object Model）DOM把整个页面映射为一个多层节点结构。HTML 或 XML 页面中的每个组成部分都是某种类型的节点，这些节点又包含着不同类型的数据。

通过 DOM 创建的这个表示文档的树形图，开发人员获得了控制页面内容和结构的主动权。借助 DOM 提供的 API，开发人员可以轻松自如地删除、添加、替换或修改任何节点。

一个简单的 HTML 页面

```html
<html>
  <head>
    <title>Sample Page</title>
  </head>
  <body>
    <p>Hello World!</p>
  </body>
</html>
```

该 HTML 页面对应的 DOM 树：
![DOM 树](https://s2.ax1x.com/2019/02/16/krjmFI.jpg)

>DOM并不只是针对 JavaScript的，很多别的语言也都实现了DOM。
不过，在 Web 浏览器中，基于 ECMAScript 实现的 DOM 的确已经成为 JavaScript 这 门语言的一个重要组成部分。

## BOM

开发人员使用BOM（BOM，Browser Object Model）可以控制浏览器显示的页面以外的部分。

而BOM真正与众不同的地方（也是经常会导致问题的地方），还是它作为 JavaScript 实现的一部分但却没有相关的标准。这个问题在 HTML5 中得到了解决，HTML5 致力于把很多 BOM 功能写入正式规范。有了 HTML5，BOM 实现的细节有望朝着兼容性越来越高的方向发展。

从根本上讲，BOM只处理浏览器窗口和框架；但人们习惯上也把所有针对浏览器的 JavaScript 扩展算作 BOM 的一部分。下面就是一些这样的扩展： 
- 弹出新浏览器窗口的功能
- 移动、缩放和关闭浏览器窗口的功能
- 提供浏览器详细信息的 navigator 对象
- 提供浏览器所加载页面的详细信息的 location 对象
- 提供用户显示器分辨率详细信息的 screen 对象
- 对 cookies 的支持
- 像 XMLHttpRequest 和 IE 的 ActiveXObject 这样的自定义对象。

<hr/>

参考资料：
- 《JavaScript 高级程序设计》