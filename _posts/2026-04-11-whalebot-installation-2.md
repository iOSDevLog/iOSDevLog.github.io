---
layout: post
title: "WhaleBot鲸鱼小车: 安装-2"
author: iosdevlog
date: 2026-04-11 00:00:00 +0800
description: "WhaleBot鲸鱼小车安装教程第二部分"
category: Robotics
tags: [Robotics, WhaleBot, Installation]
---

# WhaleBot鲸鱼小车: 安装-2

## 简介

本文是 WhaleBot 安装教程的第二部分，继续介绍硬件组装和接线步骤。

> 上一篇：[WhaleBot鲸鱼小车: 安装-1](/2026/04/02/whalebot-installation-1.html)

## 硬件组装步骤（续）

### 步骤 2: 安装电机与驱动模块

![WhaleBot-20](/assets/images/WhaleBot/WhaleBot-20.jpg)

![WhaleBot-18](/assets/images/WhaleBot/WhaleBot-18.jpg)

### 天问51 ASRPRO 的烧录

![WhaleBot-19](/assets/images/WhaleBot/WhaleBot-19.jpg)

天问BLOCK
下载地址：http://twen51.com/new/twen51/index.php

![tianwen51](/assets/images/WhaleBot/WhaleBot-tianwen51.png)

串口

![Serial](/assets/images/WhaleBot/WhaleBot-Serial.png)

![Serial2](/assets/images/WhaleBot/WhaleBot-Serial2.png)

| 语音指令 | 执行内容 (TTS/Action) |指令摘要 |
|--|--|--|
| 天问五幺 | 🔊 播报：“我在” | 设备唤醒词 ，用于激活语音交互状态。 |
| 紧急停止 | 已紧急停止 | 最高优先级指令 ，触发急停逻辑，中断当前所有动作。 |
| 取消紧急停止 | 已退出紧急状态 | 解除急停锁定状态，恢复设备待机。 |
| 打开对话模式 | 已打开对话模式 | 切换系统至对话交互逻辑，准备接收聊天指令。 |
| 开始聊天 | 🔇 无语音回复 | 触发聊天功能模块。 |
| 打开运动模式 |  已打开运动模式 | 切换系统至运动控制逻辑，激活电机/底盘控制。 |
| 前进 | 🔇 无语音回复 | 控制设备向前移动。 |
| 后退 | 🔇 无语音回复 | 控制设备向后移动。 |
| 停止 | 🔇 无语音回复 | 结束当前移动指令，设备归零/刹车。 |
| 左转 | 🔇 无语音回复 | 控制设备原地向左旋转。 |
| 右转 | 🔇 无语音回复 | 控制设备原地向右旋转。 |
| 设置为持续运动状态 | 已设置为持续运动状态 | 更改运动逻辑为“保持当前动作直到收到停止指令”。 |
| 退出持续运动状态 | 已退出持续运动状态 | 恢复默认运动逻辑（如点动模式或定时停止）。 |

### 串口屏烧录及其显示内容

开发串口屏的第一步是安装官方配套的设计软件。

软件名称 ：USART-HMI

下载地址 ：[淘晶驰官方下载页](http://wiki.tjc1688.com/download/usart_hmi.html)

第二步是硬件的连接，这里请直接对照引脚表。1

| ASRPRO 引脚 | 串口屏引脚 | 说明 |
|--|--|--|
| 5V | 5V |供电（务必保证电源电流充足，背光全亮时耗电较大）|
| GND | GND | 共地 |
| PB6 | RX | ASRPRO 发送，屏幕接收 |
| PB5 | TX | 屏幕发送，ASRPRO 接收 |

![WhaleBot-21](/assets/images/WhaleBot/WhaleBot-21.jpg)

9600 下载太慢了

![WhaleBot-9600](/assets/images/WhaleBot/WhaleBot-9600.png)

改为 115200

![WhaleBot-115200](/assets/images/WhaleBot/WhaleBot-115200.png)

> 联机成功!串口号:COM3,设备当前波特率:9600,设备型号:TJC3224T120_011R(电阻式触摸),固件版本:S56,设备序列号:D32535013BE7E862,CPUID:61760,Flash容量:4194304(4MB)地址:0
强制下载波特率:115200  开始下载

![WhaleBot-24](/assets/images/WhaleBot/WhaleBot-24.jpg)

![WhaleBot-22](/assets/images/WhaleBot/WhaleBot-22.jpg)

![WhaleBot-23](/assets/images/WhaleBot/WhaleBot-23.jpg)

![WhaleBot-25](/assets/images/WhaleBot/WhaleBot-25.jpg)

### 开机运动测试

<video controls width="100%">
  <source src="/assets/images/WhaleBot/WhaleBot-v1.mp4" type="video/mp4">
  您的浏览器不支持视频播放
</video>

### 整体组装完成

这时可以语音控制智能小车运动。

<video controls width="100%">
  <source src="/assets/images/WhaleBot/WhaleBot-v2.mp4" type="video/mp4">
  您的浏览器不支持视频播放
</video>

## 参考链接

1. [WhaleBot 官方安装教程](https://www.datawhale.cn/learn/summary/268)
2. [WhaleBot鲸鱼小车: 安装-1](/2026/04/02/whalebot-installation-1.html)

---

希望本教程对您有所帮助！如果您有任何问题或建议，请在评论区留言。
