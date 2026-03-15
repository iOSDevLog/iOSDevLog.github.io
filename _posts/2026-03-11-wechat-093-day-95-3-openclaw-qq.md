---
layout: post
title: "Day 95: 3 行命令连接 OpenClaw 与 QQ"
author: iosdevlog
date: 2026-03-11 23:33:14 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486719&idx=1&sn=6e30fd5acf9297eeb3a63eb5acbf5af4&chksm=f95c9778ce2b1e6e9cbf6fe1b3903122a41bfbd3b7798b76f94cc4bc9c03fe5a71ee5417c3cd#rd

https://q.qq.com/qqbot/openclaw/login.html

1.安装OpenClaw开源社区QQBot插件

openclaw plugins install @tencent-connect/openclaw-qqbot@latest

2.配置绑定当前QQ机器人

openclaw channels add --channel qqbot --token "AppID:AppSecret"

3.重启本地OpenClaw服务

openclaw gateway restart

测试

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/rgPAIfdrfVzlrLjvpyviaEC4zHSwttxprHbzVSFtC9TC9w1l7wlaotNZtVpjyCrMXtYwym6RFKE3c78GB2cP5EWia2Ed5pVL5XQXIPfHUr9XE/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)

![image-2](https://mmbiz.qpic.cn/sz_mmbiz_png/rgPAIfdrfVzUwX1o3bBMpYQibCXxedpiczu84J7gZAXBlNSYZHK2AuO75ia6wPrY4gyrjTnSk4Fh5qPpvgY80ic2oyBVyCFYmW23pJJVFu1Dzys/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=1)

![image-3](https://mmbiz.qpic.cn/sz_mmbiz_jpg/rgPAIfdrfVwAve3AQJXTI96xlT0AAhJhvPV1UqjTGKjaqQmm0icNZnviaYCYdVfwISakXLhNJibIVyU1jGbVrUZbRfp2Mria4kJ16O1iamzBf81c/640?wx_fmt=jpeg&from=appmsg&watermark=1#imgIndex=2)
