---
layout: post
title: "Day 68: AI 打造简易 SQL 数据库"
author: iosdevlog
date: 2025-12-03 00:42:02 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486295&idx=1&sn=ea784e13ea069472283b981a685521f1&chksm=f95c90d0ce2b19c699f5d4eafb8268a5e5e83d14f60fe0f12c1c1ff54063f6316bb10ca1c088#rd

Simple SQL Database

一个用 Python 实现的轻量级 SQL 数据库系统，支持基本的关系数据库功能。

截图

功能特性

✅ 表的创建和删除 (CREATE TABLE, DROP TABLE)

✅ 数据的增删改查 (INSERT, SELECT, UPDATE, DELETE)

✅ WHERE 子句条件过滤

✅ ORDER BY 排序

✅ 主键约束

✅ 数据持久化 (JSON 格式)

✅ 类型支持: INTEGER, TEXT, REAL

✅ 完整的错误处理

✅ 属性测试覆盖 (使用 Hypothesis)

安装

# 克隆仓库

git clone https://github.com/build-your-own-x-with-ai/Simple-SQL-Database

cd Simple-SQL-Database

# 创建虚拟环境

python3 -m venv venv

source venv/bin/activate  # Linux/Mac

# 或 venv\Scripts\activate  # Windows

# 安装依赖

pip install -r requirements.txt

使用方法

交互式 REPL

python -m simple_sql_db.repl

编程接口

from simple_sql_db.database import Database

# 创建数据库实例

db = Database(data_dir="my_data")

# 创建表

result = db.execute_sql("""

CREATE TABLE users (

id INTEGER,

name TEXT,

age INTEGER,

PRIMARY KEY(id)

)

""")

# 插入数据

db.execute_sql("INSERT INTO users (id, name, age) VALUES (1, 'Alice', 30)")

db.execute_sql("INSERT INTO users (id, name, age) VALUES (2, 'Bob', 25)")

# 查询数据

result = db.execute_sql("SELECT * FROM users WHERE age > 26")

for row in result.rows:

print(row)

# 更新数据

db.execute_sql("UPDATE users SET age=31 WHERE name='Alice'")

# 删除数据

db.execute_sql("DELETE FROM users WHERE name='Bob'")

# 删除表

db.execute_sql("DROP TABLE users")

# 关闭数据库

db.close()

支持的 SQL 语法

CREATE TABLE

CREATETABLE table_name (

column1 TYPE,

column2 TYPE,

PRIMARY KEY(column1)

)

INSERT

INSERTINTO table_name (col1, col2) VALUES (val1, val2)

SELECT

SELECT col1, col2 FROM table_name

SELECT*FROM table_name WHERE col1 >10

SELECT*FROM table_name ORDERBY col1

SELECT*FROM table_name WHERE col1 ='value'ORDERBY col2

UPDATE

UPDATE table_name SET col1=val1, col2=val2

UPDATE table_name SET col1=val1 WHERE col2 >10

DELETE

DELETEFROM table_name

DELETEFROM table_name WHERE col1 ='value'

DROP TABLE

DROPTABLE table_name

运行测试

# 运行所有测试

pytest tests/ -v

# 运行属性测试

pytest tests/test_properties.py -v

# 运行单元测试

pytest tests/test_unit.py -v

架构设计

系统采用分层架构：

┌─────────────────────────────────┐

│      SQL Interface Layer        │  ← 用户交互接口

├─────────────────────────────────┤

│         Parser Layer            │  ← SQL 解析

├─────────────────────────────────┤

│        Executor Layer           │  ← 查询执行

├─────────────────────────────────┤

│     Table Manager Layer         │  ← 表和数据管理

├─────────────────────────────────┤

│      Storage Engine Layer       │  ← 持久化存储

└─────────────────────────────────┘

核心组件

SQLParser

: 将 SQL 文本解析为抽象语法树 (AST)

QueryExecutor

: 执行解析后的 SQL 命令

TableManager

: 管理表结构和数据

StorageEngine

: 处理数据的持久化和加载

数据存储

数据以 JSON 格式存储在磁盘上，每个表对应一个 JSON 文件：

{

"name":"users",

"schema":{

"columns":[

{"name":"id","type":"INTEGER","is_primary_key":true},

{"name":"name","type":"TEXT","is_primary_key":false}

]

},

"rows":[

{"id":1,"name":"Alice"},

{"id":2,"name":"Bob"}

]

}

限制

单线程，不支持并发访问

无索引优化（全表扫描）

无查询优化器

适用于小型数据库（< 10,000 行/表）

WHERE 子句仅支持单个条件

许可证

MIT License

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTTz42WvLaDzGiaewUoTRARJeof6Lb27RYFiaetTd3Eic51hsmnZs8CjoeLMfzsuPxXRmjR7bwb6Sg9zg/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)
