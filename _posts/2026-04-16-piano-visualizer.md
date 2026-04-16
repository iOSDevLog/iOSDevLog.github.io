---
layout: post
title: "Day 101: Piano Visualizer / 钢琴可视化工具"
author: "iOSDevLog"
date: 2026-04-16 20:00:00 +0800
category: ["AI", "Open Source"]
tags: ["piano", "visualizer", "synthesia", "midi", "pdf", "music"]
---

# Piano Visualizer / 钢琴可视化工具

A Synthesia-like piano keyboard visualization software with MIDI playback, audio synthesis, PDF sheet music display, and manual keyboard input.

一个类似 Synthesia 的钢琴键盘可视化软件，支持 MIDI 播放、音频合成、PDF 乐谱显示和手动键盘输入。

## Screenshots

![AI_Piano](/assets/images/ai-piano/AI_Piano.png)

![AI_Piano_Fullscreen](/assets/images/ai-piano/AI_Piano_Fullscreen.png)

## Features / 功能特性

- 88-key piano keyboard visualization / 88键钢琴键盘可视化
- MIDI file playback with real-time note highlighting / MIDI 文件播放与实时音符高亮
- Falling notes visualization (like Synthesia) / 下落音符可视化（类似 Synthesia）
- Audio synthesis with polyphonic sound output / 多音复音音频合成
- PDF sheet music viewer / PDF 乐谱查看器
- Manual keyboard input - play piano with your computer keyboard / 手动键盘输入 - 用电脑键盘弹钢琴
- Keyboard labels showing which computer keys map to piano keys / 键盘标签显示电脑按键与钢琴键的映射
- Fullscreen support / 全屏支持
- Resizable window / 可调整窗口大小
- Drag and drop MIDI/PDF files / 拖放 MIDI/PDF 文件
- Help overlay (F1) / 帮助覆盖层（F1）
- Synchronized playback / 同步播放

## Dependencies / 依赖项

```bash
# Install dependencies (Ubuntu/Debian) / 安装依赖（Ubuntu/Debian）
sudo apt-get install libsdl2-dev libsdl2-image-dev libsdl2-ttf-dev librtmidi-dev poppler-utils
```

## Building / 编译

```bash
mkdir build && cd build
cmake ..
make
```

## Usage / 使用方法

```bash
# Play MIDI with falling notes visualization / 播放 MIDI 并显示下落音符
./piano_visualizer song.mid

# Play MIDI with PDF sheet music / 播放 MIDI 并显示 PDF 乐谱
./piano_visualizer song.mid sheet.pdf

# View PDF only and play manually with keyboard / 仅查看 PDF 并用键盘手动演奏
./piano_visualizer sheet.pdf
```

## Controls / 控制键

### MIDI Playback (when MIDI file is loaded) / MIDI 播放（加载 MIDI 文件时）
- **Space / 空格键**: Play/Pause MIDI / 播放/暂停 MIDI
- **Backspace / 退格键**: Stop MIDI / 停止 MIDI

### Manual Piano Playing / 手动钢琴演奏
You can play the piano manually using your computer keyboard:

您可以使用电脑键盘手动演奏钢琴：

**Lower octave (C3-C4) / 低八度（C3-C4）:**
- White keys / 白键: `Z X C V B N M`
- Black keys / 黑键: `S D G H J`

**Middle octave (C4-C5) / 中八度（C4-C5）:**
- White keys / 白键: `Q W E R T Y U I`
- Black keys / 黑键: `2 3 5 6 7`

## Source Code / 源代码

- GitHub: [https://github.com/iOSDevLog/AI_Piano](https://github.com/iOSDevLog/AI_Piano)

---
