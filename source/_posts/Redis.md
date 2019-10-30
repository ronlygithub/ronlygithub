---
title: Redis
date: 2019-09-11 23:16:08
tags: [Redis, NoSQL]
categories: database
---
# Redis 简介
Redis 是一个开源（BSD许可）的，内存中的数据结构存储系统，可以用作数据库、缓存和消息中间件。
**Redis 支持多种类型的数据结构：**
 - 字符串（String）
 - 散列（HashTable）
 - 列表（List）
 - 集合（Set）
 - 有序集合（Sorted Set）
   
**此外，Redis 提供了如下功能：**
 - 支持 Bitmaps， HyperLogLog 和 地理空间（geospatial） 索引半径查询
 - 复制（replication， LUA脚本（Lua scripting）， LRU驱动事件（LRU eviction），事务（transactions） 
 - 磁盘持久化（persistence）
 - 高可用，通过 Redis 哨兵（Sentinel）和自动分区（Cluster）提供高可用性（high availability）
  
# 数据结构
## 简单动态字符串 
Redis 采用 C 语言开发，Redis中的字符串没有采用 C 语言原生字符串，而是自定义了简单动态字符串 (Simple Dynamic String, SDS) 
## 链表
## 哈希表
## 跳表
## 压缩表
# 淘汰策略
# 持久化
# 事务
# 数据复制
# 高可用(哨兵)
# 应用场景