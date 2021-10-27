---
title: Hexo 博客中使用本地图片
date: 2021-10-26 20:25:27
tags:
- blog
- hexo
---

在 hexo 博客中插入博客，可以使用**图床**和**本地图片**两种方式。而图床可能由于网络原因导致加载问题，并且需要另外管理。所以，尝试使用本地的图片。

<!-- more -->

## 1 概览

在 hexo 搭建的博客中使用本地图片，主要有几种方式：

1. 在 `source/img` 文件夹中放置图片。
2. 使用插件 `hexo-asset-image`。

### 2 `source/img` 文件夹

在本地 `source` 文件夹下面，新建 `img` 文件夹，用于存放照片。

假设有一张照片 `source/img/logo.jpg`。

在文章的 `markdown` 中，使用

- `![logo](/img/logo.jpg)`
- `<img src="/img/logo.jpg">`

插入图片。

<img src="/img/logo.png" style="width:50px;margin:15px;">

上面<u>这张图片</u>就是以这种方式插入。

### 3 `hexo-asset-image` 插件

首先，安装插件 `hexo-asset-image`。

```bash
# npm install hexo-asset-image --save
npm install https://github.com/CodeFalling/hexo-asset-image --save
```

然后在 `_config.yml` 中加入 `post_asset_folder: true`。

之后，用`hexo new post_title`（post_title 就是文章标题）新建文章时，会在 `source/_post` 下生成一个同名文件夹 `source/_post/post_title`。可以把这篇文章用到的图片，放入此文件夹中，如图片 `test.png`。

那么，在文章的 markdown 中插入图片。

```markdown
![alt](test.png)
<!-- 或 -->
<img src="test.png">
```

<img src="test.png" style="width:50px;margin:15px;">

上面<u>这张图片</u>就是以这种方式插入。

### 参考

- [Hexo中添加本地图片](https://www.cnblogs.com/codehome/p/8428738.html?utm_source=debugrun&utm_medium=referral)
- [解决hexo-asset-image的图片地址错误问题](https://wangwei1237.github.io/2020/02/05/handle-the-bug-of-hexo-asset-image-plugin/)
