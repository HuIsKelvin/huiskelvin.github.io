---
title: Linux 创建新用户
date: 2021-09-22 19:26:00
tags: Linux
excerpt: Linux 创建新用户的命令：useradd、adduser。
---

## 1 常用命令

创建用户：

- `useradd`
- `adduser`

区别：
- `useradd` 需要使用参数选项指定基本设置，如果不使用任何参数，则创建的用户无密码、无主目录、没有指定shell版本。
- `adduser` 会自动为创建的用户指定主目录、系统shell版本，会在创建时输入用户密码。

## 2 useradd

`useradd` 命令用于在 `Linux` 下创建新用户。

<增加 useradd 的参数介绍>

## 3 adduser

`adduser` 与 `useradd` 指令为同一指令（经由符号连结 symbolic link）。

<使用介绍>

# 参考：

- [linux用户管理（1）—创建用户（adduser和useradd）和删除用户（userdel）](https://blog.csdn.net/beitiandijun/article/details/41678251)
