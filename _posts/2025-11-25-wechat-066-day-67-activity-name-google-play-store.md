---
layout: post
title: "Day 67: Activity Name 上架 Google Play Store"
author: iosdevlog
date: 2025-11-25 23:55:33 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486270&idx=1&sn=490c4045a2d7420ceebeca38e2063a7d&chksm=f95c90b9ce2b19af914c954b4e0cb80d61e3a1aaad54db3e5165a0c5fdf51737a1f34c2a6c23#rd

https://play.google.com/store/apps/details?id=com.iosdevlog.activityname

📸 Google Play Store 资源清单

必需的图形资源

1. 应用图标 (App Icon)

尺寸

: 512 x 512 px

格式

: 32-bit PNG（带 alpha 通道）

文件名

: icon.png

位置

: fastlane/metadata/android/<语言代码>/images/icon.png

要求

:

不能有圆角（系统会自动添加）

不能有透明背景

必须是正方形

2. 特色图片 (Feature Graphic)

尺寸

: 1024 x 500 px

格式

: JPEG 或 24-bit PNG（不带 alpha）

文件名

: featureGraphic.png 或 featureGraphic.jpg

位置

: fastlane/metadata/android/<语言代码>/images/featureGraphic.png

要求

:

在商店列表顶部显示

不能包含文字（除非是应用 logo 的一部分）

建议使用应用的主要视觉元素

3. 手机截图 (Phone Screenshots)

尺寸

:

最小: 320 px

最大: 3840 px

推荐: 1080 x 1920 px 或 1080 x 2340 px

格式

: JPEG 或 24-bit PNG

数量

: 最少 2 张，最多 8 张

文件名

: 1_screenshot.png, 2_screenshot.png, ...

位置

: fastlane/metadata/android/<语言代码>/images/phoneScreenshots/

要求

:

展示应用的主要功能

可以添加文字说明

按顺序显示

4. 7 英寸平板截图 (可选)

尺寸

: 最小 320 px，最大 3840 px

数量

: 最少 1 张，最多 8 张

位置

: fastlane/metadata/android/<语言代码>/images/sevenInchScreenshots/

5. 10 英寸平板截图 (可选)

尺寸

: 最小 320 px，最大 3840 px

数量

: 最少 1 张，最多 8 张

位置

: fastlane/metadata/android/<语言代码>/images/tenInchScreenshots/

必需的文本内容

1. 应用标题 (Title)

字符限制

: 50 字符

文件

: title.txt

位置

: fastlane/metadata/android/<语言代码>/title.txt

✅ 已完成

2. 简短描述 (Short Description)

字符限制

: 80 字符

文件

: short_description.txt

位置

: fastlane/metadata/android/<语言代码>/short_description.txt

✅ 已完成

3. 完整描述 (Full Description)

字符限制

: 4000 字符

文件

: full_description.txt

位置

: fastlane/metadata/android/<语言代码>/full_description.txt

✅ 已完成

4. 版本更新说明 (Release Notes)

字符限制

: 500 字符

文件

: changelogs/<versionCode>.txt

位置

: fastlane/metadata/android/<语言代码>/changelogs/2.txt

可选的文本内容

5. 视频链接 (Promo Video)

文件

: video.txt

内容

: YouTube 视频 URL

位置

: fastlane/metadata/android/<语言代码>/video.txt

目录结构

fastlane/metadata/android/

├── en-US/

│   ├── title.txt                           ✅ 已完成

│   ├── short_description.txt               ✅ 已完成

│   ├── full_description.txt                ✅ 已完成

│   ├── video.txt                           (可选)

│   ├── changelogs/

│   │   └── 2.txt                           (版本更新说明)

│   └── images/

│       ├── icon.png                        (512x512)

│       ├── featureGraphic.png              (1024x500)

│       ├── phoneScreenshots/

│       │   ├── 1_screenshot.png

│       │   ├── 2_screenshot.png

│       │   └── ...

│       ├── sevenInchScreenshots/           (可选)

│       └── tenInchScreenshots/             (可选)

├── zh-CN/

│   └── ... (同上结构)

├── ja-JP/

│   └── ... (同上结构)

└── ... (其他语言)

创建资源的工具

1. 应用图标

在线工具

:

https://icon.kitchen/ (推荐)

https://romannurik.github.io/AndroidAssetStudio/

设计工具

: Figma, Adobe Illustrator, Sketch

2. 特色图片

模板

: Canva, Figma

尺寸

: 1024 x 500 px

建议

: 使用应用的主色调和关键视觉元素

3. 截图

工具

:

Android Studio 模拟器截图

真机截图 (adb shell screencap)

https://mockuphone.com/ (添加设备边框)

https://screenshots.pro/ (批量处理)

4. 截图美化

添加文字说明

: Figma, Canva, Photoshop

设备边框

: Device Art Generator

背景

: 使用品牌色或渐变

快速创建命令

# 创建目录结构

mkdir -p fastlane/metadata/android/en-US/images/phoneScreenshots

mkdir -p fastlane/metadata/android/en-US/changelogs

# 创建其他语言的目录

for lang in zh-CN ja-JP de-DE fr-FR es-ES; do

mkdir -p fastlane/metadata/android/$lang/images/phoneScreenshots

mkdir -p fastlane/metadata/android/$lang/changelogs

done

截图建议

推荐的截图内容：

主界面

- 显示应用的主要功能

权限请求

- 展示悬浮窗和使用情况权限

悬浮窗显示

- 显示悬浮窗在其他应用上的效果

三种显示模式

- 展示简单名称、完整名称、应用名称

使用说明

- 展示应用内的使用说明卡片

截图文字说明建议：

"Monitor Activity Names in Real-Time"

"Easy Permission Setup"

"Floating Overlay Display"

"Three Display Modes"

"Developer-Friendly Tool"

检查清单

在提交前检查：

[ ] 应用图标 (512x512 PNG)

[ ] 特色图片 (1024x500 PNG/JPG)

[ ] 至少 2 张手机截图

[ ] 所有图片符合尺寸要求

[ ] 图片清晰，无模糊

[ ] 文字内容无拼写错误

[ ] 所有必需语言都有资源

自动化工具

使用 Fastlane 的 frameit 工具为截图添加设备边框：

# 安装 frameit

gem install fastlane

# 为截图添加边框

fastlane frameit

参考资源

Google Play 图形资源规范

应用图标设计指南

截图最佳实践

作者: iosdevlog

项目链接: https://github.com/build-your-own-x-with-ai/ActivityName

如果这个项目对你有帮助，请给它一个 ⭐️！

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTRPSlqCrgCoDJ1Q3ibHlzjt7IBmnP98icU7hYomU3ovwmCB2ibpCIQ2QiaL5ahib5S2mCnmn32HIaiaDichA/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)
