---
layout: post
title: "Day 70: AI 打造远程桌面 iOS 客户端 RemoteDesktop_iOS"
author: iosdevlog
date: 2025-12-05 00:00:00 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486310&idx=1&sn=2c1d5c735e1f6e23fed3a322aee90e45&chksm=f95c90e1ce2b19f7688466d9dd429d07a333fbab6e60d692613b5c2fcc6142f8dba3e6d529c3#rd

RemoteDesktop_iOS

English | 中文

RemoteDesktop iOS Client: https://github.com/build-your-own-x-with-ai/RemoteDesktop_iOS

RemoteDesktop Server: https://github.com/build-your-own-x-with-ai/RemoteDesktopServer

English

Overview

RemoteDesktop_iOS is a remote desktop client application for iOS devices, enabling users to remotely access and control desktop computers from their iPhone or iPad.

Screenshots

，时长

00:26

Features

Real-time Remote Control

: Connect to remote desktops via WebSocket

Video Streaming

: Hardware-accelerated video decoding for smooth display

Input Support

: Touch-based mouse and keyboard input translation

Secure Connection

: Credential management and secure authentication

Display Settings

: Customizable display configurations

Architecture

The project follows MVVM architecture with the following components:

Models

: Data structures for connection state, credentials, display settings, input events, and messages

Services

:

WebSocketClient

: Handles real-time communication

VideoDecoder

: Decodes and renders video streams

InputTranslator

: Translates touch inputs to desktop commands

ViewModels

: Business logic and state management

Views

: SwiftUI-based user interface

Requirements

iOS 14.0+

Xcode 13.0+

Swift 5.5+

Installation

Clone the repository

git clone https://github.com/build-your-own-x-with-ai/RemoteDesktop_iOS.git

Open RemoteDesktop.xcodeproj in Xcode

Build and run the project on your iOS device or simulator

Usage

Launch the app

Enter your remote desktop credentials

Configure connection settings

Connect and control your remote desktop

License

See LICENSE file for details.

中文

概述

RemoteDesktop_iOS 是一款适用于 iOS 设备的远程桌面客户端应用程序，使用户能够从 iPhone 或 iPad 远程访问和控制桌面计算机。

功能特性

实时远程控制

：通过 WebSocket 连接到远程桌面

视频流传输

：硬件加速视频解码，实现流畅显示

输入支持

：基于触摸的鼠标和键盘输入转换

安全连接

：凭据管理和安全身份验证

显示设置

：可自定义的显示配置

架构

项目采用 MVVM 架构，包含以下组件：

Models（模型）

：连接状态、凭据、显示设置、输入事件和消息的数据结构

Services（服务）

：

WebSocketClient

：处理实时通信

VideoDecoder

：解码和渲染视频流

InputTranslator

：将触摸输入转换为桌面命令

ViewModels（视图模型）

：业务逻辑和状态管理

Views（视图）

：基于 SwiftUI 的用户界面

系统要求

iOS 14.0+

Xcode 13.0+

Swift 5.5+

安装

克隆仓库

git clone https://github.com/build-your-own-x-with-ai/RemoteDesktop_iOS.git

在 Xcode 中打开 RemoteDesktop.xcodeproj

在 iOS 设备或模拟器上构建并运行项目

使用方法

启动应用

输入远程桌面凭据

配置连接设置

连接并控制您的远程桌面

许可证

详见 LICENSE 文件。

![image-1](https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486310&idx=1&sn=2c1d5c735e1f6e23fed3a322aee90e45&chksm=f95c90e1ce2b19f7688466d9dd429d07a333fbab6e60d692613b5c2fcc6142f8dba3e6d529c3)

![image-2](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTTgZQZPkpEc7icVVX9sFeHvWIwGhCEz5BjXwtr1ndiaEKs8Y6XEdw9NSKibKJqA4oAGXVasXxVj6oRQw/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)

![image-3](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTTgZQZPkpEc7icVVX9sFeHvWosXkoeYib1L7ibCqW8tjcQ5seuiaYpaj9CA177T6rufQDkvON5asuIicyA/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=1)
