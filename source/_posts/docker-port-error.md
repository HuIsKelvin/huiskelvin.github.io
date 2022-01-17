---
title: docker - 端口映射出现错误
date: 2021-11-19 16:08:37
tags:
- docker
---

## 背景

遇到一个情况，在 `docker` 启动容器时，进行端口映射，出现以下错误

```bash
Error response from daemon: driver failed programming external connectivity on endpoint quirky_allen
```

## 原因

根据网上的资料说，

> docker服务启动时定义的自定义链 DOCKER由于某种原因被清掉。
> 重启docker服务及可重新生成自定义链 DOCKER。

## 解决

重启 `docker` 服务，再启动容器。

```bash
systemctl restart docker
```

### 参考：

- [docker端口映射或启动容器时报错 driver failed programming external connectivity on endpoint quirky_allen](https://blog.csdn.net/whatday/article/details/86762264)
