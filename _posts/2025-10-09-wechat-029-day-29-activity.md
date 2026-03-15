---
layout: post
title: "Day 29: 打造自己的悬浮窗 Activity 名称"
author: iosdevlog
date: 2025-10-09 23:49:29 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247485893&idx=1&sn=c32d6059c39960812e68db7c1f080ed7&chksm=f95c9242ce2b1b5446cd6feff83e1115bca86ffc4eab1922ee2059c8309f77c8871890c32121#rd

Activity Name Monitor

一个用于显示 Android 设备上当前最顶层 Activity 名称的悬浮窗应用。

，时长

00:33

截图

功能特性

🪟 悬浮窗显示 - 实时显示任意应用的最顶层 Activity 名称

🔄 三种显示模式 - 点击切换显示：

简单名称（类名）

完整名称（包名.类名）

应用名称

👆 可拖动 - 长按拖动悬浮窗到任意位置

⚡ 自动靠边 - 松手后自动吸附到屏幕边缘（带平滑动画）

🎨 Material Design 3 - 现代化的 UI 设计

🔔 前台服务 - 持续监控，不会被系统杀死

截图

技术栈

Kotlin

- 100% Kotlin 编写

Jetpack Compose

- 现代化的声明式 UI 框架

Material Design 3

- Google 最新设计规范

Coroutines

- 异步编程

UsageStatsManager

- Activity 检测

WindowManager

- 悬浮窗管理

系统要求

Android 7.0 (API 24) 或更高版本

需要授予以下权限：

悬浮窗权限（SYSTEM_ALERT_WINDOW）

使用情况访问权限（PACKAGE_USAGE_STATS）

安装

方式 1：从源码构建

# 克隆仓库

git clone <repository-url>

cd ActivityName

# 构建 Debug APK

./gradlew assembleDebug

# 安装到设备

adb install app/build/outputs/apk/debug/app-debug.apk

方式 2：下载 APK

从 Releases 页面下载最新的 APK 文件并安装。

使用方法

启动应用

打开 Activity Name Monitor 应用

授予权限

点击「启动悬浮窗」按钮

在弹出的设置页面中授予悬浮窗权限

在使用情况访问设置页面中授予权限

使用悬浮窗

悬浮窗会显示当前最顶层的 Activity 名称

点击

悬浮窗可切换显示模式

长按拖动

悬浮窗到任意位置

松手后悬浮窗会自动吸附到最近的屏幕边缘

停止服务

返回应用主界面

点击「停止悬浮窗」按钮

开发

环境配置

Android Studio Hedgehog | 2023.1.1 或更高版本

JDK 11 或更高版本

Android SDK 36

构建项目

# 清理构建

./gradlew clean

# 构建 Debug 版本

./gradlew assembleDebug

# 构建 Release 版本

./gradlew assembleRelease

# 运行测试

./gradlew test

./gradlew connectedAndroidTest

项目结构

app/src/main/java/com/iosdevlog/activityname/

├── MainActivity.kt           # 主界面，处理权限和服务控制

├── OverlayService.kt        # 悬浮窗服务，核心功能实现

└── ui/theme/                # Material3 主题配置

├── Color.kt

├── Theme.kt

└── Type.kt

核心实现

1. 悬浮窗服务 (OverlayService)

// 使用 ComposeView 在 Service 中显示 Compose UI

classOverlayService : Service(),

LifecycleOwner,

ViewModelStoreOwner,

SavedStateRegistryOwner {

// ...

}

2. Activity 检测

// 使用 UsageStatsManager 查询前台 Activity

val usageStatsManager = getSystemService(USAGE_STATS_SERVICE) as UsageStatsManager

val events = usageStatsManager.queryEvents(currentTime - 2000, currentTime)

3. 拖动和靠边

// 自定义 OnTouchListener 实现拖动

overlayView?.setOnTouchListener { view, event ->

when (event.action) {

MotionEvent.ACTION_DOWN -> { /* 记录初始位置 */ }

MotionEvent.ACTION_MOVE -> { /* 更新窗口位置 */ }

MotionEvent.ACTION_UP -> { /* 自动靠边 */ }

}

}

// 使用 ValueAnimator 实现平滑靠边动画

ValueAnimator.ofInt(startX, targetX).apply {

duration = 300

addUpdateListener { animator ->

params.x = animator.animatedValue asInt

windowManager.updateViewLayout(overlayView, params)

}

start()

}

架构设计

权限处理流程

MainActivity

↓

检查悬浮窗权限

↓ (未授权)

请求 SYSTEM_ALERT_WINDOW

↓

检查使用情况访问权限

↓ (未授权)

请求 PACKAGE_USAGE_STATS

↓

启动 OverlayService

悬浮窗更新流程

OverlayService 启动

↓

创建前台通知

↓

启动协程定时器 (每1秒)

↓

查询 UsageStatsManager

↓

获取最近的 MOVE_TO_FOREGROUND 事件

↓

根据显示模式格式化 Activity 名称

↓

更新悬浮窗 UI

常见问题

Q: 为什么需要使用情况访问权限？

A: 该权限允许应用查询其他应用的使用情况，从而检测当前前台的 Activity。这是一个受保护的权限，需要用户在系统设置中手动授予。

Q: 悬浮窗不显示怎么办？

A: 请确保：

已授予悬浮窗权限

已授予使用情况访问权限

服务正在运行（通知栏会显示通知）

设备的省电模式没有限制该应用

Q: 为什么有时检测不到 Activity 名称？

A: 某些系统应用可能限制了信息访问，或者某些应用使用了特殊的 Activity 启动模式。这是正常现象。

Q: 如何自定义悬浮窗样式？

A: 修改 OverlayService.kt 中的 OverlayContent 函数：

@Composable

funOverlayContent(

activityInfo: String,

onClickToggle: () -> Unit

) {

Box(

modifier = Modifier

.background(

color = Color(0xCC000000), // 修改背景色

shape = RoundedCornerShape(8.dp) // 修改圆角

)

.clickable { onClickToggle() }

.padding(12.dp) // 修改内边距

) {

Text(

text = activityInfo,

color = Color.White, // 修改文字颜色

fontSize = 14.sp // 修改字体大小

)

}

}

贡献

欢迎提交 Issue 和 Pull Request！

开发指南

Fork 本仓库

创建特性分支 (git checkout -b feature/AmazingFeature)

提交更改 (git commit -m 'Add some AmazingFeature')

推送到分支 (git push origin feature/AmazingFeature)

开启 Pull Request

许可证

MIT License

致谢

Jetpack Compose - 现代化 UI 工具包

Material Design 3 - 设计规范

Android Developer Documentation - 官方文档

联系方式

作者: iosdevlog

项目链接: https://github.com/build-your-own-x-with-ai/ActivityName

如果这个项目对你有帮助，请给它一个 ⭐️链接:https://pan.baidu.com/s/1hjvHDnAHsCuQhaC5K1LMeQ?pwd=3kxq 提取码:3kxq

![image-1](https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247485893&idx=1&sn=c32d6059c39960812e68db7c1f080ed7&chksm=f95c9242ce2b1b5446cd6feff83e1115bca86ffc4eab1922ee2059c8309f77c8871890c32121)

![image-2](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTTeqqczLnYNfvMs1iaPjROdI9Ynn47jZsJlcTlmA0q2eZWicss9AgIMiaFdOOkcabpZWEHTM0zPUksZw/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)

![image-3](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTTeqqczLnYNfvMs1iaPjROdIzkAvIzcrOyG8tG0PibwDOib0LUqgZVngRNIlhibp99S8uUPYylf1kI6sQ/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=1)
