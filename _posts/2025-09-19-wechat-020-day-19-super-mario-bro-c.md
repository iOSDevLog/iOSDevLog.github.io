---
layout: post
title: "Day 19: 超级玛丽兄弟 Super Mario Bro C++ 实现"
author: iosdevlog
date: 2025-09-19 23:57:53 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247485809&idx=1&sn=8e195dc616b400d0065cd0fa9d384dbd&chksm=f95c92f6ce2b1be0f9d84036babbe2cba9ba447c42bd4c6d2c47023f5c505dd7a260da215592#rd

超级玛丽兄弟 Super Mario Bro C++ 实现

This is a C++ port of the Python/Pygame Super Mario Bros Level 1-1 game using SDL2.

这是基于 SDL2 库，将《超级马里奥兄弟》1-1 关卡的 Python/Pygame 版本移植到 C++ 的实现。

cursor-agent 实现，还有 Bug。

Screenshots

游戏截图

（注：此处为游戏启动界面截图，路径为项目内 Screenshots/start.png）

Features

游戏特性

Complete recreation of Super Mario Bros Level 1-1

完整还原《超级马里奥兄弟》1-1 关卡

Mario with all states (small, big, fire)

马里奥包含全状态（小体型、大体型、火焰形态）

Enemies (Goombas, Koopas)

包含敌人（板栗仔、乌龟）

Interactive objects (bricks, coin boxes, coins, powerups)

包含可交互物体（砖块、金币箱、金币、强化道具）

Physics system with gravity and collision detection

带有重力和碰撞检测的物理系统

Sound effects and music

音效与背景音乐

Smooth camera following

流畅的镜头跟随效果

All original graphics and sounds

全部采用原版游戏的图像与音效资源

Dependencies

依赖环境

SDL2（基础图形 / 输入 / 音频库）

SDL2_image（图像加载库）

SDL2_mixer（音频混音库）

SDL2_ttf（字体渲染库）

CMake 3.16 或更高版本（构建工具）

兼容 C++17 标准的编译器（如 GCC、Clang、MSVC）

Building

环境搭建

Ubuntu/Debian

（适用于 Ubuntu、Debian 等 Debian 系 Linux 发行版）

bash

sudoapt-getinstall libsdl2-dev libsdl2-image-dev libsdl2-mixer-dev libsdl2-ttf-dev cmake build-essential

Fedora/RHEL

（适用于 Fedora、RHEL 等红帽系 Linux 发行版）

bash

sudo dnf install SDL2-devel SDL2_image-devel SDL2_mixer-devel SDL2_ttf-devel cmake gcc-c++

macOS

（使用 Homebrew 包管理器安装依赖）

bash

brew install sdl2 sdl2_image sdl2_mixer sdl2_ttf cmake

Windows

（Windows 系统需手动安装）

下载 SDL2 及其扩展库（SDL2_image、SDL2_mixer、SDL2_ttf）的开发版本：SDL 官方下载页

安装 CMake：CMake 官方下载页

配置编译器（如 MinGW 或 Visual Studio），确保依赖库的路径被正确识别

Compilation

编译步骤

1. 创建 build 目录（用于存放编译生成的文件）

mkdir build

# 2. 进入 build 目录

cd build

# 3. 用 CMake 生成构建文件（Makefile 或 Visual Studio 工程等）

cmake ..

# 4. 执行编译（根据系统自动选择编译工具，如 make、ninja 等）

make

Running

运行游戏

编译完成后，在 build 目录下执行生成的可执行文件：

./MarioCPP

Controls

操作按键

Arrow Keys（方向键）

- Move left/right（左右移动）

A 键

- Jump（跳跃）

S 键

- Run/Shoot fireball (when fire Mario)（奔跑 / 发射火球，仅火焰形态马里奥可用）

Down Arrow（下方向键）

- Crouch（下蹲）

ESC 键

- Quit（退出游戏）

Project Structure

项目结构

Mario-CPP/

├── src/                 # 源代码文件目录

│   ├── main.cpp         # 程序入口文件（主函数所在）

│   ├── game.cpp         # 游戏循环与全局管理逻辑

│   ├── level.cpp        # 关卡系统（关卡加载、地图管理等）

│   ├── mario.cpp        # 马里奥角色逻辑（状态、动作、碰撞等）

│   ├── sprite.cpp       # 精灵基类（所有可渲染对象的父类）

│   ├── game_objects.cpp # 游戏对象（敌人、道具、场景元素等）

│   └── sdl_wrapper.cpp  # SDL 封装类（简化 SDL 接口调用）

├── include/             # 头文件目录

│   ├── game.h           # Game 类声明

│   ├── level.h          # Level 类声明

│   ├── mario.h          # Mario 类声明

│   ├── sprite.h         # Sprite 基类声明

│   ├── game_objects.h   # 游戏对象类声明

│   ├── sdl_wrapper.h    # SDL 封装类声明

│   └── constants.h      # 游戏常量定义（如速度、尺寸、颜色等）

├── resources/           # 游戏资源目录

│   ├── graphics/        # 图像资源（精灵图、背景图等）

│   ├── music/           # 背景音乐文件

│   ├── sound/           # 音效文件（跳跃、收集金币等）

│   └── fonts/           # 字体文件（用于显示文字信息）

├── CMakeLists.txt       # CMake 构建配置文件（指定编译规则、依赖等）

└── README.md           # 项目说明文档（本文档）

Game Features

核心游戏特性详情

Mario States

马里奥状态系统

Small Mario (default) - 小体型马里奥（默认初始状态，受攻击即死亡）

Big Mario (after mushroom) - 大体型马里奥（吃蘑菇后变身，受攻击变回小体型）

Fire Mario (after fire flower) - 火焰形态马里奥（吃火焰花后变身，可发射火球攻击敌人）

Invincible states with color cycling - 无敌状态（吃星星后触发，角色颜色循环闪烁，触碰敌人可直接消灭）

Enemies

敌人系统

Goombas that walk and can be stomped - 板栗仔（直线行走，被马里奥踩踏后消灭）

Koopas that turn into shells when stomped - 乌龟（直线行走，被踩踏后缩成壳，可被马里奥踢动攻击其他敌人）

Interactive Objects

可交互物体

Breakable bricks (some contain powerups) - 可破坏砖块（部分砖块内含强化道具，需马里奥头顶撞击）

Coin boxes (contain coins or powerups) - 金币箱（撞击后产出金币或道具，可重复撞击直至资源耗尽）

Coins that spin and can be collected - 可收集金币（旋转动画效果，收集后增加分数）

Powerups (mushrooms, fire flowers, stars) - 强化道具（蘑菇：变大；火焰花：变火焰形态；星星：无敌）

Physics

物理系统

Gravity system - 重力系统（所有角色和物体受重力影响，模拟下落与跳跃轨迹）

Collision detection - 碰撞检测（精确判断马里奥与敌人、道具、场景的碰撞关系）

Jump mechanics - 跳跃机制（支持二段跳、跳跃高度受按键时长影响等细节）

Running vs walking speeds - 行走 / 奔跑速度差异（按住 S 键时马里奥进入奔跑状态，移动速度提升）

Audio

音频系统

Background music - 背景音乐（随关卡进度切换，还原原版游戏音效风格）

Sound effects for jumps, coin collection, etc. - 场景音效（跳跃、收集金币、撞击砖块等操作的反馈音效）

Music state management - 音乐状态管理（暂停 / 继续、切换场景时自动切换音乐）

Technical Details

技术细节

60 FPS target frame rate - 目标帧率 60 帧 / 秒（保证游戏流畅运行）

Smooth camera following with parallax scrolling - 流畅的镜头跟随与视差滚动（背景层与前景层滚动速度不同，增强画面纵深感）

Efficient collision detection - 高效碰撞检测（采用轴对齐包围盒 AABB 算法，平衡精度与性能）

Memory management with smart pointers - 智能指针内存管理（使用 C++ 智能指针避免内存泄漏）

Modular design with clear separation of concerns - 模块化设计（功能按类拆分，职责清晰，便于维护与扩展）

Credits

致谢

Original Python/Pygame version by justinarmstrong

原版 Python/Pygame 版本由 justinarmstrong 开发

C++ SDL port maintains all original functionality and assets

C++ SDL 移植版本保留了原版的所有功能与资源

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTQEVVXhmOLbNKX1BibQbxXhiaaRicxDakibLAMT9TOkuzBFrXpn2kQEcs0OLPHSenqIYAiaEJdlIbjTYuQ/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)
