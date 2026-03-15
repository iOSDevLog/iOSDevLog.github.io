---
layout: post
title: "Day 18: 打造自己的 Windows 视频桌面背景"
author: iosdevlog
date: 2025-09-18 23:58:31 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247485804&idx=1&sn=0c3c79b7681b88fcaf2dba4a6a262505&chksm=f95c92ebce2b1bfd59d902763adb3737b66bb9db85ee870de4a74985a1b7c9758a3a52d2f801#rd

视频壁纸应用程序项目完成总结

项目概述

本项目实现了一个视频壁纸应用程序，可以将用户选择的视频文件作为桌面背景播放。应用程序具有系统托盘集成、真正的视频播放功能，并且不会遮挡其他应用程序。

已实现的功能

核心功能

系统托盘集成（最小化到系统托盘、右键菜单控制）

真正的视频播放功能（使用VLC.NET）

视频壁纸正确显示在桌面背景层级，不会遮挡任务栏和桌面图标

支持多种视频格式（MP4, AVI, MOV等）

支持创建桌面快捷方式

启动时自动运行选项

2. 用户体验改进

支持创建桌面快捷方式

简单直观的上下文菜单（选择视频、退出应用）

视频循环播放功能

3. 技术实现

使用现代 .NET 8.0 项目格式

集成 VLC.NET 和 LibVLC 实现真正的视频播放

Windows API 调用实现壁纸层级设置

注重代码质量并采用模块化架构设计

解决的问题

3. 解决的问题

3.1. VLC.NET 视频播放功能

添加了 LibVLCSharp 和 LibVLCSharp.WinForms NuGet 包引用

实现了 VLC 初始化代码

使用 VideoView 控件替换原有的 PictureBox 模拟实现

实现了视频循环播放功能

3.2. 视频壁纸层级问题

改进了 Windows API 调用，正确将视频窗体设置为桌面背景层级

确保视频壁纸不会遮挡任务栏和桌面图标

优化了窗体属性设置，确保视频窗体正确显示在桌面背景位置

通过将视频窗体设置为SHELLDLL_DefView的子窗体，确保视频正确显示在桌面图标之下

3.3. 桌面快捷方式问题

创建了 PowerShell 脚本用于生成桌面快捷方式

提供了详细的使用说明

项目文件结构

MovieBackground/

├── MovieBackground.sln

├── MovieBackground/

│   ├── Form1.cs

│   ├── Form1.Designer.cs

│   ├── Program.cs

│   ├── MovieBackground.csproj

│   └── app.manifest

├── CreateShortcut.ps1

├── README.md

└── USAGE.md

构建和运行

系统要求

Windows 10 或更高版本

.NET 8.0 SDK

构建步骤

克隆或下载项目代码

在项目根目录下运行以下命令：

dotnet build

运行步骤

构建项目后，运行以下命令：

dotnet run

（可选）创建桌面快捷方式：

powershell -ExecutionPolicy Bypass -File CreateShortcut.ps1

使用方法

应用启动后会在系统托盘显示图标

右键点击托盘图标选择"选择视频文件"来设置视频壁纸

选择视频文件后，视频将作为桌面背景播放

可以通过右键菜单选择"退出"来关闭应用程序

扩展建议

添加音量控制功能

支持多显示器设置

添加视频播放控制（暂停/继续、快进等）

实现启动时自动运行选项

添加视频预览功能

故障排除

如果应用程序无法启动，请确保已安装 .NET 8.0 SDK

如果视频无法播放，请检查视频文件格式是否受支持

如果快捷方式无法创建，请确保 PowerShell 执行策略允许脚本运行

版权信息

本项目仅供学习和参考使用。

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTRiaNgIhMcIs2vXTUSkj8rbhTAv8M6WHrJtybUCCtQ7BjFupvtdBIswiaESqcicmxUdxuXHuOiaelL1sw/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)
