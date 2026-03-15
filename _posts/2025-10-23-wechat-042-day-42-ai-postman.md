---
layout: post
title: "Day 42: AI 打造 postman"
author: iosdevlog
date: 2025-10-23 23:49:18 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486015&idx=1&sn=b2e748c45f510d857f0fce2b7c9f5768&chksm=f95c91b8ce2b18aeffa2ad2c28f398bdbb0d2080342ac81df6c41f9f379662710391286341c4#rd

用户群体

核心用户：API开发测试人员、前端开发者、后端开发者、API产品经理

应用目标：提供一个直观易用的API测试工具，简化API开发测试流程，提高工作效率

功能设计说明

基础功能：

1.请求构建器：支持HTTP/HTTPS请求，可设置请求方法、URL、参数、Headers、Body等

2.响应查看器：展示API返回的状态码、响应头、响应体等信息

3.集合管理：支持创建和管理API请求集合，便于组织和重用

亮点功能：

1.环境变量：支持定义环境变量，便于在不同环境（开发、测试、生产）间切换

2.请求历史：记录历史请求，方便重复测试和对比

设计风格

布局：左侧导航栏展示集合和历史记录，中央区域为请求编辑区，右侧为响应展示区。

交互：拖拽式参数编辑，一键发送请求，响应实时展示。

配色：专业蓝色调为主，搭配中性灰，强调色用于状态指示。

文案：简洁专业的技术术语，操作提示清晰明了。

测试发现功能还不完整，争取聚合 Electron 开发可以测试本地网站。

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTQma0PyPV4XfaCEPxQcaxD6UVLekiaXjlwaf7NpdgQacChLDQOian33ffiabP3h8TkrE8KeRCLVyiacTg/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)
