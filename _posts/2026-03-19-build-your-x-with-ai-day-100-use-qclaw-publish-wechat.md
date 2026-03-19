---
layout: post
title: "Day 100: 使用 QClaw 发布微信公众号"
author: iosdevlog
date: 2026-03-19 23:24:00 +0800
description: "Day 100：用 QClaw + Markdown 统一发布微信公众号和博客，提升内容发布效率。"
category: AI
tags: [QClaw, 微信公众号, OpenClaw, 内容发布, 工程化]
---

![Day 100 使用 QClaw 发布微信公众号](/assets/images/day100-qclaw-wechat-publish.png)

# Day 100: 使用 QClaw 发布微信公众号

今天这篇是实战复盘：如何用 QClaw 把一篇 Markdown 稳定发布到微信公众号草稿箱。

目标很简单：**写一次内容，同时用于博客和公众号**，减少重复劳动。

## 为什么用 QClaw 做发布

以前流程通常是：

1. 先在本地写 Markdown
2. 再复制到公众号编辑器
3. 手动调格式、传图、改排版
4. 最后发草稿

这个流程最大的问题是：慢，而且容易在复制过程中引入格式差异。

QClaw 的方式是把“发布”做成可复用流程：

- 内容源头统一（Markdown）
- 发布步骤可重复执行
- 失败时有明确错误信息（比如 IP 白名单）

## 发布前准备

至少需要三件事：

- 微信公众号后台可用的 `AppID`、`AppSecret`
- 调用 IP 已在公众号后台白名单
- 文章 frontmatter 完整（`title` + `cover`）

示例 frontmatter：

```yaml
---
title: "Day 100: 使用 QClaw 发布微信公众号"
cover: /Users/i/.openclaw/workspace/assets/day100-qclaw-wechat-publish.png
---
```

> 注意：封面建议 1080×864，路径用绝对路径更稳。

## 核心发布命令

用 QClaw 的 wechat-toolkit 发布脚本：

```bash
WECHAT_APP_ID="你的AppID" \
WECHAT_APP_SECRET="你的AppSecret" \
node /Users/i/.openclaw/skills/wechat-toolkit/scripts/publisher/publish.js /path/to/article.md
```

执行成功后会返回草稿 `Media ID`，这就是进入公众号后台草稿箱的凭证。

## 一个稳定的工作流（推荐）

我现在固定用这条链路：

1. 在本地写 `posts/dayXXX-xxx.md`
2. 生成封面图并写入 frontmatter
3. 先发公众号草稿（拿到 Media ID）
4. 同步转换为博客文章（Jekyll frontmatter）
5. 提交并推送 GitHub Pages

这样做的好处是：公众号与博客内容保持一致，且可以追溯每次修改。

## 常见问题与处理

### 1) `40164 invalid ip`

原因：调用机器 IP 不在微信白名单。

处理：

- 查当前公网 IP
- 加到公众号后台白名单
- 重新执行发布命令

### 2) 缺少 `title` 或 `cover`

原因：frontmatter 不完整。

处理：补齐字段后重发。

### 3) 图片路径不稳定

原因：相对路径在发布工具链里可能解析失败。

处理：改成绝对路径。

## Day 100 小结

QClaw 这套方式最核心的价值，不是“自动化本身”，而是把发布流程工程化：

- 有输入规范（Markdown + frontmatter）
- 有固定执行命令
- 有可诊断的错误输出
- 有可复用的内容资产

当你把发布当成工程问题，而不是手工操作问题，效率会非常明显地提升。

下一步，我会继续把“封面生成 + 标题备选 + 双端发布”进一步模板化，让 Day 系列可以更快连载。
