---
title: CSS-鼠标hover某元素，控制另一个元素显示
date: 2019-03-30 10:36:27
tags: CSS
description: hover一个元素，另一个元素也显示
---

# 描述

页面上有一个元素A，和另一个元素B。当鼠标悬浮在元素A上时，元素B同时显示。

例子：
[![ABoRxK.md.gif](https://s2.ax1x.com/2019/03/30/ABoRxK.md.gif)](https://imgchr.com/i/ABoRxK)

# 实现

例子页面：

```html
<!-- 页面结构 -->
<div class="container">
  <div class="box-a">
    <p>A</p>
  </div>
  <div class="box-b">
    <p>B</p>
  </div>
</div>
```

```css
.container{
  position: relative;
  background-color: #e0e0e0;
  width: 500px;
  height: 200px;
}

.container .box-a {
  background-color: #aaa;
  width: 100px;
  height: 100px;
}

.container .box-b {
  /* 默认不显示 */
  display: none;
  width: 400px;
  height: 200px;
  position: absolute;
  top: 0;
  /* 左边距离即 box-a 的width */
  left: 100px;
  background-color: antiquewhite;
}

```

## CSS实现

使用CSS的伪类和选择器来实现。

将元素B作元素A的兄弟元素或子元素，用元素A的hover状态作选择器的限制部分，控制元素B的`display: block;`。

```css
/* 在 style 中加入这一个 */
.box-a:hover ~ .box-b {
  display: block;
}
```


## Javascript事件监听来实现

通过元素A监听事件 `mouseover` 和 `mouseout`，来控制元素B的显示和隐藏。

但这种办法稍显麻烦，每次都要监听两个事件。

```js
var boxA = (document.getElementByClassName("box-a"))[0];
var boxB = (document.getElementByClassName("box-b"))[0];

// 当鼠标移入元素A时
boxA.addEventListener("mouseover", function() {
  boxB.style.display = "block";
});
// 当鼠标移出元素A时
boxA.addEventListener("mouseout", function() {
  boxB.style.display = "none";
})
```

## 最终效果

[![AB754A.md.gif](https://s2.ax1x.com/2019/03/30/AB754A.md.gif)](https://imgchr.com/i/AB754A)