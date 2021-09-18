---
title: Golang - 在 Gin 中自定义中间件
date: 2021-09-18 20:24:28
tags: Golang
---

## 0x01 引言

[Gin](https://github.com/gin-gonic/gin) 是一个基于 Golang 的网络框架，不仅具有高性能，而且极易使用。它比另一个 Golang 的常见的 HTTP 框架 [HttpRouter](https://github.com/julienschmidt/httprouter) 速度快了将近 40 倍。

使用 Gin，可以快速启动一个高效的 HTTP 服务。

```golang
package main

import "github.com/gin-gonic/gin"

func main() {
    // 初始化 Gin 的实例
    r := gin.Default()

    // 注册路由
    // GET /ping
    r.GET("/ping", func(c *gin.Context) {
        // 以 Json 格式返回数据
        c.JSON(200, gin.H{
            "message": "pong",
        })
    })

    // 启动服务
    // listen and serve on 0.0.0.0:8080 (for windows "localhost:8080")
    r.Run()
}
```

## 0x02 Gin 中的中间件

使用 `gin.Default()` 初始化的实例，已经默认使用了 2 个中间件 `gin.Logger()` 和 `gin.Recovery()`。

`gin.New()` 则返回没使用任何中间件的 Gin 实例。

```golang
r1 := gin.Default()

// 等价于
// 完全空白的 gin 实例
r2 := gin.New()
// Logger() 输出 gin 运行时的日志
r2.Use(gin.Logger())
// 当程序 panic 时，Recovery() 自动返回网络状态码为 500 的响应
r2.Use(gin.Recovery())
```

## 0x03 自定义中间件

可以自定义中间件，根据业务要求对请求做不同处理。

自定义中间件步骤：

1. 定义一个函数来做中间件，该函数返回值为 `gin.HandlerFunc`。
2. 在启动服务 `Run()` 前，注册该中间件。

### gin.HandlerFunc

`gin.HandlerFunc` 的原型如下

```golang
// HandlerFunc defines the handler used by gin middleware as return value.
type HandlerFunc func(*Context)
```

在实际使用时，参数一般使用 gin.Context。

在 `gin.HandlerFunc()` 中，需要调用 `func (c *Context) Next()`，将请求传入中间件链的后面，以继续处理。否则，该请求的处理到这个中间件为止，后面的业务逻辑均无效。

### 例子

```golang
// CalculateLatency() 计算该请求的处理耗时
func CalculateLatency() gin.HandlerFunc {
    return func(c *gin.Context) {
        // 记录当前时间
        timeBefore := time.Now()

        // 后续逻辑处理此请求
        c.Next()

        // 处理完毕后，计算耗时
        latency := time.Since(timeBefore)
        log.Print(latency)
    }
}

func main() {
	r := gin.New()
    // 注册中间件
	r.Use(CalculateLatency())

    // 注册路由
	r.GET("/test", func(c *gin.Context) {
		c.JSON(100, "hello, custom middleware!")
	})

    // 启动服务，监听 8080 端口
	r.Run(":8080")
}
```

## 参考：
- [https://github.com/gin-gonic/gin](https://github.com/gin-gonic/gin)
- [Gin custom middleware](https://github.com/gin-gonic/gin#custom-middleware)
