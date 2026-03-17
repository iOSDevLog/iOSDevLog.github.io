---
layout: post
title: "Day 99: Git 提交的艺术"
author: iosdevlog
date: 2026-03-17 23:46:00 +0800
description: "Day 99：如何把 Git 提交做成可读、可回滚、可协作的工程资产。"
category: AI
tags: [Git, 工程实践, 版本控制, 协作, 开发效率]
---

![Day 99 Git 提交的艺术](/assets/images/day99-git-commit-art.png)

# Day 99: Git 提交的艺术

很多团队把 Git 当成“文件快照工具”，但高手把它当成“可读的协作语言”。

一次好提交，不只是把代码塞进仓库，而是给未来的你、同事、评审者留下一条清晰的思路线索。

## 1) 把提交当作“最小可理解单元”

核心原则：**一个提交只做一件事**。

- ✅ 好例子：`fix(auth): handle expired token refresh`
- ❌ 坏例子：改了登录、顺手重构了样式、再修了一个埋点

为什么？

- 回滚更安全（只撤一件事）
- 评审更高效（关注点单一）
- `git bisect` 更容易定位问题

## 2) 提交信息要“说动机”，不只“说动作”

动作谁都看得见（代码 diff 就是动作），难的是上下文。

建议格式：

```text
<type>(scope): <summary>

<why>
<what>
<impact>
```

示例：

```text
fix(payment): avoid duplicate callback handling

Third-party gateway may retry callback within 3s.
Add idempotency check by order_id + callback_id.
Prevents duplicate order status updates.
```

一句话总结：**让别人不用问你“你为什么这么改”**。

## 3) 先整理再提交：`git add -p`

不要一把梭 `git add .`。真正的“提交艺术”在暂存区。

常用组合：

- `git status`：先看脏改动
- `git add -p`：按 hunk 精准挑选
- `git diff --staged`：提交前做最后审阅

这一步能把“顺手改动”挡在提交之外。

## 4) 把“重构”和“行为变化”拆开

最容易引发评审噪音的，就是两者混在一起：

- 文件重排、命名重构、格式化（无行为变化）
- 业务逻辑调整（有行为变化）

请分成两个提交：

1. `refactor:` 纯重构
2. `feat/fix:` 功能或缺陷修复

这样评审可以快速聚焦真正风险。

## 5) 避免“巨石提交”

超过 500 行的单提交，几乎注定难评审。

可执行做法：

- 按功能点切分
- 先提交基础设施，再提交业务逻辑
- UI 与后端改动分层提交（如果可独立验证）

不是行数越少越好，而是**每个提交都可被独立理解与验证**。

## 6) 写给未来的历史：善用 amend 与 rebase

本地分支（未共享）可积极整理历史：

- `git commit --amend`：修正刚刚那次提交
- `git rebase -i`：合并碎片提交、重写提交信息

目标不是“炫技”，而是让主分支历史更干净。

> 已推送到公共分支的提交，避免随意改写历史。

## 7) 推荐一套轻量约定（可直接落地）

团队可以从这套最小规范开始：

- 类型：`feat` / `fix` / `refactor` / `docs` / `test` / `chore`
- 每次提交只做一件事
- 提交信息首行不超过 72 字符
- 重要提交写 2~4 行 body（why/impact）

执行一周，仓库可读性会明显提升。

## 常见反例（你可能正在做）

- `update`、`修改`、`final-final` 这类无信息提交信息
- 一次提交里混合重构 + 新功能 + bug 修复
- 提交前不看 staged diff，导致临时调试代码入库

## 结语

Git 提交的本质，是工程沟通。

**代码是写给机器执行的，提交历史是写给人类理解的。**

从今天开始，把“能跑”升级成“可协作、可追溯、可维护”。

你会发现，团队效率和代码质量会一起上来。
