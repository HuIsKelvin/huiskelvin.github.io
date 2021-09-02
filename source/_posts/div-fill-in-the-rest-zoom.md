---
title: CSS—div的高度填满剩余空间
date: 2019-04-04 22:15:11
tags:
  - CSS
description: 用CSS实现div的高度填满剩余空间
---

# 描述

使用CSS实现。
页面有上下两个部分，上部分定高，下部分填满窗口剩余的高度，不能出现纵向滚动条。

示例：
[![ARmKG6.jpg](https://s2.ax1x.com/2019/04/04/ARmKG6.jpg)](https://imgchr.com/i/ARmKG6)
（只是为了看的直观，没考虑配色美观）

HTML结构如下：
```html
<div id="main">
  <!-- 上面的部分 -->
  <div id="nav">nav</div>
  <!-- 剩余部分 -->
  <div id="content">content</div>
</div>
```

## 使用float

将 `#nav` 设置为 `float: left;`，再让 `#content` 的宽度为 100%。

```css
html,
body {
  /* 一定要设置这个 */
  height: 100%;
  margin: 0;
}

#main {
  height: 100%;
}

#nav {
  background-color: #4B5ED7;
  width: 100%;
  height: 40px;
  float: left;
}

#content {
  background-color: #e0e0e0;
  /* width 不设置100%，也是横铺满的 */
  /* width: 100%; */ 
  height: 100%;
}
```

## 使用absolute，再限定top和bottom

使用 `position: absolute;`，再配合`top`和`bottom`，来强制定义盒模型的区域。

```css
* {
  margin: 0;
}

#nav {
  background-color: #4B5ED7;
  width: 100%;
  height: 40px;
}

#content {
  background-color: #e0e0e0;
  width: 100%;
  position: absolute;
  /* 距顶部距离就是 #nav 的 height */
  top: 40px;
  bottom: 0;
  left: 0;
}
```

## 使用flex

使用 `position: flex;`，主轴设置为纵向。
`flex-grow` 用来指定父容器多余空间的分配比率。

```css
html,
body {
  /* 一定要设置这个height */
  height: 100%;
  margin: 0;
}

#main {
  /* 一定要设置这个height */
  height: 100%;
  display: flex;
  flex-direction: column;
}

#nav {
  background-color: #4B5ED7;
  width: 100%;
  height: 40px;
}

#content {
  background-color: #e0e0e0;
  width: 100%;
  flex-grow: 1;
}
```

## 使用calc()和 vh

`calc()` 函数是`CSS`中用于动态计算长度值。
`vh` 是相对于视口的高度，视口被均分为100单位，一个单位为`1vh`。
两个都是CSS3的属性。

```css
html,
body {
  margin: 0;
}

#main {
  height: 100%;
}

#nav {
  background-color: #4B5ED7;
  height: 40px;
}

#content {
  background-color: #e0e0e0;
  width: 100%;
  height: calc(100vh - 40px);
}
```