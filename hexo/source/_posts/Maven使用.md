---
title: Maven使用
date: 2019-08-08 18:10:01
tags: maven
categories: 工具
---

## Maven 常用命令
### 部署私服
```
mvn clean deploy -U -am -pl 模块名称
```

### 版本更新
- 修改父pom中版本号
- 执行如下命令将子模块版本号与父pom中保持一致

```
mvn -N version:update-child-modules
```


### 跳过测试
```
mvn compile -Dmaven.test.skip=true
```

