---
layout: post
title: "Day 78: Spec-Kit rust 做微信朋友圈，附带提示词"
author: iosdevlog
date: 2026-01-07 23:52:39 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486391&idx=1&sn=71191a3d292014d6ccddfc3056097dd2&chksm=f95c9030ce2b1926d2b22acb7a0c27fc66ea420c4ce63dd8c04ecb54497a62747d0f76424378#rd

Moments Tauri

Local-only desktop Moments timeline app (Tauri + Rust + vanilla JS).

中文说明

本项目是一个本地优先的桌面「朋友圈」应用（Tauri + Rust + 原生 JS）。

功能概览

发布纯文字或多图动态

时间流按最新优先展示与懒加载

动态点赞与评论

数据仅存本地（SQLite + 本地文件系统）

开发运行

环境依赖

Rust toolchain（稳定版）

cargo-tauri CLI：cargo install cargo-tauri

Node.js（仅用于可选前端测试）

启动

cd src-tauri

cargo tauri dev

测试

Rust 测试：

cd src-tauri

cargo test

前端逻辑测试：

cd frontend-tests

node publish_flow.test.js

node timeline_scroll.test.js

node likes_comments.test.js

Overview

Publish text or multi-image moments

Timeline with newest-first ordering and lazy loading

Likes and comments per moment

All data stored locally (SQLite + local filesystem)

Development

Prerequisites

Rust toolchain (stable)

cargo-tauri CLI (cargo install cargo-tauri)

Node.js (only needed for optional JS tests)

Run

cd src-tauri

cargo tauri dev

Tests

Rust tests:

cd src-tauri

cargo test

Frontend logic tests:

cd frontend-tests

node publish_flow.test.js

node timeline_scroll.test.js

node likes_comments.test.js

Project Structure

src/                     # Frontend (HTML/CSS/JS)

├── pages/

├── components/

├── styles/

├── assets/

└── services/

src-tauri/               # Rust backend

├── src/

│   ├── commands/

│   ├── db/

│   ├── models/

│   ├── services/

│   └── errors.rs

└── tests/

Spec Kit

https://github.com/github/spec-kit

npm i -g @openai/codex

codex --version

codex-cli 0.79.0

curl -LsSf https://astral.sh/uv/install.sh | sh

source ~/.zshrc

uv tool install specify-cli --from git+https://github.com/github/spec-kit.git

i@MacBook-Pro-M4 Build_Your_Onw_X_With_AI % specify init moments-tauri

███████╗██████╗ ███████╗ ██████╗██╗███████╗██╗   ██╗

██╔════╝██╔══██╗██╔════╝██╔════╝██║██╔════╝╚██╗ ██╔╝

███████╗██████╔╝█████╗  ██║     ██║█████╗   ╚████╔╝

╚════██║██╔═══╝ ██╔══╝  ██║     ██║██╔══╝    ╚██╔╝

███████║██║     ███████╗╚██████╗██║██║        ██║

╚══════╝╚═╝     ╚══════╝ ╚═════╝╚═╝╚═╝        ╚═╝

GitHub Spec Kit - Spec-Driven Development Toolkit

╭──────────────────────────────────────────────────────────────────────────────╮

│                                                                              │

│  Specify Project Setup                                                       │

│                                                                              │

│  Project         moments-tauri                                               │

│  Working Path    /Users/i/Code/Build_Your_Onw_X_With_AI                      │

│  Target Path     /Users/i/Code/Build_Your_Onw_X_With_AI/moments-tauri        │

│                                                                              │

╰──────────────────────────────────────────────────────────────────────────────╯

Selected AI assistant: codex

Selected script type: sh

Initialize Specify Project

├── ● Check required tools (ok)

├── ● Select AI assistant (codex)

├── ● Select script type (sh)

├── ● Fetch latest release (release v0.0.90 (56,703 bytes))

├── ● Download template (spec-kit-template-codex-sh-v0.0.90.zip)

├── ● Extract template

├── ● Archive contents (27 entries)

├── ● Extraction summary (2 top-level items)

├── ● Ensure scripts executable (5 updated)

├── ● Cleanup

├── ● Initialize git repository (initialized)

└── ● Finalize (project ready)

Project ready.

╭─────────────────────────── Agent Folder Security ────────────────────────────╮

│                                                                              │

│  Some agents may store credentials, auth tokens, or other identifying and    │

│  private artifacts in the agent folder within your project.                  │

│  Consider adding .codex/ (or parts of it) to .gitignore to prevent           │

│  accidental credential leakage.                                              │

│                                                                              │

╰──────────────────────────────────────────────────────────────────────────────╯

╭───────────────────────────────── Next Steps ─────────────────────────────────╮

│                                                                              │

│  1. Go to the project folder: cd moments-tauri                               │

│  2. Set CODEX_HOME environment variable before running Codex: export         │

│  CODEX_HOME=/Users/i/Code/Build_Your_Onw_X_With_AI/moments-tauri/.codex      │

│  3. Start using slash commands with your AI agent:                           │

│     2.1 /speckit.constitution - Establish project principles                 │

│     2.2 /speckit.specify - Create baseline specification                     │

│     2.3 /speckit.plan - Create implementation plan                           │

│     2.4 /speckit.tasks - Generate actionable tasks                           │

│     2.5 /speckit.implement - Execute implementation                          │

│                                                                              │

╰──────────────────────────────────────────────────────────────────────────────╯

╭──────────────────────────── Enhancement Commands ────────────────────────────╮

│                                                                              │

│  Optional commands that you can use for your specs (improve quality &        │

│  confidence)                                                                 │

│                                                                              │

│  ○ /speckit.clarify (optional) - Ask structured questions to de-risk         │

│  ambiguous areas before planning (run before /speckit.plan if used)          │

│  ○ /speckit.analyze (optional) - Cross-artifact consistency & alignment      │

│  report (after /speckit.tasks, before /speckit.implement)                    │

│  ○ /speckit.checklist (optional) - Generate quality checklists to validate   │

│  requirements completeness, clarity, and consistency (after /speckit.plan)   │

│                                                                              │

╰──────────────────────────────────────────────────────────────────────────────╯

cd moments-tauri

codex login

codex login status

Logged in using ChatGPT

/prompts:speckit.constitution 创建本项目的开发原则与治理规范，重点包括：

1. 代码质量

- Rust 代码需遵循清晰的模块边界

- 禁止过度抽象，优先可读性

- 前端逻辑与后端逻辑职责明确

2. 稳定性与安全性

- 所有本地数据只存储在用户设备

- 不进行任何网络上传或外部同步

- 后端接口需具备明确的错误处理策略

3. 用户体验一致性

- 时间流（朋友圈）按时间倒序展示

- 滚动、加载、交互行为保持一致

- 操作应有即时反馈（点赞、评论、发布）

4. 性能要求

- 时间流加载需支持分页或懒加载

- UI 操作不应阻塞主线程

- Rust 后端避免不必要的拷贝和锁竞争

5. 可测试性

- 核心数据逻辑应可单元测试

- UI 行为应可通过逻辑拆分进行验证

/prompts:speckit.specify 构建一个类似「微信朋友圈」的桌面应用，用于个人内容记录和回顾。

## 产品目标

用户可以像使用朋友圈一样：

- 发布图文内容

- 按时间流浏览历史动态

- 对内容进行点赞和评论

- 所有数据仅保存在本地

## 核心概念

- 动态（Moment）：一条图文或纯文本内容

- 时间流（Timeline）：按时间倒序排列的动态列表

- 互动行为：点赞、评论

## 功能需求

1. 发布动态

- 支持纯文字

- 支持多张图片

- 发布后立即出现在时间流顶部

2. 浏览时间流

- 按时间倒序展示

- 支持滚动加载

- 单条动态可展开查看详情

3. 点赞与评论

- 每条动态支持点赞 / 取消点赞

- 支持多条评论

- 评论按时间正序排列

4. 本地数据管理

- 所有数据仅存储在本地

- 重启应用后数据仍然存在

- 不支持账号、多用户或云同步

## 非目标（明确不做）

- 不做社交网络

- 不做好友系统

- 不做网络同步

- 不支持嵌套转发或分享

## 使用场景

- 用户记录生活瞬间

- 用户按时间回顾过去的内容

- 作为私密日记或生活日志工具

/prompts:speckit.plan 本项目采用 Rust + Tauri 的桌面应用架构，整体方案如下：

## 技术栈

- 桌面框架：Tauri

- 后端语言：Rust

- 前端技术：HTML + CSS + 原生 JavaScript（尽量少依赖库）

- 数据存储：本地 SQLite 数据库

- 图片存储：本地文件系统

## 架构设计

1. Rust 后端

- 负责数据模型、数据库读写

- 提供 Tauri Command 接口供前端调用

- 管理动态、点赞、评论的生命周期

2. 前端 UI

- 时间流页面（主页面）

- 发布动态页面

- 动态详情页面

- 使用组件化思维但不引入重型框架

3. 数据模型

- Moment（动态）

- Comment（评论）

- Like（点赞状态）

## 数据流

- 前端触发操作 → 调用 Tauri Command

- Rust 处理逻辑 → 读写 SQLite

- 返回结果 → 前端更新 UI

## 约束

- 不使用前端大型框架（如 React / Vue）

- 不引入不必要的第三方 Rust crate

- 所有状态以数据库为准

/prompts:speckit.tasks

/prompts:speckit.implement

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTTXF4IQ3Kn8dWcMNm4KzLhj7QA7icIfycRgF2iaKlmkHNTxkSlIsfGL08KfvD1WVu8CuaRrcBYMib6DQ/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)

![image-2](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTTXF4IQ3Kn8dWcMNm4KzLhjuQJ8k1Es2EXveIqDrWGjoDvEDfyq1UjhtG0qHuEQI8q7YDmniaE0gvw/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=1)

![image-3](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTTXF4IQ3Kn8dWcMNm4KzLhjPVBpN5qJ3Y1l5j4JlqgNKiaxkrl9a3D09WZmMGfX0noG0eVicMgzfyCw/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=2)
