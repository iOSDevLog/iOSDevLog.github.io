---
layout: post
title: "Day 92: Android AR 相册"
author: iosdevlog
date: 2026-03-04 22:54:29 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486675&idx=1&sn=1c921e9cce31c0116a3a70fb50533405&chksm=f95c9754ce2b1e42dc2705919823676a19f989af511a1119a4a885cde27b81cb5b85c62fe7b8#rd

AR 照片摆放（Android）

一个 Android AR 照片摆放应用。

从相册选择照片，在 AR 空间中放置、移动、缩放、旋转，并支持保存与恢复。

安装

https://www.pgyer.com/arphotolibrary

截图

功能

从相册选择图片并放入 AR 场景

空中锚点放置（点击屏幕即可放置到相机前方）

点击选中；再次点击已选中照片可删除

长按拖动照片

双指缩放与旋转

保存/恢复照片位置、旋转、缩放

一键清空全部照片

已授权时自动进入 AR 页面

运行要求

Android 7.0 及以上（minSdk 24）

设备支持 ARCore

需要相机与媒体读取权限

构建

./gradlew :app:assembleDebug

使用

安装并启动应用。

首次启动授予权限。

点击 📷 添加照片 选择图片。

点击屏幕进行放置。

点击 💾 保存，重启后自动恢复。

，时长

00:25

English Version

See README.md.

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/rgPAIfdrfVz3l4265y6wRltF8lyYYL6g8m2rVrI9icpQjWaYn2jjicXL2xGbAjdOeZTnfVEkChIKNAiaibMrIemOawvklU7E3jrric3u4jhaicjSg/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)

![image-2](https://mmbiz.qpic.cn/sz_mmbiz_png/rgPAIfdrfVwcTllnhCdyicnicszsrsYDiariaj0g84PNQWDlIn6jbnXAtYHqRXAIUdwCBVV8icCBGyCxQfa65dOxg6ib5yLyMaZYnZr5FW4icG5kVE/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=1)

![image-3](https://mmbiz.qpic.cn/mmbiz_png/rgPAIfdrfVy2t1P6xbHFr1qvpsSAIgJEt8J9B6hWRZTa9jYBIKZBDDiby9l21fwE4hydagEn86adHCiaPAfmGIvmhbNVOmpXY7hXuy1Br6icFU/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=2)

![image-4](https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486675&idx=1&sn=1c921e9cce31c0116a3a70fb50533405&chksm=f95c9754ce2b1e42dc2705919823676a19f989af511a1119a4a885cde27b81cb5b85c62fe7b8)
