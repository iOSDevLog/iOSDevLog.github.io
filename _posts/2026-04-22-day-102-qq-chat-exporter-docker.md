---
layout: post
title: "Day 102: macOS 通过 Docker 部署 QQ 聊天记录导出工具 qq-chat-exporter"
author: iosdevlog
date: 2026-04-22 22:30:00 +0800
category: [AI, DevOps]
tags: [Docker, QQ, NapCat, qq-chat-exporter, macOS, ChatGPT]
---

# Day 102: macOS 通过 Docker 部署 QQ 聊天记录导出工具 qq-chat-exporter 🎮

QQ 聊天记录导出工具 [qq-chat-exporter](https://github.com/shuakami/qq-chat-exporter) 只提供 Windows 原生包，macOS 用户想用就得折腾一番。本文记录我在 MacBook Pro M4 (Apple Silicon) 上通过 Docker 成功部署的完整过程。

![QQ_Export](/assets/images/AI/Day102/QQ_Export.png)

## 问题背景

- **qq-chat-exporter** 官方只有 Windows Release
- macOS 不在官方支持列表
- NapCat Docker 方案可以曲线救国
- 导出文件默认按 `friend_{uid}_{时间戳}.html` 命名，看不出是谁

## 解决方案

使用 `mlikiowa/napcat-docker` 镜像 + qq-chat-exporter 插件，通过 Docker 跑起一个 Linux QQ 实例。

## 详细步骤

### 环境确认

```bash
docker --version
# Docker Desktop 4.x / 28.x 均可用

docker --version
# Docker version 28.5.2

# Apple Silicon (ARM64) 需要额外安装 esbuild Linux 版
npm install @esbuild/linux-arm64@0.25.10
```

### 目录结构

```
~/qq-chat-exporter/
├── config/
│   └── plugins.json
├── plugins/
│   └── qq-chat-exporter/   # 插件本体
└── qce-v4-tool/           # Web UI 前端
    └── (静态文件)
```

### 插件目录创建

```bash
mkdir -p ~/qq-chat-exporter/{config,plugins,qce-v4-tool}

# 从 Release 包解压：
# 1. qq-chat-exporter 插件 -> plugins/qq-chat-exporter/
# 2. qce-v4-tool 静态文件 -> qce-v4-tool/

# Apple Silicon 需要额外步骤
cd plugins/qq-chat-exporter
npm install @esbuild/linux-arm64@0.25.10
```

### 配置文件

**config/plugins.json**：
```json
{
  "napcat-plugin-builtin": true,
  "qq-chat-exporter": true
}
```

### docker-compose.yml

```yaml
version: "3.8"
services:
  napcat:
    image: mlikiowa/napcat-docker:latest
    container_name: napcat
    ports:
      - "3000:3000"      # Web UI
      - "40653:40653"     # WebSocket
    volumes:
      - ./config:/app/napcat/config
      - ./plugins:/app/napcat/plugins
      - ./qce-v4-tool:/app/.qq-chat-exporter/qce-v4-tool
    restart: unless-stopped
```

### 启动容器

```bash
docker compose up -d
docker logs -f napcat
```

### QQ 登录

1. 访问 http://localhost:3000
2. 扫码登录 QQ
3. 登录成功后插件自动加载

### 获取访问令牌

```bash
docker exec napcat cat /app/.qq-chat-exporter/security.json
# 返回类似：#P4!tq8%^%KGColZJ84d!PoIo8Wg3q0I
```

### 导出聊天记录

用令牌访问 Web UI，选择好友/群聊，点击导出。

**导出结果**（88个文件）：
- 18 个好友聊天记录
- 70 个群聊记录
- HTML 格式，方便浏览

### 文件名处理（重要）

导出的文件名默认是 `friend_u_xxx_timestamp.html`，看不出是谁。需要从 HTML 内容中提取昵称再重命名：

```bash
cd /app/.qq-chat-exporter/exports

# 从 <title>聊天记录 - 昵称</title> 提取并重命名
for f in friend_u_*.html; do
  nick=$(grep -oP "(?<=聊天记录 - ).+(?=</title>)" "$f" | head -1)
  if [[ -n "$nick" ]]; then
    nick_safe=$(echo "$nick" | sed "s/[\/\\&|]/_/g")
    base=$(echo "$f" | sed -E "s/_[^_]+\.html$//")
    mv "$f" "${base}_${nick_safe}.html"
  fi
done
```

**重命名后效果**：

| 原文件名 | 重命名后 |
|---------|---------|
| `friend_u_xxx_20260422.html` | `friend_u_xxx_20260422_小武.html` |
| `group_1001220381_20260422.html` | `group_1001220381_20260422_GTOC.html` |
| `group_460952208_20260422.html` | `group_460952208_20260422_C_C++学习交流群.html` |

### 复制到本地

```bash
mkdir -p ~/qq-exports
docker cp napcat:/app/.qq-chat-exporter/exports/. ~/qq-exports/
```

## 技术细节

### 为什么选 NapCat？

[NapCat](https://github.com/NapNeko/NapCatQQ) 是一个轻量级 QQ 协议实现，支持 Docker 部署。相比其他方案：
- 配置简单
- 插件生态丰富
- Web UI 易用

### Apple Silicon 特殊处理

ARM64 架构需要额外的 esbuild 二进制：
```bash
cd plugins/qq-chat-exporter
npm install @esbuild/linux-arm64@0.25.10
```

否则会出现 `esbuild: Wrong architecture` 错误。

### 文件名加昵称

这是 **qq-chat-exporter** 的待实现功能。当前导出会话名只用于目录，不用于文件名。可以向作者提 Issue 或等后续版本支持。

## 截图预览

### 好友列表导出

| 好友 | 导出文件 |
|------|---------|
| 小武 | `friend_u_7OYKOZ2ZQsFEXP6Cg1y5Kg_20260422_小武.html` |

### 群聊导出

| 群名 | 导出文件 |
|------|---------|
| GTOC 格维开源社区 | `group_1001220381_20260422_GTOC.html` |
| AI墨水屏交流群 | `group_1026120682_20260422_AI墨水屏交流群.html` |
| TuyaOpen Framework技术交流 | `group_796221529_20260422_TuyaOpen Framework技术交流.html` |

![QQ_Chat](/assets/images/AI/Day102/QQ_Chat.png)

## 踩坑记录

1. **Apple Silicon 需要额外安装 esbuild**：不装的话插件加载会失败
2. **容器名冲突**：旧容器没删干净会导致启动失败，先 `docker rm -f napcat`
3. **特殊字符处理**：昵称含 `/` `|` `\` 时需要替换为 `_`，否则重命名失败

## 相关链接

- [qq-chat-exporter](https://github.com/shuakami/qq-chat-exporter)
- [NapCat](https://github.com/NapNeko/NapCatQQ)
- [napcat-docker](https://hub.docker.com/r/mlikiowa/napcat-docker)

## 总结

通过 Docker + NapCat，成功在 macOS 上运行了 QQ 聊天记录导出工具。虽然 qq-chat-exporter 官方不支持 macOS，但借助开源社区的插件生态，曲线完成了需求。

导出的 HTML 文件可以直接在浏览器打开，也可以用其他工具进一步处理（如转换为 PDF、导入数据库等）。

后续可以尝试：
- 批量导出所有聊天记录
- 定时自动备份
- 导出为 JSON 格式方便程序处理

![QClaw_Docker](/assets/images/AI/Day102/QClaw_Docker.png)

![QClaw](/assets/images/AI/Day102/QClaw.png)

---