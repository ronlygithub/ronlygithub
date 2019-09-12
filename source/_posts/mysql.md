---
title: MySQL
date: 2019-09-04 22:14:49
tags: mysql 
categories: 数据库
---

## 索引
索引是数据库中用于加速数据查询的数据结构。MySQL 中在存储引擎层实现索引，不同的存储引擎索引实现方式不同。
### 全文索引
MyISAM 引擎支持全文索引，用以检索文本中的关键字，使用倒排索引实现。
### Hash索引
基于 Hash 表实现，可以在 O(1)时间复杂度下进行等值查询。
- 不支持排序和分组
- 仅支持等值查询，不支持范围查询。
- 不支持前缀匹配



   
  
### B-Tree索引 
目前大部分数据库采用 B-Tree 或其变种 B+Tree 实现索引。索引文件本身也很大，无法全部载入内存，需存储在磁盘。在数据检索时需将索引按块载入内存，产生磁盘IO。相比于内存读写，磁盘IO时间复杂度要高几个数量级。因此评价数据结构作为索引的优劣时最重要的一个指标就是磁盘IO次数渐进复杂度。索引实现时应尽量减少磁盘IO次数。
#### 数据结构

- B-Tree 即 平衡多路查找树(Balance Tree)。相比于二叉平衡树，每个节包含的关键字多了，可极大降低树的高度，并充分利用磁盘局部读写特性，加速数据库查询。
  - 非叶子节点中包含数据
- B+Tree 是B-Tree的变种，作为索引效率更高
  - 非叶子节点不保存数据，单个磁盘块中能保存更多节点，减少IO次数，提升查询性能。
  - 叶子节点通过指针顺序链接，提高区间查询性能
  
#### InnoDb 索引实现
#### MyISAM 索引实现
#### 索引优化

##### 索引覆盖
SQL 查询所需所有字段可通过索引获得，无需回表。
例如： 存在学生表如下所示
```sql
create table student(
    id int,
    name varchar,
    score Double,
    primary key('id'),
    key IDX_NAME('name')
) set engine=innodb;
```

查询：
```sql
select id,name from student where name = '张三 '
```
在 `name` 列存在辅助索引，且InnoDB存储引擎中辅助索引叶子节点包含主键的值。`id`,`name`  两列的值均可从辅助索引 IDX_NAME 中获得无需回表，符合索引覆盖的条件。

##### 索引下推

## 存储引擎
## 事务隔离级别
数据库通过加锁来保证事务的隔离级别。在MySQL中事务隔离级别包含如下四种：


事务隔离级别 | 脏读 | 可重复读 | 幻读 | 描述
---------|:--:|:--:|:--:|---
 读未提交 |  × | × |×| 事务 T<sub>1</sub> 读取事务 T <sub>2</sub>写入数据后，事务T回滚，读到脏数据。
 读已提交 | √ | × |×|事务 T<sub>1</sub>第一次及第二次读取之间，事务T<sub>2</sub>进行了提交，导致T<sub>1</sub>两次读取数据不一致。
 可重复读 | √ | √ |×|同一事务内多次查询结果保持一致，无法避免幻读
 串行读 | √ | √ |√| 事务读写串行进行，可避免幻读

 MySQL 实现：
 - 为避免加锁降低并发性能，MySQL 通过 MVCC 在读已提交和可重复读隔离级别实现了实现一致性快照读。同时通过 Nex-Key Locking 在可重复读隔离级别避免了幻读。读取到的数据可能时过时的数据
 - 串行读，采用悲观锁，所有事务串行进行操作，适合并发不高，对数据时效要求较高的场景。

## 锁
## MVCC

## 参考
[MySQL索引背后的数据结构及算法原理](http://blog.codinglabs.org/articles/theory-of-mysql-index.html)