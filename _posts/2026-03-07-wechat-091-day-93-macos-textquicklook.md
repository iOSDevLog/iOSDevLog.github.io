---
layout: post
title: "Day 93: macOS 快速查看文本文件扩展/插件 TextQuickLook"
author: iosdevlog
date: 2026-03-07 22:04:48 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486692&idx=1&sn=ba7731ab5675ae1e6249503f46d0f70e&chksm=f95c9763ce2b1e752bbc9d733a0d4cbcd0f84c3f1334dea79f37ed68d5028098bbb97d0d69d3#rd

TextQuickLook

https://github.com/build-your-own-x-with-ai/TextQuickLook

A macOS Quick Look extension for previewing plain-text scientific files with custom extensions.

用于 macOS 的 Quick Look 插件，支持预览带自定义后缀的科学计算纯文本文件。

Screenshots | 截图

Place your images under docs/media/ with the following names. 请将图片放到 docs/media/ 目录并使用以下文件名。

Feature | 功能

Press Space in Finder to preview text content.

Supports common scientific text file extensions.

Detects text vs binary by content.

Plain-text focused (no heavy rendering).

在 Finder 按 空格 预览文本内容。

支持常见科学计算文本后缀。

按内容判断文本/二进制。

仅纯文本展示，不做复杂渲染。

Supported Extensions | 支持后缀

txt text log out dat data csv tsv json xml yaml yml ini cfg conf xyz cube gjf com inp pdb mol sdf cif vasp poscar contcar xsf test

Requirements | 环境要求

macOS

Xcode 16+

Build & Install | 构建与安装

Open in Xcode and run TextQuickLook.app once.

Reload Quick Look services:

qlmanage -r

qlmanage -r cache

killall Finder

In Finder, select a supported file and press Space.

在 Xcode 中运行一次 TextQuickLook.app。

重载 Quick Look 服务：

qlmanage -r

qlmanage -r cache

killall Finder

在 Finder 选中文件后按 空格。

Troubleshooting | 故障排查

Extension not triggered | 扩展未触发

pluginkit -mAvv -i com.iosdevlog.TextQuickLook.TextQuickLookExtention

Check file UTI | 检查文件 UTI

mdls -name kMDItemContentType -name kMDItemContentTypeTree /path/to/file

View extension logs | 查看扩展日志

log stream --style compact --predicate 'subsystem == "com.iosdevlog.TextQuickLook.TextQuickLookExtention"'

Versioning | 版本说明

This project follows Semantic Versioning (MAJOR.MINOR.PATCH).

本项目遵循语义化版本（主版本.次版本.修订号）。

Changelog | 更新记录

v0.1.0

Initial release.

Quick Look text preview for .test and common scientific text extensions.

Content-based text/binary detection.

Basic in-app usage instructions.

Roadmap | 后续计划

Add optional large-file preview limit.

Add search/highlight in preview.

Expand extension profiles for more scientific workflows.

增加超大文件预览大小限制（可选）。

增加预览内搜索/高亮。

扩展更多科学计算工作流后缀配置。

License | 许可证

MIT License

Copyright (c) 2026 iosdevlog

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

Third-Party Notices | 第三方声明

No third-party runtime dependencies currently.

当前无第三方运行时依赖。

![image-1](https://mmbiz.qpic.cn/mmbiz_svg/Q3auHgzwzM492wC20Pia5QglJudSru7JNWLanBuib4icveWwJcicjJjx9b9jhq7fsx9YDKbo1JCP3E7SeaIS5upzBBUibuE9zrTTfRMxZ8EYqlMz6Kglw9zE88Q/640?wx_fmt=svg&from=appmsg#imgIndex=0)

![image-2](https://mmbiz.qpic.cn/mmbiz_svg/Q3auHgzwzM492wC20Pia5QrDR9eaiaI5ragErdLtficMicpJ3NiaicnzwmdSFPoR9YTcBYUr134VuTMsc9w8Q2n83qI89icAYojkTibLC7c13wOm8kRMWEicW1JthrA/640?wx_fmt=svg&from=appmsg#imgIndex=1)

![image-3](https://mmbiz.qpic.cn/mmbiz_svg/Q3auHgzwzM4uV1dDUibCfcNcp6yNcOW2KayaDWUAUniaiaJ7rPlALkm7Vqrppx0ibEVfSM3UKrKyLnvJ9HEcmCluaLpbxntV7bKa311iaWzet1KJKszd981Qy2A/640?wx_fmt=svg&from=appmsg#imgIndex=2)

![image-4](https://mmbiz.qpic.cn/mmbiz_png/rgPAIfdrfVyIfON43rico3YA22jlo9BnLbyIRXEozticWeichRkJKW7gg2icvXPkYn38QicGaZPxaHJzBmvQClUlxfh63n7al7j1pzOP0Nyfdzic4/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=3)

![image-5](https://mmbiz.qpic.cn/sz_mmbiz_png/rgPAIfdrfVxQq3ztPwROFHz6iaApT66mEfrFK6KktcxyPUELdMBOwl8uoAput4LV2Tyflgbpf4lkibIT612bbib3jibGh29pq8mVTYQcqTy47nk/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=4)

![image-6](https://mmbiz.qpic.cn/mmbiz_png/rgPAIfdrfVxfAkwskxghQs3S9862fibdPLveJdJ1icTjQBzibSDIrtRvZU61MlzXpmZ6zTDcsZq1mrFOxgJPSFmy2stMf82yBZX7hD94icCI6EI/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=5)
