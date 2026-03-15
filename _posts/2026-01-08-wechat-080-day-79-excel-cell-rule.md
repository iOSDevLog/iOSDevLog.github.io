---
layout: post
title: "Day 79: Excel Cell 自定义单元格颜色，支持 Rule"
author: iosdevlog
date: 2026-01-08 23:39:47 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486408&idx=1&sn=ba87de4826f0e12e6ef2720b045b6bec&chksm=f95c904fce2b195950c5e1fb59011283486ae9e8137622cc571efa12d0ad7dcce8e06857262f#rd

想要做一个类似 Excel 的工具/网站，用户可以使用脚本/规则定义单元格（Cell）的颜色，比如自己解码图片如何显示的。

Cell — Spreadsheet-like Grid

A React + TypeScript spreadsheet-style grid with numeric headers, auto-fit and fixed sizing, selection + manual coloring, rule-based coloring, image mapping, and JSON save/load.

Demo

Run the local demo (Vite):

cd apps/demo

npm run dev

Open http://localhost:5173.

Features

Numeric row/column headers (1-based)

Fixed sizing or auto-fit sizing (fills container)

Responsive layout recalculation on resize

Scroll on overflow or min cell constraints

Single-cell selection highlight

Manual color fill

Rule-based coloring (JSON rules)

Image-to-grid mapping (nearest neighbor)

Save/load grid state as JSON

Zoom (0.5x–2.0)

Screenshots

Cell —— 类 Excel 网格

基于 React + TypeScript 的类 Excel 网格组件，支持数字行列头、自动/固定 尺寸、选择与填色、规则脚本着色、图片映射着色，以及 JSON 保存/加载。

运行 Demo

cd apps/demo

npm run dev

浏览器打开 http://localhost:5173。

功能特性

行/列数字表头（从 1 开始）

固定尺寸或自动填充尺寸

容器变化时自动重新布局

内容溢出时滚动

单元格选择高亮

手动填色

规则脚本着色（JSON）

图片映射着色（最近邻）

JSON 保存/加载

缩放（0.5x–2.0）

截图

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTSRn2zeyh2PnQibSTkoAgmRdO0LVFLXY8koGibicKLO40OfJ8HZheAr15u13MAM48eux740RibjaZia02A/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)

![image-2](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTSRn2zeyh2PnQibSTkoAgmRdILRchd3x686llqcIqP2rbicrZBYnMofSlaib1bZicffm8v1oy1cEeHVcg/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=1)

![image-3](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTSRn2zeyh2PnQibSTkoAgmRdnic26k3oiczLuA71ROsnxVAOT6PxXcTkEvlEgfakQKJF7KoMWlHsQ9gw/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=2)
