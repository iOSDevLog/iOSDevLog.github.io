---
layout: post
title: "Day 31: Kotlin Jetpack Compose 集成 VLC 播放视频 Demo"
author: iosdevlog
date: 2025-10-11 23:40:59 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247485913&idx=1&sn=7407172eee0c5c7a85f4297df8b4d6e5&chksm=f95c925ece2b1b4830d5e7d39c74634fc53e9bd0d8a8ea819cd1c4aab32612ea38f513e75482#rd

LibVLC Android 示例

This repository contains sample Android applications demonstrating how to use LibVLC (VLC media player library) in Android applications.

本仓库包含演示如何在 Android 应用中使用 LibVLC（VLC 媒体播放器库）的示例 Android 应用程序。

安装

链接: https://pan.baidu.com/s/1hjvHDnAHsCuQhaC5K1LMeQ 提取码:3kxq

示例

1. Compose 示例 (compose_sample)

A modern Android video player built with Jetpack Compose and LibVLC.

1. Compose Sample (compose_sample)

A modern Android video player built with Jetpack Compose and LibVLC.

功能特性

网络视频播放

- 播放来自 HTTP/HTTPS URL 或流协议（HLS、RTSP 等）的视频

本地资源播放

- 播放应用程序资源中捆绑的视频文件

设备视频选择

- 从设备存储中选择并播放视频

Jetpack Compose UI

- 使用 Material Design 3 的现代声明式 UI

LibVLC 集成

- 利用 VLC 强大的媒体播放功能

Features

Network Video Playback

- Play videos from HTTP/HTTPS URLs or streaming protocols (HLS, RTSP, etc.)

Local Asset Playback

- Play video files bundled in the app's assets

Device Video Selection

- Select and play videos from device storage

Jetpack Compose UI

- Modern declarative UI with Material Design 3

LibVLC Integration

- Leverages VLC's powerful media playback capabilities

架构

Jetpack Compose

用于 UI

VLCVideoLayout

用于视频渲染

状态管理

使用 Compose 状态和 remember

Activity Result API

用于设备视频选择

Kotlin

作为主要语言

Architecture

Jetpack Compose

for UI

VLCVideoLayout

for video rendering

State management

using Compose state and remember

Activity Result API

for device video selection

Kotlin

as primary language

主要组件

MainActivity.kt

- 入口点和主要 UI 逻辑

VideoPlayerView.kt

- 使用 LibVLC 的可组合视频播放器视图

ui/theme/

- Material Design 3 主题配置

Key Components

MainActivity.kt

- Entry point and main UI logic

VideoPlayerView.kt

- Composable video player view using LibVLC

ui/theme/

- Material Design 3 theme configuration

使用方法

应用程序提供三种播放视频的方式：

播放网络视频

默认 URL: http://devimages.apple.com/iphone/samples/bipbop/gear1/prog_index.m3u8

输入任何有效的视频 URL（HTTP、HTTPS、HLS、RTSP 等）

点击"播放网络视频"按钮

播放示例视频（资源）

播放来自 assets/bbb.m4v 的捆绑示例视频

点击"播放示例视频（资源）"按钮

从设备选择视频

打开系统视频选择器

从设备存储中选择任何视频

需要 READ_MEDIA_VIDEO 权限（Android 13+）或 READ_EXTERNAL_STORAGE（Android 12 及以下）

Usage

The app provides three ways to play videos:

Play Network Video

Default URL: http://devimages.apple.com/iphone/samples/bipbop/gear1/prog_index.m3u8

Enter any valid video URL (HTTP, HTTPS, HLS, RTSP, etc.)

Click "Play Network Video" button

Play Sample Video (Asset)

Plays bundled sample video from assets/bbb.m4v

Click "Play Sample Video (Asset)" button

Select Video from Device

Opens system video picker

Select any video from device storage

Requires READ_MEDIA_VIDEO permission (Android 13+) or READ_EXTERNAL_STORAGE (Android 12 and below)

权限

<uses-permissionandroid:name="android.permission.INTERNET" />

<uses-permissionandroid:name="android.permission.READ_EXTERNAL_STORAGE"android:maxSdkVersion="32" />

<uses-permissionandroid:name="android.permission.READ_MEDIA_VIDEO" />

Permissions

<uses-permissionandroid:name="android.permission.INTERNET" />

<uses-permissionandroid:name="android.permission.READ_EXTERNAL_STORAGE"android:maxSdkVersion="32" />

<uses-permissionandroid:name="android.permission.READ_MEDIA_VIDEO" />

2. Java 示例 (java_sample)

使用 Java 和 LibVLC 的传统 Android 视频播放器。

3. Native 示例 (native_sample)

使用原生代码 (JNI) 的 LibVLC 示例。

2. Java Sample (java_sample)

Traditional Android video player using Java and LibVLC.

3. Native Sample (native_sample)

Example of using LibVLC with native code (JNI).

构建项目

先决条件

Android Studio Arctic Fox 或更高版本

Android SDK API 36

Gradle 8.14.1 或更高版本

JDK 11 或更高版本

Building the Project

Prerequisites

Android Studio Arctic Fox or later

Android SDK API 36

Gradle 8.14.1 or later

JDK 11 or later

构建步骤

克隆仓库：

git clone <repository-url>

cd libvlc

构建项目：

./gradlew build

构建特定示例：

# Compose 示例

./gradlew :compose_sample:assembleDebug

# Java 示例

./gradlew :java_sample:assembleDebug

# Native 示例

./gradlew :native_sample:assembleDebug

安装到设备/模拟器：

# Compose 示例

./gradlew :compose_sample:installDebug

# 或使用 adb

adb install compose_sample/build/outputs/apk/debug/compose_sample-debug.apk

Build Steps

Clone the repository:

git clone <repository-url>

cd libvlc

Build the project:

./gradlew build

Build specific sample:

# Compose sample

./gradlew :compose_sample:assembleDebug

# Java sample

./gradlew :java_sample:assembleDebug

# Native sample

./gradlew :native_sample:assembleDebug

Install on device/emulator:

# Compose sample

./gradlew :compose_sample:installDebug

# Or using adb

adb install compose_sample/build/outputs/apk/debug/compose_sample-debug.apk

LibVLC 集成

本项目使用 LibVLC 4.0（目前正在开发中）。该库作为本地模块包含（libvlc）。

LibVLC Integration

This project uses LibVLC 4.0 (currently in development). The library is included as a local module (libvlc).

使用的关键 LibVLC 组件

LibVLC

- 主库实例

MediaPlayer

- 媒体播放控制器

Media

- 表示媒体项（文件、URL、资源）

VLCVideoLayout

- 用于渲染视频输出的视图

Key LibVLC Components Used

LibVLC

- Main library instance

MediaPlayer

- Media playback controller

Media

- Represents a media item (file, URL, asset)

VLCVideoLayout

- View for rendering video output

Example Integration

// Initialize LibVLC

val libVLC = remember {

LibVLC(context, arrayListOf("-vvv"))

}

// Create MediaPlayer

val mediaPlayer = remember {

MediaPlayer(libVLC)

}

// Create video view

AndroidView(

factory = { ctx ->

VLCVideoLayout(ctx).apply {

mediaPlayer.attachViews(this, null, false, false)

}

}

)

// Load and play media

val media = Media(libVLC, uri)

mediaPlayer.media = media

media.release()

mediaPlayer.play()

// Cleanup

DisposableEffect(Unit) {

onDispose {

mediaPlayer.release()

libVLC.release()

}

}

支持的格式

LibVLC 支持广泛的媒体格式和协议：

视频编解码器

H.264/AVC

H.265/HEVC

VP8/VP9

MPEG-1/2/4

以及更多...

流协议

HTTP/HTTPS

HLS (HTTP Live Streaming)

RTSP

RTMP

以及更多...

容器格式

MP4

MKV

AVI

WebM

以及更多...

Supported Formats

LibVLC supports a wide range of media formats and protocols:

Video Codecs

H.264/AVC

H.265/HEVC

VP8/VP9

MPEG-1/2/4

And many more...

Streaming Protocols

HTTP/HTTPS

HLS (HTTP Live Streaming)

RTSP

RTMP

And many more...

Container Formats

MP4

MKV

AVI

WebM

And many more...

故障排除

常见问题

找不到 Activity 错误

确保 build.gradle 和源代码之间的包名匹配

清理并重新构建：./gradlew clean build

安装前从设备卸载旧版本

Troubleshooting

Common Issues

Activity not found error

Ensure package names match between build.gradle and source code

Clean and rebuild: ./gradlew clean build

Uninstall old version from device before installing

视频无法播放

检查 logcat 中的 VLC/libvlc 日志

验证权限是否已授予

确保视频 URL 可访问

检查流媒体的网络连接

构建错误

同步 Gradle 文件

使缓存无效并重新启动 Android Studio

检查 Android SDK 和构建工具版本

调试日志

LibVLC 使用详细日志记录（-vvv）进行初始化。检查 logcat：

adb logcat -s "VLC:*""libvlc:*"

Video not playing

Check logcat for VLC/libvlc logs

Verify permissions are granted

Ensure video URL is accessible

Check network connectivity for streaming

Build errors

Sync Gradle files

Invalidate caches and restart Android Studio

Check Android SDK and build tools versions

Debug Logging

LibVLC is initialized with verbose logging (-vvv). Check logcat:

adb logcat -s "VLC:*""libvlc:*"

许可证

本项目遵循 VideoLAN 许可证条款。有关详细信息，请参见各个示例的 LICENSE 文件。

资源

LibVLC Android 文档

VLC 媒体播放器

VideoLAN Wiki

Jetpack Compose 文档

贡献

欢迎贡献！请随时提交拉取请求或为错误和功能请求开启议题。

示例来源

示例视频："Big Buck Bunny" 由 Blender Foundation 制作（知识共享许可）

测试 HLS 流：Apple 的 Bipbop 示例流

License

This project follows the VideoLAN license terms. See individual sample LICENSE files for details.

Resources

LibVLC Android Documentation

VLC Media Player

VideoLAN Wiki

Jetpack Compose Documentation

Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues for bugs and feature requests.

Sample Credits

Sample video: "Big Buck Bunny" by Blender Foundation (Creative Commons)

Test HLS stream: Apple's Bipbop sample stream

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTQtU68S4S7UgwianP0fkZIeEiaBjBuaibj54b8ibtyCeGYA7qcyDkiadXXDd8AJuxZ0kvkFn5TBKG7miaqg/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)

![image-2](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTQtU68S4S7UgwianP0fkZIeEqEEcEVxCPVfnks4nMfN3dJicwsDcMibXLKLVMHO2EV2UuUpujEhJOaJQ/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=1)

![image-3](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTQtU68S4S7UgwianP0fkZIeEcuW3tzGQySkzl4KRSWpbTm6rQR5GZR6ZZjgbDm1JJWmdmCQjtFketw/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=2)
