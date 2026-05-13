---
layout: post
title: "Day 104: 跨平台按键监控工具 - 在桌面半透明悬浮窗中实时显示键盘输入，不同类型按键用不同颜色高亮显示"
author: iosdevlog
date: 2026-05-13 00:00:00 +0800
category: [AI, Tools]
tags: [ToastKeys, Python, tkinter, pynput, 按键监控, 跨平台]
---

# ToastKeys - 跨平台按键监控工具

![ToastKeys Logo](https://img.shields.io/badge/ToastKeys-v1.0-blue)
![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey)
![Python](https://img.shields.io/badge/python-3.7+-green)
![License](https://img.shields.io/badge/license-MIT-orange)

一个简洁优雅的跨平台按键监控工具，在桌面半透明悬浮窗中实时显示键盘输入，并用不同颜色高亮显示不同类型的按键。

---

## 📸 效果展示

### 主界面
悬浮窗默认显示在屏幕中下方，半透明黑色背景，实时显示当前按键。

![Combo](https://raw.githubusercontent.com/build-your-own-x-with-ai/ToastKeys/main/Screenshots/Combo.png)

![Space](https://raw.githubusercontent.com/build-your-own-x-with-ai/ToastKeys/main/Screenshots/Space.png)

F1 Help

![F1](https://raw.githubusercontent.com/build-your-own-x-with-ai/ToastKeys/main/Screenshots/F1.png)

### 不同按键类型展示

**字母键** - 绿色大字体
```
显示效果：绿色 "A"
```

**数字键** - 青色大字体
```
显示效果：青色 "1"
```

**功能键** - 紫色
```
显示效果：紫色 "F1"
```

**控制键** - 橙色
```
显示效果：橙色 "Ctrl"
```

**组合键** - 黄色文字 + 红色背景
```
显示效果：红底黄字 "Ctrl + C"
```

### 帮助文档
按 F1 显示帮助文档，包含所有按键类型的彩色示例。

---

## 功能特性

- ✅ 跨平台支持（Windows、macOS、Linux）
- ✅ 半透明桌面悬浮窗
- ✅ 实时监控键盘输入
- ✅ 高亮显示复合按键（如 Ctrl+C、Cmd+V）
- ✅ 时间戳显示
- ✅ 窗口可拖动
- ✅ 始终置顶显示

## 安装

### 1. 安装依赖

```bash
pip install -r requirements.txt
```

### 2. 权限设置（macOS）

在 macOS 上，需要授予终端或 Python 辅助功能权限：

1. 打开 **系统设置** > **隐私与安全性** > **辅助功能**
2. 添加你的终端应用（Terminal.app 或 iTerm2）或 Python

## 使用方法

```bash
python toastkeys.py
```

或者添加执行权限后直接运行：

```bash
chmod +x toastkeys.py
./toastkeys.py
```

## 按键显示样式

不同类型的按键使用不同的颜色和样式：

- **字母键**：绿色大字体
- **数字键**：青色大字体
- **功能键**（F1-F12、ESC、Tab等）：紫色
- **控制键**（Ctrl、Alt、Shift、Cmd）：橙色
- **符号键**：白色
- **组合键**（如 Ctrl+C）：黄色文字 + 红色背景

## 界面特性

- 半透明黑色背景（透明度 90%）
- 窗口默认显示在屏幕中下方
- 只显示当前按键，不显示历史记录
- 鼠标悬停或获得焦点时显示边框，平时隐藏边框
- 可以拖动标题栏移动窗口位置
- 始终置顶，不会被其他窗口遮挡
- 按 F1 显示帮助文档

## 快捷键

- **F1**：显示帮助文档
- **点击右上角 ✕**：退出程序

## 注意事项

- 某些系统可能需要管理员权限才能监听键盘事件
- 在某些应用中（如密码输入框），按键监控可能受到限制
- 请遵守当地法律法规，仅在授权环境下使用

## 技术栈

- **tkinter**：跨平台 GUI 框架（Python 内置）
- **pynput**：跨平台键盘监听

## 作者

**AI开发日志**

## GitHub 仓库

[build-your-own-x-with-ai/ToastKeys](https://github.com/build-your-own-x-with-ai/ToastKeys)

## 许可证

MIT License

---

<div align="center">
Made with ❤️ by AI开发日志
</div>
