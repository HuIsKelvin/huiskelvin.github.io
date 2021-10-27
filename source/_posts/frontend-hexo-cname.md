---
title: Hexo + Github Page 配置博客的个人域名
date: 2021-10-27 20:43:46
tags:
- blog
- hexo
---

如果有自己的域名，并解析到 Github Page 的域名（`your_name.github.io`）上时，直接使用 `hexo deploy` 部署博客，每次都会覆盖掉 `CNAME`。

以下将解决这个问题。

## 概览

在 `GitHub` 的 `repo` 中，设置 `GitHub Page` 并自定义自己的域名，如下图所示。

![github page setting cname](github_page_setting_cname.png)

但是这种方法，每次 `hexo deploy` 之后，都会覆盖掉生成的 `CNAME`。每次都要重新设置，非常麻烦。

解决方法：
1. 手动配置 `CNAME` 文件
2. `hexo-generator-cname` 插件

<!-- more -->

## 1 手动配置 `CNAME` 文件

在 `source` 文件夹下，创建 `CNAME` 文件，并写入自己的域名。

栗子，`CNAME` 文件：

```
hurk.top  # 我自己的域名
```

## 2 使用 `hexo-generator-cname` 插件

安装插件。

```bash
npm i hexo-generator-cname --save
```

然后，配置 `_config.yml` 文件。

```yml
# 启用插件
plugins:
- hexo-generator-cname

# 配置想用的域名
# 如果默认用 Github Page，则是 https://your_github_name.github.io
url: http://hurk.top
```

## 参考

- [github+hexo搭建自己的博客网站（七）注意事项（避免read.me，CNAME文件的覆盖，手动改github page的域名）](https://www.cnblogs.com/chengxs/p/7496265.html)
- [Hexo在部署到Github后CNAME文件会消失或改变的解决方法](https://blog.csdn.net/aealen/article/details/105516944)
