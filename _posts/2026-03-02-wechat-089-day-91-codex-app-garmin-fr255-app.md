---
layout: post
title: "Day 91: Codex App 开发佳明手表（Garmin）fr255 日历 app"
author: iosdevlog
date: 2026-03-02 23:25:00 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486650&idx=1&sn=f9b252719fe1f420bad133cdb32b47f9&chksm=f95c973dce2b1e2b9d8c3d8fe4daaf6f1df84b0c2d6d5eb8b000283b86029809a7fb068adc89#rd

Garmin 日历（Connect IQ）

English | 简体中文

ConnectIQ: https://apps.garmin.com/apps/81d408e1-3fd8-4627-af3a-a3e6a0a65d81

这是一个 Garmin Connect IQ 手表日历应用，支持：

公历模式

农历模式

同时模式（同一日期格同时显示公历和农历）

语言切换：简体中文 / 繁體中文 / English

截图

日历主界面

功能

高亮显示今天

按月份翻页

农历转换带按月缓存（避免性能超时）

农历初一显示为农历月份（如 正月 / 閏二月 / M2）

菜单支持：

显示模式：公历 / 农历 / 同时

语言：简体中文 / 繁體中文 / English

回到今天

构建

示例构建命令：

java -Xms1g -Dfile.encoding=UTF-8 -Dapple.awt.UIElement=true \

-jar "/Users/i/Library/Application Support/Garmin/ConnectIQ/Sdks/connectiq-sdk-mac-8.4.1-2026-02-03-e9f77eeaa/bin/monkeybrains.jar" \

-o bin/Calendar.prg \

-f monkey.jungle \

-y /Users/i/Documents/Garmin/developer_key \

-d fr255_sim -w

模拟器运行：

"/Users/i/Library/Application Support/Garmin/ConnectIQ/Sdks/connectiq-sdk-mac-8.4.1-2026-02-03-e9f77eeaa/bin/monkeydo" \

bin/Calendar.prg fr255

说明

App 名称已支持 eng、zhs、zht 多语言。

启动图标已更新为 40x40 兼容 SVG。

![image-1](https://mmbiz.qpic.cn/mmbiz_png/rgPAIfdrfVzLqSIHYcDzhCjQCYl0ZpPfyZXiaVLia72sHtKR1nBp0j0b6IDMCIjy2lWd31Zu6BERuzqaz4jp3DkUJiaPLCjib6SaAxRRyOryLF0/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)

![image-2](https://mmbiz.qpic.cn/sz_mmbiz_png/rgPAIfdrfVyQRmq1oH5I6xiboEB6iavPIkxcFd0WQRu41yjGA3r9RASS0ibWmTS9lf7spbxCVeVhBQ8w1lVsuVibZiaygLfWpBG56nLFJx5oBz50/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=1)

![image-3](https://mmbiz.qpic.cn/mmbiz_png/rgPAIfdrfVzKkWLT0VYPyRUCvnW23rANnv7OMyNzD3DGNBRscrMR5kpIpibRabKHuQIZWpib2DEk9hgDhdTibvjm0icNN2KZ5kPC5L4Zdt4WaYk/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=2)

![image-4](https://mmbiz.qpic.cn/mmbiz_png/rgPAIfdrfVyRADF7DyQ3jyG1k3LnQYQab7CZFJgIW2pLu1Fg0tJwVmCYSHbdhBtXSBkblIHEHhIFRDP00a3MpcBhPEUrD3vKOTJ20ZJlSHA/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=3)

![image-5](https://mmbiz.qpic.cn/sz_mmbiz_png/rgPAIfdrfVxatGqYYicleo5vICoWApoKsicK3mWY7PDia2ebTmbBdW9WJNaib1DNpz9zNg4KF4UZ1ibbzgb9ic0AkxD6p5DZ4cc7C4IcFEnpbeZxc/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=4)

![image-6](https://mmbiz.qpic.cn/mmbiz_png/rgPAIfdrfVxnibBib6IxgXkk3BIyA0qhfibzIHgYQlMa5lroB3mSIVpWmvD0sdTeeBAkIB1zq7nLyH0NQSw7Mz2OU3DzLGjdkp03dnicibg1tib90/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=5)
