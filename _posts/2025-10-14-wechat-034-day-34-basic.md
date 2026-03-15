---
layout: post
title: "Day 34: 打造自己的 BASIC 解释器"
author: iosdevlog
date: 2025-10-14 23:59:04 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247485952&idx=1&sn=35b23aa5271b7fde199a7d55b3ec66c1&chksm=f95c9187ce2b189179bb8e8482782af5960ed2d8fbfd58ac846005e9e58dce49d0df7ad66083#rd

BASIC 解释器

一个使用 Swift 和 SwiftUI 为 macOS 构建的全功能 BASIC 语言解释器。该解释器支持经典的 BASIC 程序，包括来自 Basic Computer Games 仓库的程序。

功能特性

支持的 BASIC 关键字

基于经典的 BASIC 语言规范：

关键字

英文

描述

LET

LET

变量赋值

IF/THEN

IF/THEN

条件执行

GOTO

GOTO

跳转到行号

GOSUB

GOSUB

调用子程序

RETURN

RETURN

从子程序返回

FOR/TO/STEP/NEXT

FOR/TO/STEP/NEXT

循环结构

PRINT

PRINT

输出文本

INPUT

INPUT

读取用户输入

DATA/READ/RESTORE

DATA/READ/RESTORE

数据存储和检索

DIM

DIM

定义数组维度

DEF

DEF

定义函数

REM

REM

注释

STOP/END

STOP/END

程序终止

内置函数

数学函数：

ABS(x)

- 绝对值

INT(x)

- 整数部分

SQR(x)

- 平方根

SIN(x)

, COS(x), TAN(x), ATN(x) - 三角函数

EXP(x)

, LOG(x) - 指数和对数

RND

- 随机数 (0-1)

字符串函数：

LEN(s$)

- 字符串长度

VAL(s$)

- 将字符串转换为数字

STR$(n)

- 将数字转换为字符串

LEFT$(s$, n)

- 左子字符串

RIGHT$(s$, n)

- 右子字符串

MID$(s$, start, len)

- 中间子字符串

TAB(n)

- 间距

项目结构

BASIC/

├── BASIC/

│   ├── BASICToken.swift       # 令牌定义

│   ├── BASICLexer.swift       # 词法分析器

│   ├── BASICAST.swift         # AST 节点和表达式

│   ├── BASICParser.swift      # 语法解析器

│   ├── BASICContext.swift     # 运行时上下文

│   ├── BASICInterpreter.swift # 主解释器

│   ├── FileLoader.swift       # 文件 I/O 和示例

│   ├── ContentView.swift      # SwiftUI 界面

│   └── BASICApp.swift         # 应用程序入口点

构建和运行

从 Xcode：

在 Xcode 中打开 BASIC.xcodeproj

按 Cmd+R 构建和运行

解释器窗口将显示代码编辑器和输出面板

从命令行：

cd BASIC

xcodebuild -project BASIC.xcodeproj -scheme BASIC -configuration Debug build

open Build/Products/Debug/BASIC.app

使用方法

运行程序：

在左侧编辑器面板中输入或粘贴 BASIC 代码

点击 "Run" 按钮或按 Cmd+R

输出显示在右侧面板中

对于 INPUT 语句，底部将出现一个输入字段

示例程序：

点击 "Samples" 按钮加载预设的示例程序

示例包括：猜数字游戏、倒计时、计算器等

加载文件：

点击 "Open" 从磁盘加载 .BAS 文件

支持标准文本编码 (UTF-8/ASCII)

示例程序：

10 REM 猜数字游戏

20 PRINT"我想了一个 1 到 100 之间的数字"

30 LET N = INT(RND * 100) + 1

40 LET G = 0

50 INPUT"你的猜测"; G

60 IF G = N THENGOTO100

70 IF G < N THENPRINT"太小了!"

80 IF G > N THENPRINT"太大了!"

90 GOTO50

100 PRINT"正确! 你猜对了!"

110 END

架构

解释器流程：

词法分析器

(BASICLexer.swift)：将输入文本标记化

语法解析器

(BASICParser.swift)：构建抽象语法树

上下文

(BASICContext.swift)：管理运行时状态

解释器

(BASICInterpreter.swift)：执行解析后的程序

关键组件：

令牌类型

：关键字、运算符、字面量、标识符

表达式求值

：支持算术、逻辑和字符串操作

语句执行

：所有标准 BASIC 语句

控制流

：GOTO、GOSUB/RETURN、FOR/NEXT 循环

变量存储

：数字和带 $ 后缀的字符串

数组支持

：通过 DIM 实现多维数组

运行 basic-computer-games 中的程序

解释器与许多经典 BASIC 程序兼容。要运行仓库中的程序：

从 basic-computer-games 下载 .BAS 文件

某些程序可能需要轻微修改以确保兼容性：

如果出现问题，从 REM 语句中删除行号

确保 INPUT 提示正确引用

检查 PRINT 语句是否使用分号进行适当间距

键盘快捷键

Cmd+R

- 运行程序

Enter

- 提交输入（当输入字段处于活动状态时）

系统要求

macOS 26.0 或更高版本

Xcode 26.0 或更高版本用于构建

Swift 5.0

许可证

作为教育项目创建，用于实现 BASIC 编程语言。

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTRbKwha48946cza4ndicGRMyf2sDqrhXH7mX5iblXhyoDOIZTOLBtFiabceQlGxMRL1BCgjPicUaSH7pg/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)

![image-2](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTRbKwha48946cza4ndicGRMyWZF0biaHssZXJndUicS3PPHX8OnQyeNMalFN699U9BAIUt66rHhpdqYw/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=1)

![image-3](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTRbKwha48946cza4ndicGRMyeqNfD6DslKXU3YkpGFkeXh5tkbufwIGSu5U1bwuA8O4IdxficgaSQeQ/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=2)
