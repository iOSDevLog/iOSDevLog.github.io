---
layout: post
title: "Day 44: AI 打造 http tools"
author: iosdevlog
date: 2025-10-25 23:59:17 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486028&idx=1&sn=36c3c5f62223f641d7ad9f336ff4d150&chksm=f95c91cbce2b18dd599fbc3b484321e0baae6b1cab70dd874d7b559b96bc2bf1613b70be4123#rd

Electron API 测试工具

一个基于 Electron 的 API 测试工具，类似于 Postman，使用 React 和 TypeScript 构建。

English | 简体中文

功能特性

🚀 HTTP 请求测试（GET、POST、PUT、DELETE、PATCH）

🌍 环境管理与变量替换

📁 请求集合与组织管理

📜 请求历史记录追踪

🎨 响应格式化与语法高亮

💾 数据持久化存储

⌨️ 键盘快捷键支持

🔒 安全的 IPC 通信

开发环境设置

前置要求

Node.js（v16 或更高版本）

npm 或 yarn

安装

克隆仓库

git clone https://github.com/build-your-own-x-with-ai/http_tools.git

cd http_tools

安装依赖：

npm install

开发

启动开发环境：

npm run dev

这将同时启动 Electron 主进程和 React 渲染进程的开发模式。

构建

构建生产版本：

npm run build

打包

创建可分发的安装包：

npm run package

支持的平台：

macOS（.dmg）

Windows（.exe）

Linux（.AppImage、.deb）

测试

运行测试：

npm test

运行测试并生成覆盖率报告：

npm run test:coverage

项目结构

src/

├── main/                      # Electron 主进程

│   ├── main.ts               # 主进程入口点

│   ├── preload.ts            # IPC 预加载脚本

│   └── services/             # 后端服务

│       ├── APIService.ts     # HTTP 请求服务

│       ├── DataManager.ts    # 数据持久化管理

│       ├── EnvironmentProcessor.ts  # 环境变量处理

│       ├── HistoryManager.ts # 历史记录管理

│       └── SecurityService.ts # 安全服务

├── renderer/                  # React 渲染进程

│   ├── index.tsx             # 渲染进程入口点

│   ├── App.tsx               # 主应用组件

│   ├── components/           # React 组件

│   │   ├── RequestBuilder.tsx      # 请求构建器

│   │   ├── ResponseViewer.tsx      # 响应查看器

│   │   ├── EnvironmentSelector.tsx # 环境选择器

│   │   ├── CollectionSidebar.tsx   # 集合侧边栏

│   │   ├── HistoryPanel.tsx        # 历史面板

│   │   └── Toast.tsx               # 通知组件

│   ├── contexts/             # React 上下文

│   │   └── AppContext.tsx    # 应用状态管理

│   ├── hooks/                # 自定义 Hooks

│   │   └── useCollections.ts # 集合管理 Hook

│   └── index.css             # 全局样式

├── types/                     # TypeScript 类型定义

│   └── index.ts              # 共享类型

└── test/                      # 测试配置

├── setup.ts              # Jest 设置

└── setup-renderer.ts     # 渲染进程测试设置

使用指南

发送请求

在 URL 输入框中输入 API 端点

选择 HTTP 方法（GET、POST 等）

添加请求头（可选）

添加请求体（对于 POST/PUT 请求）

点击"发送"按钮或按 Ctrl/Cmd + Enter

环境管理

点击环境选择器下拉菜单

点击"+ 新建"创建新环境

定义变量（例如：baseUrl, apiKey）

在请求中使用变量：{{baseUrl}}/users

保存请求

配置您的请求

点击"保存"按钮或按 Ctrl/Cmd + S

请求将被保存到当前集合

查看历史

点击侧边栏的"历史"标签

浏览之前的请求

点击任意历史项重新加载请求

使用过滤器按方法、状态或 URL 搜索

键盘快捷键

请求操作

Ctrl/Cmd + Enter

- 发送请求

Ctrl/Cmd + S

- 保存请求

Ctrl/Cmd + N

- 新建请求

Ctrl/Cmd + K

- 清除响应

导航

Ctrl/Cmd + 1

- 显示集合

Ctrl/Cmd + 2

- 显示历史

Ctrl/Cmd + B

- 切换侧边栏

通用

Ctrl/Cmd + R

- 重新加载

F12

- 切换开发者工具

技术栈

Electron

- 跨平台桌面应用框架

React

- UI 组件库

TypeScript

- 类型安全的 JavaScript

Webpack

- 模块打包工具

Jest

- 测试框架

React Testing Library

- React 组件测试

架构

该应用遵循 Electron 的多进程架构：

主进程

：处理系统级操作、文件 I/O 和 HTTP 请求

渲染进程

：运行 React UI 和用户交互

预加载脚本

：在主进程和渲染进程之间提供安全的 IPC 桥接

安全性

启用上下文隔离

禁用 Node.js 集成

通过 contextBridge 进行安全的 IPC 通信

输入验证和清理

安全的数据存储

贡献

欢迎贡献！请随时提交 Pull Request。

许可证

MIT

致谢

本项目受 Postman 和其他 API 测试工具的启发。

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTSkjtG2uuBWcqmBlcohPOg8EqacdV7xc17vicA2aLoj1d1yn0Y8SnyTDSkoia2giaL2m48qXc6QFFpFA/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)

![image-2](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTSkjtG2uuBWcqmBlcohPOg8juRLwUydCgC0uDQQuV00ZwM5oHNdEjnkshdjFOJTJpL2LS4bgZ6OsQ/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=1)
