---
layout: post
title: "101：使用小米 Mimo V2 Pro 开发 100 个 Javascript 小游戏"
date: 2026-03-26
author: iOSDevLog
categories: [JavaScript, Game Development, AI]
tags: [JavaScript, HTML5, Game, Mimo, OpenClaw]
---

## 🎮 项目介绍

一个包含 **100 个极简 JavaScript 小游戏** 的集合！每个游戏都是独立的 HTML 文件，可以直接在浏览器中运行，无需安装任何依赖。

本项目使用 **小米 Mimo V2 Pro** 辅助开发，展示了 AI 辅助编程的强大能力。

![游戏主页面](/assets/images/100-games/index.png)

## 🎯 项目特色

- **100个独立游戏** - 每个游戏都是完整的 HTML 文件
- **即开即玩** - 无需安装，双击即可运行
- **响应式设计** - 支持桌面端和移动端
- **本地存储** - 自动保存最高分记录
- **纯原生实现** - 无框架依赖，适合学习

## 🧩 三大游戏分类

### 益智解谜类 (35个)

2048、数独、扫雷、记忆翻牌、汉诺塔、华容道、迷宫生成、路径规划等经典益智游戏。

![2048 游戏](/assets/images/100-games/game-004.png)

### 纸牌棋盘类 (35个)

五子棋、黑白棋、国际象棋、中国象棋、扑克接龙、老虎机、骰子游戏等棋盘游戏。

![贪吃蛇](/assets/images/100-games/game-071.png)

### 动作射击类 (30个)

贪吃蛇、俄罗斯方块、打砖块、太空侵略者、飞机大战、吃豆人等动作游戏。

![俄罗斯方块](/assets/images/100-games/game-072.png)

![打砖块](/assets/images/100-games/game-073.png)

## 🚀 快速开始

### 方法一：直接运行

1. 下载或克隆本项目
2. 双击 `index.html` 文件
3. 选择游戏开始玩耍

### 方法二：本地服务器（推荐）

```bash
# 进入项目目录
cd 100-javascript-games

# 启动本地服务器
python3 -m http.server 8000

# 打开浏览器访问 http://localhost:8000
```

### 方法三：在线演示

🔗 [GitHub Pages 在线演示](https://build-your-own-x-with-ai.github.io/mimo-v2-pro-100-games/)

## 🎮 完整游戏列表

### 🧩 益智解谜类 (35个)

| 编号 | 游戏名称 | 说明 | 难度 |
|------|----------|------|------|
| 001 | 点击计数器 | 5秒内点击最多次数 | ⭐ |
| 002 | 猜数字 | 1-100猜数字 | ⭐ |
| 003 | 记忆翻牌 | 配对卡片 | ⭐⭐ |
| 004 | 2048 | 数字合并游戏 | ⭐⭐⭐ |
| 005 | 数独 | 简化版数独 | ⭐⭐⭐ |
| 006 | 滑块拼图 | 15拼图 | ⭐⭐ |
| 007 | 连连看 | 图案配对 | ⭐⭐ |
| 008 | 找不同 | 两图对比 | ⭐ |
| 009 | 汉诺塔 | 经典递归游戏 | ⭐⭐⭐ |
| 010 | 华容道 | 滑块解谜 | ⭐⭐⭐ |
| 013 | 扫雷 | 经典扫雷 | ⭐⭐⭐ |
| 014 | 迷宫生成 | 随机迷宫 | ⭐⭐ |

### ♟️ 纸牌棋盘类 (35个)

| 编号 | 游戏名称 | 说明 | 难度 |
|------|----------|------|------|
| 036 | 井字棋 | 经典Tic-Tac-Toe | ⭐ |
| 037 | 五子棋 | 连五子获胜 | ⭐⭐ |
| 038 | 四子棋 | 连四子获胜 | ⭐⭐ |
| 039 | 黑白棋 | Reversi | ⭐⭐ |
| 041 | 国际象棋 | 象棋简化版 | ⭐⭐⭐ |
| 043 | 扑克接龙 | Solitaire | ⭐⭐ |
| 047 | 老虎机 | 老虎机模拟 | ⭐ |

### 🎯 动作射击类 (30个)

| 编号 | 游戏名称 | 说明 | 难度 |
|------|----------|------|------|
| 071 | 贪吃蛇 | 经典贪吃蛇 | ⭐⭐ |
| 072 | 俄罗斯方块 | Tetris | ⭐⭐⭐ |
| 073 | 打砖块 | Breakout | ⭐⭐ |
| 074 | 太空侵略者 | Space Invaders | ⭐⭐⭐ |
| 075 | 飞机大战 | 飞机射击 | ⭐⭐ |
| 077 | 吃豆人 | Pac-Man简化版 | ⭐⭐ |
| 095 | 小行星 | Asteroids | ⭐⭐⭐ |
| 097 | 月球登陆 | Moon Landing | ⭐⭐⭐ |

## 🛠️ 技术栈

- **HTML5** - 页面结构
- **CSS3** - 样式和动画
- **JavaScript (ES6+)** - 游戏逻辑
- **Canvas API** - 图形渲染
- **LocalStorage** - 数据持久化

## 📱 浏览器支持

| 浏览器 | 最低版本 |
|--------|----------|
| Chrome | 60+ |
| Firefox | 55+ |
| Safari | 11+ |
| Edge | 79+ |
| Opera | 47+ |

## 🔗 相关链接

- [GitHub 仓库](https://github.com/build-your-own-x-with-ai/mimo-v2-pro-100-games)
- [在线演示](https://build-your-own-x-with-ai.github.io/mimo-v2-pro-100-games/)
- [问题反馈](https://github.com/build-your-own-x-with-ai/mimo-v2-pro-100-games/issues)

## 📄 许可证

MIT License

---

⭐ 如果这个项目对你有帮助，请给个 Star！
