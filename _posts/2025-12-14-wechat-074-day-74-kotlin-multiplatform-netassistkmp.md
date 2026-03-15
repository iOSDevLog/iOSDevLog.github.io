---
layout: post
title: "Day 74: Kotlin Multiplatform 网络调试助手 NetAssistKMP"
author: iosdevlog
date: 2025-12-14 23:37:47 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486347&idx=1&sn=1cafff3cf42c3c5c9fda5631a45bbde2&chksm=f95c900cce2b191abf3d80e41a6a25b0d9a65ed05eed9d07083c5b7a7456c069ec5f0bc9c055#rd

NetAssistKMP 是一款基于 Kotlin Multiplatform 和 Compose Multiplatform 构建的全面跨平台网络调试工具。它为开发者提供了统一的界面，用于在 macOS、Windows、Linux、Android 和 iOS 平台上测试 UDP、TCP Server 和 TCP Client 协议。

架构概览

项目结构

项目采用模块化架构，具有清晰的关注点分离：

NetAssistKMP/

├── composeApp/              │   ├── src/

│   │   ├── commonMain/      # 共享 UI 组件

│   │   ├── androidMain/     # Android 特定 UI

│   │   ├── iosMain/         # iOS 特定 UI

│   │   └── jvmMain/         # 桌面 UI

├── shared/                  # 业务逻辑层

│   ├── src/

│   │   ├── commonMain/      # 跨平台业务逻辑

│   │   ├── androidMain/     # Android socket 实现

│   │   ├── iosMain/         # iOS socket 实现

│   │   └── jvmMain/         # JVM socket 实现

├── iosApp/                  # iOS 应用包装器

└── server/                  # 可选的 Ktor 服务器

核心功能

网络协议支持

NetAssistKMP 全面支持三种基础网络协议：

协议

用例

关键特性

UDP

无连接通信

轻量级消息传递、广播支持

TCP Server

多客户端服务器架构

并发客户端处理、选择性消息传递

TCP Client

可靠的客户端-服务器通信

基于流的数据传输、连接监控

数据处理能力

功能

描述

实现

数据模式

ASCII 和 HEX 编码/解码

DataEncoder

实时日志

实时数据流可视化

DataLogView

统计跟踪

发送/接收指标

StatisticsManager

文件操作

数据导出和导入

FileLogger

用户体验功能

直观界面

：Material 3 设计，响应式布局

实时状态

：连接状态监控，可视化指示器

选择性消息传递

：TCP Server 可定向发送消息给特定客户端或广播给所有客户端

键盘管理

：点击关闭功能，改善移动端体验

跨平台一致性

：所有支持平台上的统一行为

技术栈

核心技术

Kotlin Multiplatform

：跨平台代码共享和编译

Compose Multiplatform

：声明式 UI 框架，原生性能

Kotlin Coroutines

：异步编程和并发管理

Material 3

：现代设计系统，具有可访问性功能

平台集成

Android

：原生 socket 实现，Android 特定优化

iOS

：Foundation 框架集成，用于网络操作

JVM 桌面

：标准 Java socket API，Swing 协程集成

开发工作流

构建系统

项目使用带有 Kotlin DSL 的 Gradle 进行构建配置，支持：

多平台编译目标

通过版本目录进行依赖管理

桌面平台的原生分发包

模块依赖

快速开始

对于初学者，推荐的学习路径是：

快速开始

- 设置开发环境并运行应用程序

项目结构

- 理解代码库组织

构建说明

- 学习平台特定的构建流程

掌握基础知识后，探索架构深入分析章节：

Kotlin Multiplatform 架构

- 平台抽象细节

网络服务架构

- 核心网络实现

UI 状态管理

- 响应式状态处理

关键架构模式

服务层模式

网络功能通过服务接口抽象：

NetworkService - 所有协议的通用接口

特定协议实现：UdpService、TcpClientService、TcpServerService

MVVM 架构

Model

：model/ 目录中的数据类和枚举

View

：ui/ 目录中的 Compose UI 组件

ViewModel

：NetworkAssistantViewModel 管理状态和业务逻辑

平台抽象

Socket 实现按平台分离，同时保持通用接口：

socket/ 目录中的通用契约

相应源集中的平台特定实现

NetAssist 是一款强大的跨平台网络调试工具，可帮助开发者测试和排查网络连接问题。它基于 Kotlin Multiplatform 和 Compose Multiplatform 构建，在桌面和移动平台上提供统一的体验。

前置条件

在开始之前，请确保已安装以下组件：

Java 11 或更高版本

- Gradle 和 Kotlin 编译所必需

Android Studio

（用于 Android 开发）

Xcode

（用于 iOS 开发，仅限 macOS）

Git

- 用于克隆代码仓库

获取项目

git clone https://github.com/build-your-own-x-with-ai/NetAssistKMP.git

cd NetAssistKMP

项目架构概览

NetAssist 采用清晰的多平台架构，具有共享业务逻辑和平台特定实现：

快速构建选项

桌面应用程序

平台

命令

输出格式

输出位置

macOS	./build-desktop.sh

DMG

composeApp/build/compose/binaries/main/dmg/

Windows	build-desktop.bat

MSI

composeApp/build/compose/binaries/main/msi/

Linux	./build-desktop.sh

DEB

composeApp/build/compose/binaries/main/deb/

移动应用程序

平台

命令

输出格式

输出位置

Android	./build-android.sh

APK

composeApp/build/outputs/apk/debug/

iOS

在 Xcode 中打开

IPA

通过 Xcode 构建

运行应用程序

桌面开发模式

用于快速测试和开发，直接运行桌面应用程序：

./gradlew :composeApp:run

这将启动开发模式下的应用程序，支持 UI 更改的热重载。

Android 开发模式

在 Android Studio 中打开项目

连接 Android 设备或启动模拟器

选择 composeApp配置

点击运行按钮或使用：

./gradlew :composeApp:installDebug

iOS 开发模式

在 Xcode 中打开 iosApp/iosApp.xcodeproj

选择目标设备或模拟器

点击运行按钮

核心功能概览

NetAssist 提供全面的网络调试功能：

功能类别

功能特性

协议

UDP、TCP 客户端、TCP 服务器（多客户端）

数据模式

ASCII、HEX 编码/解码

实时监控

连接状态、数据日志、统计信息

高级选项

自动换行、AT 命令处理、文件解析

项目结构

NetAssistKMP/

├── composeApp/              │   ├── src/

│   │   ├── commonMain/      # 共享 UI 代码

│   │   ├── androidMain/     # Android 特定 UI

│   │   ├── iosMain/         # iOS 特定 UI

│   │   └── jvmMain/         # 桌面 UI

├── shared/                  # 共享业务逻辑

│   ├── src/

│   │   ├── commonMain/      # 跨平台逻辑

│   │   ├── androidMain/     # Android 网络实现

│   │   ├── iosMain/         # iOS 网络实现

│   │   └── jvmMain/         # 桌面网络实现

├── iosApp/                  # iOS 应用包装器

└── server/                  # 可选的 Ktor 服务器

常用构建命令

开发命令

# 清理构建缓存

./gradlew clean

# 运行桌面应用

./gradlew :composeApp:run

# 构建 Android 调试 APK

./gradlew :composeApp:assembleDebug

# 为当前操作系统打包桌面应用

./gradlew :composeApp:packageDistributionForCurrentOS

平台特定打包

# macOS DMG

./gradlew :composeApp:packageDmg

# Windows MSI

./gradlew :composeApp:packageMsi

# Linux DEB

./gradlew :composeApp:packageDeb

# Android Release APK

./gradlew :composeApp:assembleRelease

# Android App Bundle (Play Store)

./gradlew :composeApp:bundleRelease

故障排除

常见问题

Java 版本

：确保安装了 Java 11+ 并设置为 JAVA_HOME

Android SDK

：创建包含 sdk.dir=/path/to/android/sdk的 local.properties文件

构建失败

：重新构建前尝试 ./gradlew clean

macOS 签名

：对于未签名应用，使用 xattr -cr /Applications/NetAssist.app

对于 Windows MSI 构建，确保已安装 WiX Toolset。构建过程需要默认未包含的特定 Windows 打包工具。

iOS 开发需要配备 Xcode 的 macOS 机器。iOS 项目使用无法在其他平台上构建的 Xcode 项目文件。

后续步骤

应用程序运行后，请探索这些资源：

项目结构

- 深入了解代码库组织结构

构建说明

- 详细的构建配置

功能特性

- 完整的功能文档

如需了解架构和实现细节，请继续阅读

Kotlin Multiplatform 架构

指南。

NetAssistKMP 是一款 Kotlin Multiplatform网络助手应用程序，展示了现代跨平台开发模式。该项目采用模块化架构，在 UI、业务逻辑和平台特定实现之间实现了清晰的关注点分离。

整体架构

项目由三个主要模块组成，在 settings.gradle.kts 中定义：

composeApp

：使用 Compose Multiplatform 的多平台 UI 应用程序

shared

：通用业务逻辑和网络服务

server

：基于 JVM 的后端服务器应用程序

模块结构

composeApp - UI 模块

composeApp模块包含使用 Compose Multiplatform 构建的跨平台用户界面 composeApp/build.gradle.kts。它面向 Android、iOS（ARM64 和模拟器）和 JVM 平台：

composeApp/src/

├── androidMain/          ├── commonMain/           # 共享 UI 组件

├── commonTest/           # 共享 UI 测试

├── iosMain/              # iOS 特定的 UI 代码

└── jvmMain/              # 桌面特定的 UI 代码

composeApp/src/commonMain/kotlin/com/iosdevlog/netassist/ 中的通用 UI 层包含：

App.kt

：应用程序入口点

ui/

：屏幕和组件实现

NetworkAssistantScreen.kt：主应用程序屏幕

ConfigurationPanel.kt：网络配置界面

DataLogView.kt：数据可视化组件

StatisticsBar.kt：实时统计显示

shared - 业务逻辑模块

shared模块包含核心业务逻辑、网络服务和数据模型 shared/build.gradle.kts。这是应用程序的核心：

shared/src/

├── androidMain/          # Android 平台实现

├── commonMain/           # 共享业务逻辑

├── commonTest/           # 共享测试

├── iosMain/              # iOS 平台实现

└── jvmMain/              # JVM 平台实现

shared/src/commonMain/kotlin/com/iosdevlog/netassist/ 中的通用业务逻辑按层次组织：

数据模型(model/)：

NetworkConfig.kt、ProtocolType.kt：网络配置

ConnectionState.kt、NetworkStatistics.kt：状态管理

LogEntry.kt、ReceivedData.kt：数据结构

服务(service/)：

NetworkService.kt：抽象网络服务接口

TcpClientService.kt、TcpServerService.kt：TCP 实现

UdpService.kt：UDP 实现

平台抽象(socket/)：

TcpClientSocket.kt、TcpServerSocket.kt：TCP 套接字抽象

UdpSocket.kt：UDP 套接字抽象

工具类(util/)：

DataEncoder.kt：ASCII/HEX 编码工具

FileReader.kt：文件操作

ValidationUtils.kt：输入验证

状态管理(viewmodel/)：

NetworkAssistantViewModel.kt：中央状态管理

server - 后端模块

server模块提供使用 Ktor 的基于 JVM 的后端服务 server/build.gradle.kts：

server/src/

├── main/

│   ├── kotlin/com/iosdevlog/netassist/

│   │   └── Application.kt    # 服务器入口点

│   └── resources/

│       └── logback.xml        # 日志配置

└── test/                     # 服务器测试

平台特定配置

Android 平台

最低 SDK

：24 gradle/libs.versions.toml

目标 SDK

：36 gradle/libs.versions.toml

编译 SDK

：36 gradle/libs.versions.toml

清单文件

：composeApp/src/androidMain/AndroidManifest.xml

资源

：composeApp/src/androidMain/res/ 中的启动图标和字符串资源

iOS 平台

目标

：ARM64 设备和 ARM64 模拟器 composeApp/build.gradle.kts

框架

：名为 "ComposeApp" 的静态框架

配置

：iosApp/Configuration/Config.xcconfig

应用结构

：iosApp/iosApp/ 中的 Swift 集成

JVM 桌面平台

目标

：JVM 11 composeApp/build.gradle.kts

资源

：composeApp/src/jvmMain/resources/ 中的桌面图标

依赖管理

项目使用 Gradle Version Catalogs进行集中依赖管理 gradle/libs.versions.toml：

技术

版本

用途

Kotlin

2.2.21

核心语言

Compose Multiplatform

1.9.3

UI 框架

Ktor

3.3.3

网络服务器

KotlinX Coroutines

1.10.2

异步编程

AndroidX Lifecycle

2.9.6

生命周期管理

构建配置

项目使用 Kotlin DSL作为构建脚本，启用了类型安全项目访问器 settings.gradle.kts。关键构建文件：

根目录

：build.gradle.kts - 插件管理

Compose App

：composeApp/build.gradle.kts - 多平台 UI 配置

Shared

：shared/build.gradle.kts - 业务逻辑配置

Server

：server/build.gradle.kts - 后端服务配置

支持文件

仓库包含全面的文档和构建自动化：

文档：涵盖 README.md、构建说明、故障排除指南和功能文档的多个 markdown 文件

构建脚本：用于自动编译的平台特定构建脚本（build-android.sh、build-desktop.sh）

图标生成：用于跨所有平台生成应用程序图标的 Python 脚本（generate-icons.py）

测试：测试 TCP 服务器实现（test-tcp-server.py）

这种模块化结构实现了跨平台的 代码复用，同时在需要时保持 平台特定优化。UI、业务逻辑和后端服务之间的分离提供了清晰的架构，为未来的开发提供了良好的扩展性。

下一步

要了解这些模块如何协同工作，请继续阅读

构建说明

以了解如何编译和运行应用程序，然后探索

Kotlin Multiplatform 架构

以获得更深入的架构洞察。

本指南提供了 NetAssist 的完整构建说明，NetAssist 是一款支持桌面端（macOS、Windows、Linux）、Android 和 iOS 平台的 Kotlin Multiplatform 网络助手应用程序。

先决条件

系统要求

要求

最低版本

用途

Java JDK

11 或更高版本

构建环境

Android SDK

API 24+

Android 开发

Xcode

最新版本

iOS 开发

Gradle

8.5+

构建系统

环境设置

在构建之前，请验证您的 Java 安装：

java -version

确保 JAVA_HOME 环境变量已正确设置为 JDK 11 或更高版本的路径，以便成功构建。

快速构建选项

一键构建脚本

项目提供了自动化构建脚本以实现快速部署：

./build-desktop.sh    # macOS/Linux

build-desktop.bat     # Windows

# Android 应用程序

./build-android.sh    # macOS/Linux

build-android.bat     # Windows

这些脚本会自动检测您的平台并执行相应的构建命令 build-desktop.sh。

桌面应用程序构建

开发模式

直接运行桌面应用程序进行测试：

./gradlew :composeApp:run

生产构建

平台特定包

平台

命令

输出格式

输出位置

macOS

./gradlew :composeApp:packageDmg

DMG

composeApp/build/compose/binaries/main/dmg/NetAssist-1.0.0.dmg

Windows

./gradlew :composeApp:packageMsi

MSI

composeApp/build/compose/binaries/main/msi/NetAssist-1.0.0.msi

Linux

./gradlew :composeApp:packageDeb

DEB

composeApp/build/compose/binaries/main/deb/netassist_1.0.0-1_amd64.deb

通用构建命令

为您当前的平台生成相应的包：

./gradlew :composeApp:packageDistributionForCurrentOS

应用程序配置

桌面应用程序的配置在 composeApp/build.gradle.kts 中完成，包括：

包名：NetAssist

版本：1.0.0

供应商：iOSDevLog

描述：Network Assistant - UDP/TCP Client/Server Tool

Android 应用程序构建

开发构建

将调试版本安装到已连接的设备：

./gradlew :composeApp:installDebug

生产构建

APK 构建

构建类型

命令

输出

使用场景

Debug

./gradlew :composeApp:assembleDebug	composeApp-debug.apk

测试和开发

Release

./gradlew :composeApp:assembleRelease	composeApp-release.apk

分发（需要签名）

Google Play 分发

为 Google Play 商店生成 App Bundle：

./gradlew :composeApp:bundleRelease

输出：composeApp/build/outputs/bundle/release/composeApp-release.aab

Android 配置

应用程序详细信息来自 composeApp/build.gradle.kts：

应用 ID：com.iosdevlog.netassist

最低 SDK：24 (Android 7.0)

目标 SDK：36 (Android 14)

版本代码：1

版本名称：1.0

iOS 应用程序构建

框架生成

生成 iOS 框架用于 Xcode 集成：

./gradlew :composeApp:linkDebugFrameworkIosArm64

Xcode 构建过程

在 Xcode 中打开 iosApp/iosApp.xcodeproj

选择目标设备或模拟器

使用 Xcode 的 Run 或 Archive 命令构建

iOS 应用程序通过 iosApp/目录中的 Xcode 项目设置进行配置。

构建架构

Multiplatform 模块结构

依赖管理

项目使用在 gradle/libs.versions.toml 中定义的 Gradle 版本目录进行集中依赖管理，包括：

Kotlin Multiplatform 2.2.21

Compose Multiplatform 1.9.3

Android Gradle Plugin 8.13.2

Ktor 3.3.3

故障排除

常见构建问题

Java 版本错误

# 验证 Java 版本

java -version

# 如有需要，设置 JAVA_HOME

export JAVA_HOME=/path/to/java11

构建缓存问题

# 清理并重新构建

./gradlew clean

./gradlew build

Windows 需要 WiX Toolset

对于 Windows 上的 MSI 构建，请从 https://wixtoolset.org/ 安装 WiX Toolset

macOS 代码签名

如需分发，请配置 Apple Developer 证书。测试时：

# 允许未签名的应用程序

xattr -cr /Applications/NetAssist.app

Android SDK 配置

创建 local.properties文件：

sdk.dir=/path/to/android/sdk

构建输出验证

通过检查输出目录来验证构建是否成功：

桌面端：composeApp/build/compose/binaries/main/

Android：composeApp/build/outputs/

iOS：通过 Xcode 生成

后续步骤

构建完成后，探索应用程序架构：

Kotlin Multiplatform 架构

- 了解多平台项目结构

网络服务架构

- 了解核心网络组件

项目结构

- 熟悉代码组织

有关更多构建细节和平台特定要求，请参阅完整的 BUILD_INSTRUCTIONS.md 文件。

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTSCrwzeDLT0ZvBVicA7ibdtuIc7nRP3ReXktHxEuGiaKUAEdu4QZgjVxfwYicBcw2LhBea0p8SHjy6IhQ/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)

![image-2](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTSCrwzeDLT0ZvBVicA7ibdtuITVMMOuTh6mdy3s0Xx2Fq6LOibtYJiay9gu2gvsIKCFpb10C6RNEndWicw/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=1)

![image-3](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTSCrwzeDLT0ZvBVicA7ibdtuIibt7nvlwJqMmoRGuec6kibPQK37bxuBWLUt5zswFic3WSsHtEszNPvnyQ/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=2)

![image-4](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTSCrwzeDLT0ZvBVicA7ibdtuInd4PDNvRmfftdVjoGLRw6KtMiaFDgY6zxOpjiaBGGm8zbVYyNYibZqa1Q/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=3)

![image-5](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTSCrwzeDLT0ZvBVicA7ibdtuI8Xk2oRkrGyok6ria4rHqwZCWdl23EwwXPB2xDZKfsAKJN1jLFhziaqlg/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=4)

![image-6](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTSCrwzeDLT0ZvBVicA7ibdtuIqvdNDBYTSv2iczHBjN55caZVqZiaabNticH2miah8ETn15Fda7lpw0cBZA/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=5)
