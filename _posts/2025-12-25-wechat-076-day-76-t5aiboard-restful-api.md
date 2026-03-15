---
layout: post
title: "Day 76: 涂鸦 T5AIBoard 服务端 RESTful API"
author: iosdevlog
date: 2025-12-25 22:13:55 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486357&idx=1&sn=114f4264feec9c00c965d515f376363c&chksm=f95c9012ce2b190464b1ed247faec6e5a46c2d67f18093fe4773c184ae7cc7cc6b53853caa6a#rd

文件管理 RESTful API

一个基于 FastAPI 的文件管理 API，支持文件上传、查看、删除功能，并对上传的文件进行自动处理。

截图

功能特性

文件上传

：支持上传文本文件和图片文件

文件处理

：

竖屏分辨率：最大 480x800

保持宽高比

大于 480x800 的图片会被压缩到符合要求

小于等于 480x800 的图片保持原样

TXT 文档：自动转换为 GBK 编码

图片文件（BMP、PNG、WEBP、HEIC、JPG 等）：自动转换为 1bit BMP 格式

文件管理

：支持查看文件列表、下载文件和删除文件

自动生成 API 文档

：使用 Swagger UI 可访问 http://localhost:8000/docs

安装依赖

pip install -r requirements.txt

启动服务

uvicorn main:app --reload

服务将在 http://localhost:8000 启动。

CURL 使用说明

1. 上传文件

上传文本文件

curl -X POST "http://localhost:8000/files" \

-H "accept: application/json" \

-H "Content-Type: multipart/form-data" \

-F "file=@your_file.txt"

上传图片文件

curl -X POST "http://localhost:8000/files" \

-H "accept: application/json" \

-H "Content-Type: multipart/form-data" \

-F "file=@your_image.png"

2. 获取文件列表

curl -X GET "http://localhost:8000/files"

3. 下载文件

curl -X GET "http://localhost:8000/files/filename.txt" -o downloaded_file.txt

4. 更新文件

curl -X PUT "http://localhost:8000/files/filename.txt" \

-H "accept: application/json" \

-H "Content-Type: multipart/form-data" \

-F "file=@new_content.txt"

5. 删除文件

curl -X DELETE "http://localhost:8000/files/filename.txt"

API 端点

方法

路径

描述

POST

/files

上传文件

GET

/files

获取文件列表

GET

/files/{filename}

下载指定文件

PUT

/files/{filename}

更新指定文件

DELETE

/files/{filename}

删除指定文件

项目结构

.

├── main.py          # API 主文件

├── requirements.txt # 项目依赖

├── README.md        # 项目说明

└── uploads/         # 文件存储目录

注意事项

上传的文件会自动保存在 uploads/ 目录下

文本文件会被转换为 GBK 编码

图片文件会被转换为 1bit BMP 格式

HEIC 格式支持需要 pyheif 库，如果安装失败，HEIC 格式将被禁用

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTSb1Alf3NHhdhv1AyOcMt7aXAxeVLHqye9icKcwyMhcECP3Ov1CYcIMDU3KajRIHmwL0Jtt30ibZ2vA/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)

![image-2](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTSb1Alf3NHhdhv1AyOcMt7abSt7lPm90jnKcg9E61em1icETAuuIIqTk7FCNQvoiadFndP4icceKzbaA/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=1)
