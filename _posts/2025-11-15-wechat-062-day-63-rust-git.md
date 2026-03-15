---
layout: post
title: "Day 63: Rust 编译 Git"
author: iosdevlog
date: 2025-11-15 23:26:08 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486206&idx=1&sn=0016ac200b6512fa698f73d9549dbc27&chksm=f95c9179ce2b186ff86187d7b52d80233759390cfff8933eb2be9ee1011394d7851b29f8d998#rd

rgit

一个用 Rust 从零实现的最小可用 Git，支持基本的版本控制操作和远程推送功能。

特性

✅ 完整的本地 Git 操作：init、add、commit、status、log

✅ 分支管理：branch、checkout

✅ 远程仓库：remote add、push

✅ 兼容标准 Git 对象格式（blob/tree/commit）

✅ 使用 zlib 压缩和 SHA-1 哈希

✅ 支持 SSH 和 HTTPS 协议推送

安装

确保已安装 Rust 工具链（≥1.75），然后克隆并编译：

git clone <repository-url>

cd rgit

cargo build --release

编译后的二进制文件位于 target/release/rgit。

使用方法

初始化仓库

rgit init

添加文件到暂存区

rgit add <文件路径>

提交更改

rgit commit -m "提交信息"

查看状态

rgit status

查看提交历史

rgit log

分支操作

# 创建新分支

rgit branch <分支名>

# 切换分支

rgit checkout <分支名>

远程操作

# 添加远程仓库

rgit remote add <远程名> <URL>

# 推送到远程

rgit push <远程名> <分支名>

完整示例

# 初始化仓库

rgit init

# 添加文件

echo"Hello, rgit!" > README.txt

rgit add README.txt

# 提交

rgit commit -m "Initial commit"

# 添加远程仓库

rgit remote add origin git@github.com:username/repo.git

# 推送到远程

rgit push origin main

技术实现

核心模块

repo.rs

- 仓库初始化、配置管理

objects.rs

- Git 对象（blob/tree/commit）的编码/解码

index.rs

- 最小暂存区实现

refs.rs

- 引用（HEAD、分支）管理

pack.rs

- 打包对象处理

push.rs

- 远程推送实现

pktline.rs

- Git 协议行处理

依赖库

clap

- 命令行参数解析

anyhow

- 错误处理

tracing

- 日志记录

flate2

- zlib 压缩

sha1

- SHA-1 哈希

walkdir

- 目录遍历

chrono

- 时间处理

对象存储

所有 Git 对象遵循标准格式：

<类型> <长度>\0<内容>

使用 zlib 压缩后存储在 .git/objects/xx/yyyy... 路径下。

远程推送

支持通过 SSH 和 HTTPS 协议推送：

SSH

- 使用本机 ssh-agent 或私钥文件（~/.ssh/id_rsa、~/.ssh/id_ed25519）

HTTPS

- 支持 token 或密码认证

调试模式

使用 --verbose 标志启用详细日志：

rgit --verbose commit -m "详细日志模式"

限制与假设

采用最小暂存区实现，不支持完整的 Git index 二进制格式

推送操作针对当前分支，不支持复杂的 rebase/merge 场景

不支持交互式认证，需预先配置 SSH 密钥或环境变量

使用 SHA-1 哈希算法（与标准 Git 兼容）

后续计划

[ ] 完整的 index 二进制格式支持

[ ] 支持 merge 和 rebase 操作

[ ] 实现自定义协议层（pkt-line/packfile）

[ ] 支持 SHA-256 模式

[ ] 性能优化与增量传输

[ ] 更丰富的进度显示

许可证

本项目采用 MIT 许可证 - 详见 LICENSE 文件。

贡献

欢迎提交 Issue 和 Pull Request！

致谢

本项目是一个教育性质的 Git 实现，旨在深入理解 Git 内部机制。

https://github.com/build-your-own-x-with-ai/rust_git

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTQwQyupngaTn0c4vc0Taxspr7YlmNvl8Uib93sPbAdVmpF9vr96p8T64HOvsrWHRcviaDVKLhQEPcUQ/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)
