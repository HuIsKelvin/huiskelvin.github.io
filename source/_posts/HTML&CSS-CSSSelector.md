---
title: 《HTML5与CSS3基础教程》笔记—定义选择器
date: 2019-01-12 20:43:30
tags: CSS
description: CSS的选择器
---

待更新...

## 按类或ID选择元素



## 按上下文选择元素
在 CSS 中，可以根据元素的祖先、父元 素或同胞元素来定位它们。
**祖先**（ancestor）是包含目标元素（**后代**，descendant）的任何元素，不管它们之间隔了多少代。（父元素是直接包含另一个元素的元素，它们之间只隔一代，被包含的元素称为子元素。）
```css
/*
这里组合使用了类选择器和类型选择器。
.architect 和 p 之间的空格表示这个选择器会寻找任何作为 architect 类元素后代（无论是第几代）的 p 元素。
*/
architech p {
  color: red;
}

/*
是任意 article 祖先的所有p元素，
这是三个中特殊性最低的一个
*/
article p {
  color: red;
}

/*
属于 architect 类 article 元素的祖先的任意p元素，
是三个中特殊性最高的一个
*/
article.architect p {
  color: red;
}
```

### 按祖先元素选择要格式化的元素
1. 输入ancestor，这里的 ancestor 是希望格式化的元素的祖先元素的选择器。 
2. 输入一个空格（必不可少）。 
3. 如果需要，对后续的每个祖先元素重复第 (1) 步和第 (2) 步。 
4. 输入descendant，这里的 descendant 是希望格式化的元素的选择器

```css
/*
这里 article 就是 ancestor，p 是 descendant。
*/
article p {
  color: red;
}
```
>我们通常将基于元素祖先的选择器称为后代选择器，不过 CSS3 将其重新命名为后代结合符。

### 按父元素选择要格式化的元素

### 按相邻同胞元素选择要格式化的元素


## 选择第一或最后一个子元素


## 选择元素的第一个字母或者第一行


>**伪元素、伪类及 CSS3 语法** 
在 CSS3 中，:first-line 的语法为 ::first-line，:first-letter 的语法为 ::firstletter。注意，它们用两个冒号代替了单个冒号。这样修改的目的是将伪元素（有四个， 包 括 ::first-line、::first-letter、::before 和 ::after） 与 伪 类（ 如 :first-child、 :link、:hover 等）区分开。 
**伪元素**（pseudo-element）是 HTML 中并不存在的元素。例如，定义第一个字母或第一行文字时，并未在HTML中作相应的标记。它们是另一个元素（在本例中为 p 元素）的部分 内容。
相反，**伪类**（pseudo-class）则应用于一组 HTML 元素，而你无需在 HTML 代码中用类标记它们。例如，使用 :first-child 可以选择某元素的第一个子元素，你就不用写成 class="first-child"。更多关于伪类的内容，请参见下一节。 

>未来，::first-line 和 ::first-letter 这样的双冒号语法是推荐的方式，现代浏览器也支持它们。原始的单冒号语法则被废弃了，但浏览器出于向后兼容的目的，仍然支持它们。 不过，IE9 之前的 Internet Explorer 版本均不支持双冒号。因此，你可以选择继续使用单冒 号语法，除非你为 IE8 及以下版本设置了单独的

## 按状态选择链接元素


## 按属性选择元素


## 指定元素组


## 组合使用选择器