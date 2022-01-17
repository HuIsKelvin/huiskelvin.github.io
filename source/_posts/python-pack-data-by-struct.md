---
title: python-基于 struct 模块的自定义网络协议打包和解包
date: 2021-12-30 21:19:30
tags:
- python
- 网络传输
---

`python` 中的 `struct` 模块主要是用来处理 `C` 结构数据的。使用该 `struct` 模块，将 Python 数据打包为二进制数据，或者将二进制数据解包为 Python 数据，可用于网络的二进制流传输。

<!-- more -->

## struct 模块

`struct` 的使用和相关 `api` 可以查看[官方文档](https://docs.python.org/zh-cn/3/library/struct.html)。

## 自定义网络协议

在实际使用中，一般会自定义自己的网络协议，以实现业务需求。一个数据包中包括协议头和数据内容两部分。

一个最简单的协议头可以包括：数据包类型 `type` 和数据内容长度 `content length`。

一个简单例子：

```python
import struct

""" 协议头的相关变量 """
# 数据包类型
header_type = "t01".encode("utf-8")     # 注意，pack 时的字符串 string 要先转换为字节类型
# 数据内容长度
header_content_len = 0
# 协议头自己的长度
header_len = (len(header_type)+1) + 4

""" pack """
# 传输的数据
msg = "HelloStruct".encode("utf-8")

# pack
header_content_len = len(msg)
pack_formatter = "{}si{}s".format(len(header_type),
                                header_content_len)
# 获取二进制数据
pack_bytes = struct.pack(pack_formatter, 
                        header_type, 
                        header_content_len, 
                        msg)

print("pack msg: {}".format(msg))   # pack msg: b'HelloStruct'

""" unpack """
# 解包读取协议头
unpack_formatter = "{}si".format(len(header_type))
unheader_type, unpack_content_len = struct.unpack_from(unpack_formatter, 
                                                    pack_bytes, 
                                                    offset=0)

# 根据协议头读取传输的数据内容
unpack_msg, = struct.unpack_from(f"{unpack_content_len}s", 
                                pack_bytes, 
                                offset=header_len)

print("get msg: {}".format(unpack_msg.decode("utf-8")))  # get msg: HelloStruct

```

## 参考

- [struct --- 将字节串解读为打包的二进制数据](https://docs.python.org/zh-cn/3/library/struct.html)
