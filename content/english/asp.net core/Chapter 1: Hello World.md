---
title: "Chapter 1: Hello World"
date: 2025-08-12T21:28:53+08:00
draft: false
---
编程语言的起点就是 Hello World！我们也不例外

首先打开 Visual Studio，选择新建项目，项目类型选择 ASP.NET Core（注意语言要是 C# 而不是 F#）

之后输入项目名称 HelloWorld，回车。取消 Enable OpenAPI support 和 Use controllers 的勾选

像这样

![](https://cdn.nlark.com/yuque/0/2025/png/21733593/1754549635899-4bb7c8a6-1e34-486c-b0a5-c6b144971777.png)

点击 Create 创建项目。我们的项目就建好了。



之后打开 Program.cs，可以看到初始化的项目代码是这样的

```csharp
var builder = WebApplication.CreateBuilder(args);

// Add services to the container.

var app = builder.Build();

// Configure the HTTP request pipeline.

app.UseHttpsRedirection();

var summaries = new[]
{
    "Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
};

app.MapGet("/weatherforecast", () =>
    {
        var forecast = Enumerable.Range(1, 5).Select(index =>
            new WeatherForecast(DateOnly.FromDateTime(DateTime.Now.AddDays(index)),
                Random.Shared.Next(-20, 55),
                summaries[Random.Shared.Next(summaries.Length)])).ToArray();
        return forecast;
    });

app.Run();

internal record WeatherForecast(DateOnly Date, int TemperatureC, string? Summary)
{
    public int TemperatureF => 32 + (int)(TemperatureC / 0.5556);
}

```



之后我们删除下面的代码

```csharp
var summaries = new[]
{
    "Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
};

app.MapGet("/weatherforecast", () =>
{
    var forecast = Enumerable.Range(1, 5).Select(index =>
        new WeatherForecast
        (
            DateOnly.FromDateTime(DateTime.Now.AddDays(index)),
            Random.Shared.Next(-20, 55),
            summaries[Random.Shared.Next(summaries.Length)]
        ))
        .ToArray();
    return forecast;
});

```

和

```csharp
internal record WeatherForecast(DateOnly Date, int TemperatureC, string? Summary)
{
    public int TemperatureF => 32 + (int)(TemperatureC / 0.5556);
}
```



让 program.cs 变成这样

```csharp
var builder = WebApplication.CreateBuilder(args);

// Add services to the container.

var app = builder.Build();

// Configure the HTTP request pipeline.

app.UseHttpsRedirection();

app.Run();

```

除去 `//` 注释之外，只有 4 行代码，这就是 asp.net core 的初始框架了。



我们在 app.Run() 之前，加入一段代码

`app.MapGet("/", () => "Hello World!");`

让 Program.cs 变成这样

```csharp
var builder = WebApplication.CreateBuilder(args);

// Add services to the container.

var app = builder.Build();

// Configure the HTTP request pipeline.

app.UseHttpsRedirection();

app.MapGet("/", () => "Hello World!");

app.Run();

```



之后点击运行。可以看到运行的弹窗

![](https://cdn.nlark.com/yuque/0/2025/png/21733593/1754550015631-9230b0f0-164f-4730-8895-ca65388e1517.png)



然后我们在浏览器中输入 `https://localhost:7225/`如果你本地的端口和我们的不一样，使用弹出提示的端口

之后就可以看到

![](https://cdn.nlark.com/yuque/0/2025/png/21733593/1754550214899-2e43d968-d2d2-4161-847a-44036c1a8874.png)

我们的 Hell World！ 运行成功啦！

恭喜！

我们的 hello world 做出来啦！（此处应有掌声）



总结：

这篇文章以最快的速度做出来了一个 ASP\.NET Core 程序，实现了 Hello World！ 的输出。

当然，你的内心可能有疑问，例如：

为什么 Hello World！要放在浏览器里面访问才能拿到？

前面的哪些代码是干嘛用的？

这个 app.MapGet 是什么？

以及为什么我们要取消 Enable OpenAPI support 和 Use controllers 的勾选？我要是勾上它们会怎样？

还有一个 Do not use top-level statements 的选项是干什么用的？

接下来的第二篇文章，我们会提出一些进阶的知识，同时会回答这些问题。


