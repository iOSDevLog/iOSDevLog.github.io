---
layout: post
title: "Day 4: 移动端低功耗蓝牙通信（中）：Android"
author: iosdevlog
date: 2025-09-04 01:25:38 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247485664&idx=1&sn=59e50945b9ba82483a56cbb195237b55&chksm=f95c9367ce2b1a71c0dece2c4ae4e8e9bf70f4aed1de753670a32648699481334810da642341#rd

BLE Chat Android

一个基于蓝牙低功耗(BLE)技术的 Android 聊天应用，可实现附近设备间的通信。

📱 概述

BLE_Chat 是一款 Androi 应用程序，允许用户发现附近的 BLE 设备并与之交换消息。该应用采用 Jetpack Compose 构建的现代化 UI，并实现了BLE通信协议以实现实时消息传递。

📸 Screenshots

🚀 功能特性

BLE设备发现

: 扫描并发现附近的BLE设备

实时消息传递

: 与连接的设备发送和接收消息

现代化UI

: 使用 Jetpack Compose 构建流畅的用户体验

权限管理

: 正确管理BLE和媒体访问的Android权限

多平台支持

: 兼容 Android 7.0 (API级别24)及以上版本

🛠️ 技术详情

架构

MVVM模式

: 使用 ViewModel 和 LiveData 进行状态管理

Jetpack Compose

: 用于构建原生 Android 界面的现代化UI工具包

导航组件

: 使用 Compose Navigation 处理屏幕导航

BLE实现

: 自定义 BLE 协议实现消息交换

核心组件

MainActivity

: 应用程序入口点

ChatViewModel

: 管理聊天状态和 BLE 操作

DeviceListScreen

: 显示可连接的 BLE 设备

ChatScreen

: 处理消息显示和输入

BLEProtocol

: 实现BLE通信协议

BluetoothUtils

: BLE操作的辅助函数

📋 系统要求

Android 7.0 (API级别24)或更高版本

蓝牙低功耗(BLE)支持

摄像头(用于可选的媒体功能)

🔧 权限说明

应用需要以下权限:

BLUETOOTH

及相关权限用于设备通信

ACCESS_FINE_LOCATION

用于 BLE 扫描

CAMERA

用于媒体功能

存储权限用于媒体处理

📦 依赖项

主要依赖包括:

Jetpack Compose UI 工具包

Android Lifecycle 组件

Navigation Compose

CameraX 用于相机功能

Gson 用于 JSON 序列化

🚀 快速开始

前提条件

Android Studio Flamingo 或更高版本

支持 BLE 的 Android 设备(或支持 BLE 的模拟器)

安装步骤

克隆仓库:

git clone https://github.com/buld-your-own-x-with-ai/BLE_Chat_Android.git

在 Android Studio 中打开项目

构建并运行应用程序

构建项目

在 Android Studio 中打开项目

选择"Build" > "Make Project" 或按 Ctrl+F9(Windows/Linux)或Cmd+F9(Mac)

APK 文件将生成在 app/build/outputs/apk/ 目录中

📱 使用说明

在 Android 设备上启动应用

在提示时授予必要的权限

如果尚未启用蓝牙，请启用蓝牙

使用扫描按钮扫描附近的设备

选择要连接的设备

开始与连接的设备聊天

📁 项目结构

app/

├── src/

│   ├── main/

│   │   ├── java/com/haotek/ble_chat/

│   │   │   ├── ble/          # BLE实现

│   │   │   ├── models/       # 数据模型

│   │   │   ├── protocol/     # 通信协议

│   │   │   ├── ui/           # UI 组件

│   │   │   ├── utils/        # 工具类

│   │   │   └── MainActivity.kt

│   │   └── res/              # 资源文件

│   └── build.gradle.kts

└── build.gradle.kts

🤝 贡献指南

欢迎贡献！请随时提交 Pull Request。

Fork 仓库

创建功能分支 (git checkout -b feature/AmazingFeature)

提交更改 (git commit -m 'Add some AmazingFeature')

推送到分支 (git push origin feature/AmazingFeature)

打开 Pull Request

📄 许可证

本项目采用 MIT 许可证 - 详情请见LICENSE文件。

🙏 致谢

使用 Android Jetpack Compose构建

使用 Android BLE APIs

受各种 BLE 通信项目的启发

📞 技术支持

如需支持，请在 GitHub 仓库中提交 issue。

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_jpg/kIE7WtwNFTT2owAbN7famQMcK0Sh2CPxjUBPov8W17bVd0YFlICTAiaWcOsXOzbEEoR7iaUCQfPiaYq3eZAriaSLEg/640?wx_fmt=jpeg&from=appmsg&watermark=1#imgIndex=0)
