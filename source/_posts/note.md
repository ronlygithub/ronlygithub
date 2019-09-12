---
title: note
date: 2019-09-03 19:06:06
tags:
categories:
---

- 数据源对应的数据库连接池管理。由于系统中将会定义多个数据源，需要对这些数据源采用一定的策略进行管理。初步方案是：单机（LRU + WeakCache)策略 + JSF层根据dbid路由到不同的机器上。这样，数据源连接池总体分散在集群各个机器上，同时单机可以配置管理的数据源大小，并利用WeakCache机制进行一定程度的复用。目前，单机（LRU + WeakCache）功能已经完成，详情见LruCachedDataSoruceFactory


-   开发中心SQL模式下，需要对用户输入的SQL进行解析及校验，以避免不合规的SQL出现。需要分别对MySQL、Kylin、Presto按各自的语法进行处理，因此需要熟悉各自SQL解析引擎。本周完成MySQL及Presto SQL 解析引擎的调研，并基于此完成开发中心SQL模式下的SQL解析、校验、执行后端程序及接口程序的开发，并进行了初步测试。目前的SQL解析、校验的内容包括：
① 非查询语句的校验，包括不支持select into, select for update
② SQL语句中使用的表校验，非用户申请的表不允许SQL执行
③ SQL中的宏变量校验，检验SQL中的宏变量是否为后端支持的宏变量
④ SQL校验过程中的宏变量及SQL参数的替换 ⑤ SQL执行过程中的命名SQL及参数生成
4.      后端SQL宏变量的机制建立。目前只是建立基本的机制，后续需要丰富可用的SQL宏，并提供根据SPI机制或者自定义扫描策略自动进行SQL宏的注册。