---
title: Transact-sql 
date: '2021-12-13 09:06:00'
tags:
  - Transact-SQL
  - SQL server
categories: T-SQL
cover: /img/sql.jpg
abbrlink: 77b1bbb0
top_img: "#0f4c81"
---

## 实体

实体是客观事物真实反映，可以是实际存在的对象、抽象概念或事物
1. 属性
将事物特性称为实体属性
>性质相同的同类实体的集合称为实体集
2. 类型与值
属性类型就是属性名及其取值类型，属性值就是属性所取得具体值

## 实体间的联系

实体之间的对应关系称为联系，反映现实与事物之间的相互关联
类型：
一对一：1 ：1
（乘客与座位联系）
一对多联系：1 ：n
（公司与员工的联系）
多对多联系：m : n
（供应商与货物）

## 数据库文件

数据库是由数据文件和事务日志文件组成的，一个数据库至少应包含一个数据文件和一个事务日志文件
主数据文件*.mdf（仅有一个）、次数据文件*.ndf（零到多个）、事务日志文件*.ldf（一到多个）

# T-SQL语句

## 创、修、删数据库

## 最简单形式创建数据库（不指定文件）
```SQL
create database 数据库名称
```

### 创建指定数据文件和事务日志文件的数据库
```SQL
create database 数据库名称
on	//数据文件
(
	name = 逻辑名称,	//指定文件的逻辑名称
	filename='C:\sql_data\逻辑名称.mdf',	//指定路径，执行前，指定路径必须存在
	size=10MB,	//文件大小
	maxsize=50MB,	//文件可增加到的最大大小
	filegrowth=10%	//文件的自动增量
)
Log on	//日志文件
(
	name=日志文件名称,
	filename='C:\sql_data\日志文件名称.ldf',
	size=5MB,
	maxsize=10MB,
	filegrowth=1MB
)
```

### 修改数据库的设置
```SQL
alter database 数据库名称	//alter database语句可以完成对数据库的修改
modify file		//指定应修改的文件
(
	name=逻辑名称,
	size=15MB,
	maxsize=60MB,
	filegrowth=10%
)
```

### 数据库增加一个数据文件
```SQL
alter database Student
Add file
(
	name=逻辑名称1,
	filename='C:\sql_data\逻辑名称1.mdf',
)
```

### 数据库增加一个日志文件
```SQL
alter database 数据库名称
Add log file	//将要添加的日志文件到指定的数据库
(
	name=日志文件名称1,
	filename='C:\sql_data\日志文件名称1.ldf',
)
```

### 新增一个数据文件并放到用户自定义的文件组中
```SQL
alter database 数据库名称
Add filegroup
go 文件组名 		//向数据库中添加文件组
alter database 数据库名称
add file
(
	name=逻辑名称2,
	filename='C:\sql_data\逻辑名称2.mdf',
)
go
```

### 删除文件组
```SQL
alter database 数据库名 remove filegroup 文件组名;
```

### 删除数据库
```SQL
drop database 数据库名
```

## 创、改、删表

### 创建表
```SQL
use 数据库名
create table 表名
(
	employee_id char(4) not null,	//列名,数据类型，是否允许空值
)
```

### 插入数据
```SQL
use 数据库名
go
insert 表名
	values('数据1','数据2','数据3')
```

### 添加列
```SQL
use 数据库名
alter table 表名 add 列名 varchar(10)null
go
```

### 修改列数据
```SQL
update 表名 set 列名=char(10)
```

### 删除列
```SQL
delete from 表名 where 列名=''
```

## 语句查询

### 查询表所有信息
```SQL
Select * from 表名
```

### 三种方法改变查询列标题
```SQL
Select 学号=sno,sname 姓名,sex AS 性别,birthady AS 出生日期  from s
```

### 消除重复列
```SQL
Select distinct 学号=sno from s
```

### 显示前5条列信息
```SQL
Select top 5* from s
//显示前25%条学生记录信息
Select top 25percent * from s
```