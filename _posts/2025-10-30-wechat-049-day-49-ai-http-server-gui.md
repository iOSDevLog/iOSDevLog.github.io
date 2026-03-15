---
layout: post
title: "Day 49: AI 打造 HTTP Server GUI 服务器"
author: iosdevlog
date: 2025-10-30 22:16:27 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486069&idx=1&sn=340fedb651dc95d3adfde1b8e5a63d20&chksm=f95c91f2ce2b18e4e2cf2f4bbca25e0654f5063c2baadc9f3ee983f5b6257408464b19553939#rd

HTTP Server GUI 服务器

一个跨平台的桌面应用程序，为管理 Caddy HTTP 服务器实例提供图形界面。轻松通过 HTTPS 提供文件服务，自动生成证书。

截图

下载

链接: https://pan.baidu.com/s/1hjvHDnAHsCuQhaC5K1LMeQ?pwd=3kxq 提取码:3kxq

功能特性

🚀 快速设置 - 选择目录后几秒钟即可开始服务

🔒 自动 HTTPS，使用自签名证书

📁 文件浏览器模式，便于文件共享

🌐 网站模式，用于提供静态网站服务

📊 实时服务器日志

🖥️ 跨平台支持（Windows、macOS、Linux）

⚙️ 可配置端口和设置

📋 一键复制服务器 URL

安装

下载预编译版本

下载适合您平台的最新版本：

Windows: HTTPS-Server-Setup-1.0.0.exe

macOS: HTTPS-Server-1.0.0.dmg

Linux: HTTPS-Server-1.0.0.AppImage

从源码构建

要求：

Node.js 18+

npm 或 yarn

# 克隆仓库git clone https://github.com/build-your-own-x-with-ai/caddy-gui-server.gitcd caddy-gui-server# 安装依赖npm install# 下载 Caddy 二进制文件（参见 resources/README.md）# 构建应用npm run build# 为您的平台打包npm run package

截图

应用构建并运行后将添加截图。请参阅 resources/screenshots/README.md了解如何生成截图。

使用方法

启动服务器

启动 HTTP Server GUI 服务器

点击"浏览"选择要提供服务的目录

配置端口（默认：8443）

点击"启动服务器"

通过显示的 HTTPS URL 访问您的服务器

服务器模式

网站模式：如果您的目录包含 index.html或 index.htm，服务器将作为网站提供服务。

文件浏览器模式：如果未找到索引文件，服务器将显示文件浏览器界面，您可以：

浏览目录

下载文件

上传文件

查看文件元数据

查看日志

点击"日志"选项卡查看实时服务器活动，包括：

HTTP 请求

错误和警告

服务器状态变化

按级别（信息、警告、错误）过滤日志或搜索特定消息。

设置

在设置选项卡中配置应用程序首选项：

主题（浅色、深色、系统）

启动时自动启动服务器

日志级别

开发

项目结构

├── src/

│   ├── main/           # Electron 主进程

│   ├── renderer/       # React UI

│   └── shared/         # 共享类型和工具

├── resources/          # Caddy 二进制文件和资源

├── dist/              # 编译输出

└── release/           # 打包的应用程序

开发脚本

# 启动开发服务器npm run dev# 生产构建npm run build# 打包应用程序npm run package# 为特定平台打包npm run package:win npm run package:mac npm run package:linux

添加 Caddy 二进制文件

从 https://github.com/caddyserver/caddy/releases 下载 Caddy v2

将二进制文件放在 resources/目录中：

caddy-windows.exe

caddy-macos

caddy-linux

在 macOS/Linux 上设置可执行权限：

chmod +x resources/caddy-macos chmod +x resources/caddy-linux

故障排除

端口已被占用

如果看到"端口已被占用"错误：

尝试不同的端口号

检查是否有其他应用程序正在使用该端口

错误消息将建议替代端口

权限被拒绝

如果看到权限错误：

确保您对所选目录具有读取权限

在 macOS/Linux 上，检查目录权限

尝试选择不同的目录

服务器无法启动

验证 Caddy 二进制文件存在于 resources 目录中

检查日志以获取详细的错误消息

确保端口在 1024-65535 之间

尝试重启应用程序

证书警告

访问 https://localhost时，您的浏览器会显示安全警告，因为证书是自签名的。这是正常的。

Chrome/Edge：

点击"高级"

点击"继续访问 localhost（不安全）"

Safari：

点击"显示详细信息"

点击"访问此网站"

可能需要输入 macOS 密码确认

Firefox：

点击"高级"

点击"接受风险并继续"

永久信任证书（macOS）：

在 Safari 证书警告对话框中点击"显示证书"

将证书拖到桌面

双击证书文件，添加到"钥匙串访问"

在钥匙串中找到该证书，双击打开

展开"信任"部分，选择"始终信任"

安全注意事项

应用程序使用自签名证书为 localhost 提供 HTTPS

端口选择限制在 1024-65535（非特权端口）

目录路径经过验证以防止遍历攻击

Caddy 进程以最小权限运行

许可证

MIT 许可证 - 详见 LICENSE 文件

致谢

构建工具：

Electron

React

Caddy

TypeScript

支持

如有问题和功能请求，请访问：

关于

作者：AIDevLog

主页：https://github.com/build-your-own-x-with-ai/HTTPS-Server

微信公众号：AIDevLog

扫码关注 AIDevLog 微信公众号

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTQiaOQDEN3ylpfEMsx7mVhUnPQzyKAosY48SHlbbG6icAlmWjVhqMNpPaFxSSluOjzicKiayw0l0Gaqkw/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)

![image-2](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTQiaOQDEN3ylpfEMsx7mVhUnutyRwVryPiaX2rvL7dujy6DDOnuSsc55nVCljGyMlthy38DCHAC4Bug/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=1)

![image-3](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTQiaOQDEN3ylpfEMsx7mVhUnwqa2FzYR2gNicRHGJrQDSDJbGAzohJQqicqDXKPpcQnPmm28golHMDHA/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=2)

![image-4](https://mmbiz.qpic.cn/sz_mmbiz_jpg/kIE7WtwNFTQiaOQDEN3ylpfEMsx7mVhUnLDaOa6iaPibrc93b8CkWyEDQXe94wsmy2SURdiazo0v8DKqcB5r7hm2vQ/640?wx_fmt=jpeg&from=appmsg&watermark=1#imgIndex=3)
