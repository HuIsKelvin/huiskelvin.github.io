---
title: Duplicate repetitive elements in array
date: 2019-04-03 22:36:13
tags: 
  - 算法
---

去除数组中重复元素

# 描述

去除数组中重复元素，并得到被删除元素的数组。

```
input:
[1, 2, 1, 5, 2, 6, 1]
```

```
output:
[1, 2, 1]

// 被删除的数组中有重复值
```

# JavaScript实现

```js
// 原数组
var arr = [1, 2, 1, 5, 2, 6, 1];
// 被删除元素的数组
var removed = [];

arr.forEach(function(e, index) {
  if(arr.indexOf(e) !== index) {
    arr.splice(index, 1);
    removed.push(e);
  }
});

```
