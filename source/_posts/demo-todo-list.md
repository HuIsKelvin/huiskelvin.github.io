---
title: 一个 todo list 的小 demo
date: 2019-04-13 23:14:20
tags:
description: Todo list
---

# todo list

## 功能需求

- 新增待做事项
- 删除待做事项
- 搜索，并在列表中高亮检索词

## 实现效果

![ALxjlq.jpg](https://s2.ax1x.com/2019/04/13/ALxjlq.jpg)

## 具体实现

- Dom操作
- Js事件监听

## 源码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>To do list</title>
    <style>
        #app {
            width: 400px;
            margin: 0 auto;
            text-align: center;
        }

        #app .app-title {
            text-transform: capitalize;
        }
        
        #add-to-do,
        ul[id="list"] {
            width: 300px;
        }

        #add-to-do {
            height: 30px;
        }

        ul[id="list"] {
            text-align: left;
            list-style: none;
            margin: 20px auto;
            padding: 0;
        }

        #list li {
            padding: 5px;
            margin: 2px 0;
            background-color: #eee;
        }

        #list li:hover {
            background-color: #e0e0e0;
        }

        #list span[class="del"] {
            float: right;
            cursor: pointer;
        }

        #list span[class="hl"] {
            color: red;
        }
    </style>
</head>

<body>
    <div id="app">
        <h1 class="app-title">to do list</h1>
        <input type="text" id="add-to-do" placeholder="add thing to do">
        <ul id="list"></ul>
    </div>
    <script>
        window.onload = function () {
            var add = document.getElementById("add-to-do");
            var list = document.getElementById("list");
            // 存储待做事项
            var items = [];

            // 新增待做事项
            add.onkeydown = function (e) {
                if (e.keyCode === 13) {
                    removeList();
                    var val = add.value;
                    items.push(val);
                    showList("");
                    add.value = "";
                }
            }

            // input输入改变时，高亮
            add.addEventListener("input", function() {
                redrawList(add.value);
            })

            list.addEventListener("click", function(e) {
                // 删除待做事项
                if(e.target.className === "del") {
                    // var parent = e.target.parentNode;
                    // var index = (parent.id.split("-"))[1];
                    var index = (e.target.id.split("-"))[1];
                    items.splice(index, 1);
                    redrawList("");
                }
            })

            function redrawList(val) {
                removeList();
                showList(val);
            }
            function removeList() {
                var lis = document.querySelectorAll("#list li");
                for (var i of lis) {
                    list.removeChild(i);
                }
            }
            function showList(val) {
                if (items) {
                    for (var i = 0; i < items.length; i++) {
                        var text = items[i];
                        // 若需要匹配val
                        if(val) {
                            var reg = new RegExp(val, 'g');
                            text = text.replace(reg, "<span class='hl'>" + val + "</span>");
                        }
                        // create li element
                        var elemLi = document.createElement("li");
                        elemLi.innerHTML = text + "<span id='del-" + i+ "' class='del'>x</span>";
                        list.appendChild(elemLi);
                    }
                }
            }
        }
    </script>
</body>

</html>
```