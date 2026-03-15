---
layout: post
title: "Day 2: ASCII Art"
author: iosdevlog
date: 2025-09-02 01:34:40 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247485645&idx=1&sn=879819152c3eef71d518db62533d1b2d&chksm=f95c934ace2b1a5c6b6cfa28c8506a269476d234b3fa594a35803ddfa042f9579457024743e7#rd

https://github.com/new

SSH

cat ~/.ssh/id_ed25519.pub

Claude Code

使用 C 语言编写一个命令行工具，输入图片，在终端显示对应的 ASCII Art，添加是否输出彩色 ASCII  Art 选项。更新 README.md，提交 Git。

https://docs.github.com/en/authentication/connecting-to-github-with-ssh

● Update Todos

⎿  ☒ 分析项目结构并了解现有代码

☒ 创建 C 语言 ASCII Art 转换核心功能

☒ 实现命令行参数解析（输入文件、彩色选项）

☒ 添加图片加载和处理功能（支持常见格式）

☒ 实现彩色 ASCII Art 输出功能

☒ 创建 Makefile 用于编译

☒ 更新 README.md 文档

☒ 测试工具功能

☒ 提交 Git 更改

● ✅ 已完成 C 语言 ASCII Art 命令行工具！

主要功能：

- 图片转 ASCII Art：支持 JPEG、PNG、BMP、TGA、PSD、GIF、HDR、PIC 格式

- 彩色输出选项：使用 -c 或 --color 启用彩色 ASCII Art

- 自定义宽度：使用 -w 或 --width 设置输出宽度

- 完整的构建系统：包含 Makefile，支持编译、清理、安装等操作

使用方法：

./ascii-art image.jpg           # 基本用法

./ascii-art -c image.jpg        # 彩色输出

./ascii-art -w 120 image.jpg    # 自定义宽度

./ascii-art -c -w 100 image.jpg # 组合选项

已成功编译、测试并提交到 Git。

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTSRf28NwnbKO0gTlDyuia45vtpgsFY4oedWFcdBSEYXruXeicjowFRnOSCcaaNo1ib2maBdOgyZIwwUw/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)

![image-2](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTSRf28NwnbKO0gTlDyuia45vE6NPvicsibfiakiaCqqDRRHohZS4KzDE00BoMRjtKxSY219DVPdXEF7iaiaQ/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=1)

![image-3](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTSRf28NwnbKO0gTlDyuia45vCGI73ClOh5riaSULxRvcwEnQOrxlhHFm1a57mFXjOghgZMeib3Cy0Epg/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=2)

![image-4](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTSRf28NwnbKO0gTlDyuia45vthOy9Qouz0S5blZlskE2KpuXkR82tp4IkXeIlaWDpYx6yhGuosTPUQ/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=3)

![image-5](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTSRf28NwnbKO0gTlDyuia45vCYBra7Y5bIpxTNYXp3VOLptib2jqcnOEHWCbvgJUicALenCFxgfWI0AA/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=4)

![image-6](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTSRf28NwnbKO0gTlDyuia45vnicaQia9CcLvt4V1iciaZVyY0QKcOicdLP1lFOibyicnTxsFt5XM2JQradYjA/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=5)
