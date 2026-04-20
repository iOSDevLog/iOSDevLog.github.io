---
layout: post
title: "DuckyClaw 端云硬件-智造桌面智能小车搭子"
author: "iOSDevLog"
date: 2026-04-21 00:00:00 +0800
category: ["IoT", "Open Source", "AI"]
tags: ["DuckyClaw", "TuyaT5AIBoard", "ESP32", "语音控制", "智能小车", "MCP"]
---

# DuckyClaw 端云硬件-智造桌面智能小车搭子

## 项目简介

本项目实现了使用 **TuyaT5AIBoard** 开发板通过语音命令控制 ESP32 智能小车。用户可以通过自然语言与 AI 助手对话，AI 助手会理解用户意图并发送 HTTP 命令到小车，实现前进、后退、转向等操作。

### 核心特性

- ✅ **语音控制**：通过自然语言控制小车（"小车前进1000ms"）
- ✅ **AI 理解**：智能理解复杂指令（"小车先前进100，然后左转90，再前进50"）
- ✅ **实时反馈**：AI 语音播报执行结果
- ✅ **灵活配置**：支持动态设置小车 IP 地址
- ✅ **命令序列**：支持执行多个连续动作

### 技术栈

- **硬件**：TuyaT5AIBoard (带 3.5 寸 LCD 屏幕)
- **小车**：ESP32 开发板 + 电机驱动
- **AI 框架**：DuckyClaw (基于 TuyaOpen SDK)
- **通信协议**：HTTP/JSON
- **AI 模型**：云端大语言模型

---

## 系统架构图

```
用户语音命令 → TuyaT5AIBoard (DuckyClaw) → AI Agent (云端大模型) → MCP Tool 调用 → car_command (HTTP Client) → ESP32 小车 (WebServer) → 电机控制
```

---

## 硬件准备

### 1. TuyaT5AIBoard 开发板

- 型号：TuyaT5AIBoard
- 屏幕：3.5 寸 LCD
- 网络：WiFi 连接
- 音频：麦克风 + 扬声器

### 2. ESP32 智能小车

- ESP32 开发板（ESP32-S3 推荐）
- 电机驱动模块（L298N 或 TB6612）
- 4 个直流电机
- 电池供电系统
- 车体底盘

---

## 快速开始

### 步骤 1: 准备 ESP32 小车

确保你的 ESP32 小车已经烧录了 WebServer 程序，支持以下 API：

**单个命令接口**：
```bash
POST http://192.168.3.115/command
Content-Type: application/json

{"action": "forward", "value": 1000}
```

**命令序列接口**：
```bash
POST http://192.168.3.115/sequence
Content-Type: application/json

[
  {"action": "forward", "value": 100},
  {"action": "rotate_left", "value": 90},
  {"action": "forward", "value": 50}
]
```

### 步骤 2: 编译 DuckyClaw

```bash
# 进入 TuyaOpen 目录并初始化环境
cd TuyaOpen
source ./export.sh
cd ..

# 选择 TuyaT5AIBoard 配置
cp config/TUYA_T5AI_BOARD_LCD_3.5_CAMERA.config app_default.config

# 编译项目
cd TuyaOpen
python3 tos.py build

# 烧录到开发板
python3 tos.py flash
```

### 步骤 3: 启动并配置小车 IP

1. 启动 TuyaT5AIBoard，等待连接到云端
2. 对着麦克风说："小车IP为192.168.3.115"
3. AI 会确认："Car IP address set to: 192.168.3.115"

### 步骤 4: 开始控制小车

现在你可以通过语音控制小车了：

- "小车前进1000毫秒"
- "小车后退500"
- "小车左转90度"
- "小车停止"

---

## 功能说明

### 支持的命令

| 命令示例 | 动作 | 参数说明 |
|---------|------|---------|
| "小车前进1000ms" | 前进 | 持续时间（毫秒） |
| "小车后退500" | 后退 | 持续时间（毫秒） |
| "小车左平移200" | 左平移 | 持续时间（毫秒） |
| "小车右平移200" | 右平移 | 持续时间（毫秒） |
| "小车停止" | 停止 | 无 |

### 旋转命令

⚠️ **重要提示**：由于硬件接线原因，左转和右转的命令是反向的：

| 用户说 | AI 发送的命令 | 实际动作 |
|-------|-------------|---------|
| "小车左转90" | `rotate_right` | 左转 |
| "小车右转90" | `rotate_left` | 右转 |

AI 会自动处理这个映射，用户只需要说"左转"或"右转"即可。

### 复杂命令序列

AI 可以理解复杂的连续动作：

```
用户："小车先前进100毫秒，然后左转90度，再前进50毫秒"
```

AI 会自动拆解为命令序列，实现复杂的动作组合。

---

## 进阶使用

### 查看详细日志

```bash
tail -f monitor.log | grep car_control
```

### 自定义 Skill

修改 `skills/skill_loader.c` 中的 `BUILTIN_CAR_CONTROL` 来自定义 AI 的行为。

### 使用命令行测试

```bash
# 测试单个命令
curl -X POST http://192.168.3.115/command \
  -H "Content-Type: application/json" \
  -d '{"action":"forward","value":1000}'
```

---

## 故障排查

### 问题 1: "小车没有响应"
- 检查当前配置的 IP：对 AI 说 "小车当前IP是多少"
- 重新设置正确的 IP：对 AI 说 "小车IP为192.168.3.115"
- 测试网络连通性：`ping 192.168.3.115`

### 问题 2: "左转和右转反了"
这是正常的！由于硬件接线原因，代码中已经做了映射。

### 问题 3: "HTTP 请求超时"
- 检查小车的 WebServer 是否正常运行
- 检查防火墙是否阻止了连接
- 检查 WiFi 信号是否稳定

---

## 技术原理

### SKILL vs MCP Tool

- **SKILL（技能文档）**：存储在 `skills/skill_loader.c` 中，告诉 AI 什么时候、如何使用工具
- **MCP Tool（工具）**：实现在 `tools/tool_car_control.c` 中，发送 HTTP 请求到 ESP32

### HTTP 通信协议

DuckyClaw 使用 TuyaOpen 的 `http_client_interface` 发送 HTTP 请求。

---

## 源代码

- **GitHub**: [https://github.com/tuya/DuckyClaw](https://github.com/tuya/DuckyClaw)
- **详细教程**: [docs/TUTORIAL_CAR_CONTROL_ZH.md](https://github.com/tuya/DuckyClaw/blob/main/docs/TUTORIAL_CAR_CONTROL_ZH.md)

---
