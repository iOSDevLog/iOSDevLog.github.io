---
layout: post
title: "Day 90: OpenClaw 聊天渠道连接飞书，下载并隐藏 GESP 真题答案"
author: iosdevlog
date: 2026-03-01 22:31:03 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486637&idx=1&sn=94c91c149af0762ecb2d6c48bb5de12d&chksm=f95c972ace2b1e3c959a540bb41db9653983840770e622d9fdf740a02483b9cbe002a6414838#rd

安装 OpenClaw

https://docs.openclaw.ai/zh-CN/install

安装

除非有特殊原因，否则请使用安装器。它会设置 CLI 并运行新手引导。

快速安装（推荐）

curl -fsSL https://openclaw.ai/install.sh | bash

Windows（PowerShell）：

iwr -useb https://openclaw.ai/install.ps1 | iex

下一步（如果你跳过了新手引导）：

openclaw onboard --install-daemon

系统要求

Node >=22

macOS、Linux 或通过 WSL2 的 Windows

pnpm

仅在从源代码构建时需要

飞书开发平台

https://open.feishu.cn/app?lang=zh-CN

https://docs.openclaw.ai/zh-CN/channels/feishu

飞书手机版本访问 OpenClaw

OpenClaw 实现下载 GESP PDF 真题并且隐藏答案。

i@MacBook-Pro-M4 ~ % openclaw dashboard

🦞 OpenClaw2026.2.26(bc50708)—Chat APIs that don't require a Senate hearing.

Dashboard URL: http://127.0.0.1:18789/#token=c8ec709fed177f86ce1185bfe97c05770669f4e81a50aaee

Copied to clipboard.

Opened in your browser. Keep that tab to control OpenClaw.

![image-1](https://mmbiz.qpic.cn/mmbiz_png/rgPAIfdrfVyGTnriaUrEpyL0C9mjdiceAKR2lvumPK9iccRYa2bePaBG3WkcLRcdyU1EFZibRFicvqJGOhu39tm60Iibj02vQgZaxNqsAibvEChMrg/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)

![image-2](https://mmbiz.qpic.cn/mmbiz_png/rgPAIfdrfVyuIibABTbrpz2nz6QrxKASqicdWphH16lAQ60sb6Vg91vdcUkBRKmL0k968VRh0ib0ISIC7JwudRciarrl9ogKPjUY45ZrZAD9ibUM/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=1)

![image-3](https://mmbiz.qpic.cn/sz_mmbiz_png/rgPAIfdrfVyBM3REjiaVF1F9LxB6IWLFOqpYhvuibZ6oG2Jx01ibsCWGdXZvWKWYmxuQLwfaZgHjR6H1Tl0m2D14q4afh8Aia9YKnGJZpm2I2Nc/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=2)

![image-4](https://mmbiz.qpic.cn/mmbiz_png/rgPAIfdrfVzBcEGP3xq2iaD1iav22SMQrcXD3361uJWTwFcSsb9clegx7qstxEtsTZdk0rLAUqNxTLeBvTwm5AibsmjcWJTibiah3aZq7RnxU0LM/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=3)

![image-5](https://mmbiz.qpic.cn/sz_mmbiz_png/rgPAIfdrfVxZH8AsbEkVMMmGjmJ69UVYP5H6Oyn0bnVgtK8q8nM2fcFMedAJCia5OGR0JW5MevmqhttMN0wh86UvbcibHIp6w9vTMho9iaeOp8/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=4)
