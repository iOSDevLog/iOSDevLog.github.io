---
layout: post
title: "Day 64: Simple 1Panel (macOS) 简版"
author: iosdevlog
date: 2025-11-17 23:54:31 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486216&idx=1&sn=5e9310a415810a949e5508938591dd56&chksm=f95c908fce2b19997052b25e425dff2fb32324869af4398d893517086a9fd3c5ff4a8226623b#rd

Simple 1Panel (macOS) 简版

一个在 macOS 本地运行的轻量面板，参考 1Panel 思路，提供基础的系统监控、文件与进程管理。前后端分离，Electron 打包为桌面应用。

截图

功能

仪表盘：CPU、内存、磁盘挂载点等摘要信息

文件管理：列目录、下载文件、创建/删除文件或目录

进程管理：按名称筛选、结束进程

设置：修改后端 API 地址（默认 http://127.0.0.1:48080）

快速开始

git clone https://github.com/build-your-own-x-with-ai/Simple1Panel

构建后端：

bash scripts/build_backend.sh

启动后端（默认 48080）：

./backend/build/paneld --port 48080

安装并启动 Electron（使用 cnpm）：

cd electron && cnpm install

node_modules/.bin/electron .

直接打开前端（开发调试）：

frontend/index.html

主要 API

GET /api/system/summary

GET /api/files/list?path=...

GET /api/files/download?path=...

GET /api/files/mkdir?path=...

GET /api/files/touch?path=...

GET /api/files/delete?path=...

GET /api/process/list?limit=...&q=...

GET /api/process/kill?pid=...

目录结构

backend/

C++17 最小后端（CMake），提供上述 API

frontend/

轻量 HTML/CSS/JS 页面，仿 1Panel 风格布局

electron/

Electron 主进程，拉起后端并加载前端

scripts/

构建脚本

注意

为本地单机简化版本，无用户与权限体系；操作需谨慎（尤其结束进程、删除文件）。

某些文件操作可能需要管理员权限；如失败会返回错误码。

后续可升级到 React + Arco Design，并接入 httplib、Loguru、RapidJSON 等以增强可维护性。

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTT2funNmNz6u8D2lEAwPwHTwTiaxQPuS5qrRR0pKbzTTnLnBLqp4qMHEHLwcu8p05JzRoJXiacpDFfQ/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)

![image-2](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTT2funNmNz6u8D2lEAwPwHT6icrvrnWuG63TWPfbU02HsKV0gJ7TnMKia7RkhhTic25egXJblXPhQiaXw/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=1)
