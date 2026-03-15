---
layout: post
title: "Day 30: 打造自己的 AppTime - 应用使用时长统计"
author: iosdevlog
date: 2025-10-10 23:33:27 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247485905&idx=1&sn=b2c14a7c479f9cd7959fc8ea1bd3fb3f&chksm=f95c9256ce2b1b400f100cb92966675321e21aea2e11da6158e87fc454d70cce67384137c2f2#rd

AppTime - 应用使用时长统计

一个简洁的 Android 应用，用于统计和可视化应用使用时长，支持图表展示和数据分享。

安装

链接: https://pan.baidu.com/s/1hjvHDnAHsCuQhaC5K1LMeQ 提取码:3kxq

截图

功能特性

📊 使用统计

实时统计所有应用的使用时长

支持查看今天和过去一周的统计数据

显示每个应用的图标、名称和详细使用时间

自动按使用时长排序

📈 图表可视化

使用饼图展示应用使用时长占比

显示前 10 个最常用应用

列表形式展示所有应用详情

美观的 Material Design 3 界面

📤 分享导出

自动生成精美的长截图

包含饼图和详细的应用列表

显示时间戳和应用信息

支持通过系统分享功能发送到其他应用

高清 PNG 格式输出

权限说明

应用只需要一个权限：

使用情况访问权限 (PACKAGE_USAGE_STATS)

用于获取应用使用统计数据

需要在系统设置中手动授权

使用方法

首次使用

安装应用

./gradlew installDebug

授予权限

打开应用

点击"Grant Permission"授予使用情况访问权限

在系统设置中允许应用访问使用统计数据

日常使用

查看统计

打开应用查看统计数据

切换"Today"和"Week"标签查看不同时间段

刷新数据

点击右上角刷新图标更新统计数据

分享数据

点击右上角分享图标

应用会自动生成包含图表和列表的长截图

选择目标应用分享图片

技术架构

项目结构

app/src/main/java/com/iosdevlog/apptime/

├── model/

│   └── AppUsageInfo.kt              # 数据模型

├── service/

│   └── UsageStatsService.kt         # 使用统计服务

├── viewmodel/

│   └── AppUsageViewModel.kt         # ViewModel

├── utils/

│   └── ScreenshotGenerator.kt       # 截图生成工具

├── ui/

│   ├── screens/

│   │   └── AppUsageScreen.kt        # 主界面

│   └── theme/                       # 主题配置

└── MainActivity.kt                   # 主活动

技术栈

Jetpack Compose

: 现代化 UI 框架

Material Design 3

: 最新设计规范

UsageStatsManager

: 系统使用统计 API

MPAndroidChart

: 图表库

Kotlin Coroutines

: 异步处理

ViewModel & StateFlow

: 状态管理

依赖库

Jetpack Compose BOM

Material 3

MPAndroidChart (图表)

Lifecycle Components

Kotlin Coroutines

构建说明

环境要求

Android Studio Hedgehog | 2023.1.1 或更高版本

JDK 11 或更高版本

Android SDK 34

Gradle 8.0+

构建命令

# 构建 Debug 版本

./gradlew assembleDebug

# 构建 Release 版本

./gradlew assembleRelease

# 安装到设备

./gradlew installDebug

# 运行测试

./gradlew test

# 清理构建

./gradlew clean

注意事项

权限管理

使用情况访问权限需要在系统设置中手动授予

应用不会收集或上传任何个人数据

性能优化

应用使用统计 API 可能在某些设备上有延迟

建议定期刷新数据以获取最新统计

兼容性

最低支持 Android 7.0 (API 24)

目标版本 Android 14 (API 34)

后续优化建议

[ ] 添加数据持久化（Room 数据库）

[ ] 支持自定义时间范围查询

[ ] 添加应用分类统计

[ ] 支持设置使用时长提醒

[ ] 添加数据导出为 CSV/Excel

[x] 支持图表截图分享（已实现）

[ ] 添加深色模式主题

[ ] 支持多种图表类型（柱状图、折线图）

[ ] 优化长截图样式和排版

[ ] 支持自定义截图模板

许可证

MIT License

作者

Generated with Claude Code

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTRKJP3Mqaz022ibmyFxwqKNGKGEAonOJ9NXRan75y23sVPCHq5n1jUPnqz9LFE8Euicdp7BQkJAyvvQ/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)

![image-2](https://mmbiz.qpic.cn/sz_mmbiz_jpg/kIE7WtwNFTRKJP3Mqaz022ibmyFxwqKNGjBSITn5rXTtKmJdeNX6OrIezrdiaEMYrgQmciaeDjoBiatLJ6I8ZrcicOA/640?wx_fmt=jpeg&from=appmsg&watermark=1#imgIndex=1)
