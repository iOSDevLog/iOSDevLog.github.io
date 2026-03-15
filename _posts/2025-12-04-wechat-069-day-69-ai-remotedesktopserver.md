---
layout: post
title: "Day 69: AI 打造远程桌面服务端 RemoteDesktopServer"
author: iosdevlog
date: 2025-12-04 22:46:36 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486300&idx=1&sn=5721c2e8a20b67d9db9b7a72e31bf197&chksm=f95c90dbce2b19cd77d6dabde72f835027408934500f2a18a16127576675896cfaab19d8846b#rd

Features

Real-time Screen Streaming

: Capture and stream desktop at up to 60 FPS

Remote Input Control

: Support for mouse, keyboard, and scroll events

Adaptive Quality

: Automatically adjusts video quality and frame rate based on network conditions

Secure Authentication

: User authentication with bcrypt password hashing

TLS/SSL Support

: Optional encrypted connections for secure remote access

Multi-client Support

: Handle multiple concurrent client connections

Configurable Settings

: Flexible configuration via JSON file

Requirements

Python 3.8+

Operating System: Windows, macOS, or Linux

Dependencies listed in requirements.txt

Installation

Clone the repository:

git clone https://github.com/build-your-own-x-with-ai/RemoteDesktopServe

cd RemoteDesktopServer

Install dependencies:

pip install -r requirements.txt

Configure the server by editing config.json:

{

"server":{

"host":"0.0.0.0",

"port":8765,

"max_clients":5

},

"screen":{

"fps":30,

"quality":80,

"width":1920,

"height":1080

}

}

Usage

Create a user account

:

python create_user.py

Start the server

:

python src/server/main.py

Or use the provided script:

./run_server.sh

Enable TLS (Optional)

:

./generate_cert.sh

Then set "use_tls": true in config.json.

Configuration

Edit config.json to customize:

Server Settings

: Host, port, max clients

Screen Settings

: FPS, quality, resolution

Security

: TLS, authentication attempts, block duration

Performance

: Adaptive quality, FPS range, buffer size

Testing

Run the test suite:

./run_tests.sh

Or manually:

pytest tests/

Project Structure

RemoteDesktopServer/

├── src/

│   ├── server/          # Server components

│   │   ├── main.py      # Main server application

│   │   ├── auth.py      # Authentication manager

│   │   ├── screen_capturer.py

│   │   ├── video_encoder.py

│   │   ├── input_simulator.py

│   │   └── adaptive_quality.py

│   └── common/          # Shared models

├── tests/               # Test suite

├── config.json          # Configuration file

└── requirements.txt     # Python dependencies

License

See LICENSE file for details.

中文

基于 Python 和 WebSocket 构建的高性能远程桌面服务器，支持实时屏幕共享、远程控制和自适应质量流传输。

功能特性

实时屏幕流传输

：以最高 60 FPS 捕获和传输桌面画面

远程输入控制

：支持鼠标、键盘和滚轮事件

自适应质量

：根据网络状况自动调整视频质量和帧率

安全认证

：使用 bcrypt 密码哈希的用户认证系统

TLS/SSL 支持

：可选的加密连接，确保远程访问安全

多客户端支持

：处理多个并发客户端连接

可配置设置

：通过 JSON 文件灵活配置

系统要求

Python 3.8+

操作系统：Windows、macOS 或 Linux

依赖项列在 requirements.txt 中

安装步骤

克隆仓库：

git clone https://github.com/build-your-own-x-with-ai/RemoteDesktopServe

cd RemoteDesktopServer

安装依赖：

pip install -r requirements.txt

编辑 config.json 配置服务器：

{

"server":{

"host":"0.0.0.0",

"port":8765,

"max_clients":5

},

"screen":{

"fps":30,

"quality":80,

"width":1920,

"height":1080

}

}

使用方法

创建用户账户

：

python create_user.py

启动服务器

：

python src/server/main.py

或使用提供的脚本：

./run_server.sh

启用 TLS（可选）

：

./generate_cert.sh

然后在 config.json 中设置 "use_tls": true。

配置说明

编辑 config.json 自定义：

服务器设置

：主机、端口、最大客户端数

屏幕设置

：帧率、质量、分辨率

安全设置

：TLS、认证尝试次数、封禁时长

性能设置

：自适应质量、帧率范围、缓冲区大小

测试

运行测试套件：

./run_tests.sh

或手动运行：

pytest tests/

项目结构

RemoteDesktopServer/

├── src/

│   ├── server/          # 服务器组件

│   │   ├── main.py      # 主服务器应用

│   │   ├── auth.py      # 认证管理器

│   │   ├── screen_capturer.py

│   │   ├── video_encoder.py

│   │   ├── input_simulator.py

│   │   └── adaptive_quality.py

│   └── common/          # 共享模型

├── tests/               # 测试套件

├── config.json          # 配置文件

└── requirements.txt     # Python 依赖

许可证

详见 LICENSE 文件。

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTTgZQZPkpEc7icVVX9sFeHvWBXd8uvRwkEzOSVpv9jaZvjS7hTqXadWEBNWRhyRl4svrLialDJGehBQ/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)
