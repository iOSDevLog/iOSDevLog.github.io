---
layout: post
title: "Day 94: UVC Camera SDL Display with FFmpeg Encoding"
author: iosdevlog
date: 2026-03-10 23:55:07 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486711&idx=1&sn=6b07d71a16e72e6e06ab74f223aa137c&chksm=f95c9770ce2b1e6613c829d23cc96a57228b78757be5c0b9bfdda58c2589b91b70c0b5277726#rd

UVC Camera SDL Display with FFmpeg Encoding

一个基于 libuvc、SDL2 和 FFmpeg 的摄像头实时显示与编码工具，支持将摄像头画面实时显示在 SDL 窗口并编码为 MP4 视频文件。

功能特性

实时显示 UVC 摄像头画面（SDL2 窗口）

将摄像头画面编码为 H.264 格式的 MP4 视频

支持多线程安全的帧采集与渲染

优雅的退出机制（ESC/Q/Ctrl+C）

详细的日志输出，便于问题排查

Screenshots

环境依赖

系统要求

Ubuntu 20.04/22.04/24.04（其他 Linux 发行版可适配）

已安装 UVC 兼容摄像头

依赖库安装

# 基础编译工具

sudo apt update

sudo apt install -y build-essential git

# libuvc 依赖

sudo apt install -y libusb-1.0-0-dev libuvc-dev

# SDL2 依赖

sudo apt install -y libsdl2-dev

# FFmpeg 依赖

sudo apt install -y libavformat-dev libavcodec-dev libavutil-dev libswscale-dev

# 线程库

sudo apt install -y libpthread-stubs0-dev

编译运行

编译

# 克隆/下载代码后，进入目录

make clean  # 清理旧编译文件

make        # 编译生成可执行文件

运行

# 必须使用 sudo 运行（摄像头访问权限）

sudo ./uvc_sdl_example

退出方式

按下 ESC 或 Q 键退出

按下 Ctrl+C 退出

点击 SDL 窗口关闭按钮退出

配置说明

摄像头参数

修改代码中 main 函数的以下参数，匹配你的摄像头实际支持的参数：

ctx.width = 640;    // 摄像头宽度

ctx.height = 480;   // 摄像头高度

ctx.fps = 30;       // 摄像头帧率

查看摄像头支持的参数

v4l2-ctl --list-formats-ext -d /dev/video0

输出文件

编码后的视频文件默认保存为：uvc_capture_working.mp4

常见问题解决

1. SDL 窗口黑屏

确认摄像头参数配置正确

确认使用 sudo 运行（摄像头权限）

确认 SDL 渲染在主线程执行（本代码已修复此问题）

2. 编译错误

检查所有依赖库是否安装完整

确认 Makefile 中的编译参数正确

检查结构体访问符：栈上实例用 .，指针用 ->

3. 摄像头无法识别

检查摄像头是否为 UVC 兼容设备

运行 lsusb 确认摄像头已被系统识别

运行 v4l2-ctl --list-devices 确认摄像头设备节点

代码结构说明

函数

功能

ffmpeg_init

初始化 FFmpeg 编码器，配置编码参数

sdl_init

初始化 SDL2 窗口、渲染器、帧缓存

uvc_frame_callback

UVC 回调函数，采集帧数据并转换为 BGR 格式

sdl_render_frame

主线程 SDL 渲染函数，显示缓存中的帧数据

uvc_init_and_start

初始化 UVC 上下文并启动视频流

sdl_event_loop

处理 SDL 窗口事件（按键、关闭等）

cleanup

资源清理函数，释放所有申请的内存和句柄

使用说明

文件结构 将以下文件放在同一目录：

uvc_sdl_example.c

（最终修复版代码）

README.md

（本文档）

Makefile

（编译脚本）

Makefile 命令说明

命令

功能

make

编译代码生成可执行文件

make clean

清理可执行文件和生成的 MP4 视频

make run

编译并直接运行程序（等效于 make && sudo ./uvc_sdl_example）

注意事项

Makefile 中的编译参数已包含所有必要的库链接，无需手动修改

确保 uvc_sdl_example.c 文件名与 Makefile 中的 SRC 变量一致

运行 make run 时会自动使用 sudo 权限，避免摄像头访问权限问题

许可证

本项目为开源学习用途，可自由修改和使用。

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/rgPAIfdrfVzcsk9eVeUib0TAHicT8A1oJnOp2asNiaaMTewDO2fiaI0p1JsArmGmNllFl6mlltoqicY0c0xztXmw8P2BxwqgUYqiaGLvJIgDXwmH0/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)
