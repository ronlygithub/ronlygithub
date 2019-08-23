---
title: Security Framwork
date: 2019-08-23 10:46:55
tags: security
categories:
---
# Apache Shiro
Apache Shiro 是一个灵活且功能丰富的开源安全框架，支持鉴权、授权、session管理、加密等功能。Apache Shiro 致力于尽可能通过框架屏蔽复杂性，对外提供简洁的API，帮助开发者在应用安全方面的工作量。

## Apache Shiro Features

![features](./Security-Framwork/ShiroFeatures.png)

四个主要特性
- Authentication(鉴权): 鉴定用户身份，可归类于登录
- Authorization(授权):  访问控制处理，决定`谁`可以访问`什么`
- Session Management: 管理用户 session
- Cryptography(加密)：通过加密算法对数据进行加密，保证数据安全

其他特性：
- Web Support: web support api 方便的对web应用提供安全保护
- Caching：API层添加缓存，保证安全相关操作快速高效
- Concurrency: 支持多线程应用
- Testing：便于开发者开发单元及集成测试
- Run As：允许用户模拟其他用户的身份
- Remember Me：在session中保存用户身份信息

## Apache Shiro Architecture



## 参考
[Apache Shiro Architecture](http://shiro.apache.org/architecture.html)
