---
title: "Chapter 2: 关于 API"
date: 2025-08-14T21:31:28+08:00
draft: false
---

这是一篇理论文章，旨在说明我们在上节课做出的程序。

那么首先回答，为什么 Hello World！要在浏览器中得到？

我们做的是一个 API 程序。在点击运行时，我们的程序会侦听机器上面的端口，处理端口进来的请求。

使用浏览器就是模拟请求的过程，我们访问 `https://localhost:7225/`

就是访问我们的服务，之后就可以得到对应的返回值 "Hello World！"



前面的代码干嘛用的？

我们逐个解读

`var builder = WebApplication.CreateBuilder(args);`

这是创建构造器 builder 的语句，构造器可以添加服务

`var app = builder.Build();`

这是构造器创建应用程序实例的语句，app 就可以当作是我们的 API 项目的实例了，

`app.UseHttpsRedirection();`

app 使用了 (Use) 一个 Https 的重定向 Redirection，就是将 http 请求重定向为更安全的 https 请求。

这种 Usexxx 的语法就是使用中间件的形式。ASP\.NET core 框架的各种中间件都是这种形式 Use 进来的。

他们组成了一个管道（pipeline）。

有用户的请求进来，会像水管中的水一样，经过中间件组成的流入管道，到达我们的接口，生成响应，响应经过流出管道，最终返回给用户。



那么 app.MapGet 是干嘛的？

app 是我们的程序实例，MapGet 顾名思义，就是将 Get 请求映射到后边的函数。

Get 请求的地址就是 `/` 对应的函数是 `() => "Hello World!"`

意思就是说，如果有请求 `/`的，就执行后面的函数给它一个 Hello world！



为什么我们要取消 Enable OpenAPI support 和 Use controllers 的勾选？我要是勾上它们会怎样？

第一勾选上会加入一个 OpenAPI 的文档支持，只是我们当前不需要

第二个 Use controllers 我们会勾上的，只是要到后面。这个 Controller 和现在的 API 项目的组织形式有所不同。一般小型的项目不需要，等到接口变多了，要考虑拆分，就会把不同类型的接口，按照类型归并到不同的 Controller 中去。下一节，我们将开始使用 Controller，完成一个番茄时钟的接口设计。



Do not use top-level statements 是干嘛用的？

这个是以前 C# 程序的风格，启动的代码是在 Class Program.cs 的 Main 函数里面。现在默认是把这块语句拿出来了，让代码更简化了。



好了，解答了前面的问题，现在我们来了解一些概念。

什么是 API？

API 是 **A**pplication **P**romgramming **I**nterface 应用程序接口

在互联网环境，代表一个服务系统提供的接口，可以让别的系统通过这些接口来使用它。



什么是 API 的设计风格 RESTful？

RESTful 是一种软件架构风格，不是标准。**RE**presentational **S**tate **T**ransfer 代表状态转移。

REST 的核心是资源 Resource，资源通过 API 接口地址标记和定位，客户端通过 HTTP 方法操作这些资源。

