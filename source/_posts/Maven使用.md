---
title: Maven使用
date: 2019-08-08 18:10:01
tags: maven
categories: 工具
---



## Maven 常用命令

### 常用参数

- -D 指定参数，如 -Dmaven.test.skip=true 跳过单元测试；

- -P 指定 Profile 配置，可以用于区分环境；

- -e 显示maven运行出错的信息；

- -o 离线执行命令,即不去远程仓库更新包；

- -X 显示maven允许的debug信息；

- -U 强制去远程更新snapshot的插件或依赖，默认每天只更新一次。


### 部署远程仓库
```
mvn clean deploy -U -am -pl 模块名称
```

### 版本更新
- 修改子模块版本号与父pom中保持一致

```
mvn -N versions:update-child-modules
```
- 同时修改父模块与子模块版本号

```
mvn versions:set -DnewVersion=0.0.2-SNAPSHOT
```


### 跳过测试
```
mvn compile -Dmaven.test.skip=true
```

