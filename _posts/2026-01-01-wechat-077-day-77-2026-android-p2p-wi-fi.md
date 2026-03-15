---
layout: post
title: "Day 77: 2026 元旦快乐 Android P2P Wi-Fi 直连"
author: iosdevlog
date: 2026-01-01 00:16:03 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486363&idx=1&sn=754aa2b71c61569b176af8f27a406af8&chksm=f95c901cce2b190ad921381b0741e4f332bd44bc08a0d26ce782eba9736eb1ab78c9ab2164b3#rd

WiFi Direct Chat

WiFi Direct聊天应用

A simple WiFi Direct chat application that allows devices to connect directly and exchange messages. 一个简单的WiFi Direct聊天应用，允许设备直接连接并交换消息。

Features

功能特性

WiFi Direct Device Discovery

: Discover nearby WiFi Direct devices

WiFi Direct设备发现

: 发现附近的WiFi Direct设备

Auto Connection

: Automatically connect to chat server when WiFi Direct connection is established

自动连接

: 当WiFi Direct连接建立时自动连接到聊天服务器

Real-time Messaging

: Send and receive messages in real-time

实时消息

: 实时发送和接收消息

IP Address Display

: Shows the device's WiFi Direct IP address

IP地址显示

: 显示设备的WiFi Direct IP地址

Connection Status

: Real-time connection status updates

连接状态

: 实时连接状态更新

Requirements

系统要求

Android 7.0 (API level 24) or higher

Android 7.0（API级别24）或更高版本

WiFi Direct supported device

支持WiFi Direct的设备

Chat server running on 192.168.49.1:8080

聊天服务器运行在192.168.49.1:8080

Installation

安装说明

Clone or download the project

克隆或下载项目

Open the project in Android Studio

在Android Studio中打开项目

Build and run the project on your Android device

在Android设备上构建并运行项目

Usage

使用方法

Enable WiFi on your device

在设备上启用WiFi

Launch the application

启动应用程序

Grant the required permissions

授予所需权限

Click "Discover Devices" to scan for nearby WiFi Direct devices

点击"Discover Devices"扫描附近的WiFi Direct设备

Select a device from the list and click "Connect"

从列表中选择一个设备并点击"Connect"

Once connected, the application will automatically connect to the chat server

连接成功后，应用程序将自动连接到聊天服务器

Type a message in the input field and click "Send" to send a message

在输入框中输入消息并点击"Send"发送消息

Screenshots

截图

Device Discovery

设备发现

Chat Interface

聊天界面

Project Structure

项目结构

├── app/

│   ├── src/

│   │   ├── main/

│   │   │   ├── AndroidManifest.xml

│   │   │   ├── java/com/iosdevlog/p2p/

│   │   │   │   ├── MainActivity.kt

│   │   │   │   ├── WifiDirectManager.kt

│   │   │   │   ├── ChatClient.kt

│   │   │   │   └── ChatServer.kt

│   │   │   └── res/

│   │   └── test/

│   └── build.gradle.kts

└── build.gradle.kts

Permissions

权限说明

The application requires the following permissions: 应用程序需要以下权限：

ACCESS_WIFI_STATE

: To check WiFi status

ACCESS_WIFI_STATE

: 检查WiFi状态

CHANGE_WIFI_STATE

: To enable/disable WiFi Direct

CHANGE_WIFI_STATE

: 启用/禁用WiFi Direct

ACCESS_FINE_LOCATION

: To discover nearby devices

ACCESS_FINE_LOCATION

: 发现附近的设备

ACCESS_COARSE_LOCATION

: To discover nearby devices (Android 12+)

ACCESS_COARSE_LOCATION

: 发现附近的设备（Android 12+）

NEARBY_WIFI_DEVICES

: To discover nearby WiFi Direct devices (Android 13+)

NEARBY_WIFI_DEVICES

: 发现附近的WiFi Direct设备（Android 13+）

INTERNET

: To connect to the chat server

INTERNET

: 连接到聊天服务器

CHANGE_NETWORK_STATE

: To manage network connections

CHANGE_NETWORK_STATE

: 管理网络连接

ACCESS_NETWORK_STATE

: To check network status

ACCESS_NETWORK_STATE

: 检查网络状态

Technologies Used

技术栈

Kotlin

: Primary programming language

Kotlin

: 主要编程语言

Jetpack Compose

: UI framework

Jetpack Compose

: UI框架

WiFi Direct API

: For device discovery and connection

WiFi Direct API

: 用于设备发现和连接

TCP Socket

: For message communication

TCP Socket

: 用于消息通信

License

许可证

This project is licensed under the MIT License. 本项目采用MIT许可证。

Contributing

贡献

Contributions are welcome! Please feel free to submit a Pull Request. 欢迎贡献！请随时提交Pull Request。

Troubleshooting

故障排除

No devices found

: Make sure WiFi is enabled and other devices are in WiFi Direct mode

未找到设备

: 确保WiFi已启用且其他设备处于WiFi Direct模式

Connection failed

: Check if the chat server is running on 192.168.49.1:8080

连接失败

: 检查聊天服务器是否在192.168.49.1:8080上运行

Messages not received

: Verify the WiFi Direct connection is stable

未收到消息

: 验证WiFi Direct连接是否稳定

Authors

作者

iosdevlog

iosdevlog

Version

版本

1.0.0 1.0.0

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTRUxBiaycDVIIIcam51dsvEM2LlYt8d6wzRUJRYfh4clw0N68Smfib8IibLXEyG8SNtU07JKYGYaiatEA/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)

![image-2](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTRUxBiaycDVIIIcam51dsvEMRNv2KZOgRnibRdEr8o9EMib81bTSyC3G6bmLGCyVIwibhUSG90JkhJXCA/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=1)
