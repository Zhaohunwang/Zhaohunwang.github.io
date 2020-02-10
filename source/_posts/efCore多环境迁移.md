---
title: efCore多环境迁移
date: 2020-01-27 14:08:27
tags: ef core
category: ef
top_img: /Zhaohunwang.github.io/img/archive.jpg
---
Ef Core迁移数据库中，使用不同环境的连接字符串对数据库进行迁移

## 查看ef当前使用环境

```
dotnet ef dbcontext info
```

## 设置环境

#### windows

###### Console

```
set ASPNETCORE_ENVIRONMENT=环境名
```

###### Powershell

```
$Env:ASPNETCORE_ENVIRONMENT = "环境名"
```

## 进行迁移

```
dotnet ef migrations add InitialCreate
dotnet ef database update
```

参考资料

[1][在 ASP.NET Core 中使用多个环境](https://docs.microsoft.com/zh-cn/aspnet/core/fundamentals/environments?view=aspnetcore-3.1)

[2][迁移](https://docs.microsoft.com/zh-cn/ef/core/managing-schemas/migrations/?tabs=dotnet-core-cli)

