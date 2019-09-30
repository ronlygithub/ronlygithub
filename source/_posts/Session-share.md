---
title: Session-share
date: 2019-09-19 11:22:23
tags: session
categories: network
---

# 一、Session
HTTP 是无状态协议，无法记录用户信息。Session 将用户信息保存在服务端，并通过SessioId唯一标识用户与服务器的会话。
# 二、Session 共享
## Sessio 复制
Web 服务器间同步复制 Session，当请求到不同的服务器时均可
## Session 粘连
通过一致性hash等方式，使得同一个请求落在同一服务器上。
优点：简单，无需其他开发、配置。
缺点：存在单点故障风险，若当前服务器故障则session丢失。
## Session 数据库存储
将Session存储到Redis等分布式缓存中，各个服务器从存储器中查询。

## Session Cookie存储
Session 经过加密、序列化处理后存储放到Cookie中，存储在一级域名下。
缺点：受限于HTTP头部大小限制，每次请求中需携带相关信息，占用带宽。

