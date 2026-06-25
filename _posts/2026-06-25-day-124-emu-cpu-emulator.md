---
layout: post
title: "Day 124: EMU - 多架构 CPU 模拟器"
date: 2026-06-25 23:58:00 +0800
categories: Build_Your_Own_X
---

# EMU - 多架构 CPU 模拟器

一个模块化、可扩展的 CPU 模拟器框架，支持多种 CPU 架构和外设设备。

## 项目特性

### 已实现的 CPU 架构

#### 1. RISC-V (RV32I)
- **完整的 RV32I 基础指令集** (47 条指令)
- 支持所有算术、逻辑、内存访问、控制流指令
- CSR (控制状态寄存器) 支持
- 系统调用 (ECALL, EBREAK)
- 内存屏障 (FENCE)

#### 2. MCS-51/8051
- **经典 8051 微控制器架构**
- 8 位累加器和 B 寄存器
- 程序状态字 (PSW) - 进位、辅助进位、溢出、奇偶校验
- 128 字节内部 RAM
- 128 字节特殊功能寄存器 (SFR)
- 16 位数据指针 (DPTR)
- 栈操作 (PUSH/POP)
- 寄存器组选择 (4 组 × 8 寄存器)

### 核心系统

- **内存总线系统**: 支持 RAM 和 MMIO 设备的统一地址空间
- **CPU 抽象接口**: 易于添加新的 CPU 架构
- **设备框架**: 标准化的设备接口 (read/write/tick)
- **中断控制器**: 可配置优先级的中断管理

### 外设设备

#### UART (通用异步收发器)
- 16 字节 TX/RX FIFO
- 状态寄存器 (TX ready/empty, RX ready/full)
- 控制寄存器 (TX/RX enable, 中断使能)
- 波特率除数寄存器
- 中断生成 (TX/RX 事件)
- 输出回调机制

**寄存器映射:**
- 0x00: 数据寄存器 (RX/TX)
- 0x04: 状态寄存器
- 0x08: 控制寄存器
- 0x0C: 波特率除数

#### 定时器
- 32 位计数器，可配置预分频器
- 比较寄存器 (周期中断)
- 自动重置模式 (周期定时器)
- 单次触发模式 (超时事件)
- 比较匹配中断
- 手动计数器设置/读取

**寄存器映射:**
- 0x00: 控制寄存器 (enable, IRQ, auto-reset, one-shot)
- 0x04: 状态寄存器 (running, match, overflow)
- 0x08: 计数器值
- 0x0C: 比较值
- 0x10: 预分频器除数

## 测试覆盖

- **9 个测试套件**, 100% 通过
- 完整的单元测试覆盖所有组件
- 每个 CPU 架构都有专门的测试套件
- 设备功能的全面测试

## 示例应用

### RISC-V 演示程序
位于 `targets/freertos-riscv/demo.c`

功能演示:
- CPU 初始化和复位
- 内存映射 I/O 访问
- UART 设备配置和数据传输
- 程序执行和设备交互

**运行演示:**
```bash
cd build
./targets/freertos-riscv/riscv_demo
```

**输出:**
```
=== RISC-V Emulator Demo ===
Simple program: Print 'Hi' via UART

Starting execution at 0x80000000
Output from UART:
----------------------------------------
Hi

----------------------------------------
Execution completed
```

## 构建说明

### 依赖
- CMake 3.12+
- C11 编译器 (GCC/Clang)

### 编译
```bash
mkdir build
cd build
cmake ..
make -j4
```

### 运行测试
```bash
make test
```

## 项目结构

```
EMU/
├── include/
│   ├── emu/           # 核心框架头文件
│   │   ├── cpu.h      # CPU 抽象接口
│   │   ├── memory.h   # 内存总线
│   │   ├── device.h   # 设备接口
│   │   ├── interrupt.h
│   │   └── machine.h
│   ├── cpu/           # CPU 架构头文件
│   │   ├── riscv.h
│   │   └── mcs51.h
│   └── devices/       # 设备头文件
│       ├── uart.h
│       └── timer.h
├── src/
│   ├── core/          # 核心实现
│   ├── cpu/           # CPU 实现
│   │   ├── riscv/
│   │   └── mcs51/
│   └── devices/       # 设备实现
├── tests/
│   └── unit/          # 单元测试
├── targets/           # 示例应用
│   └── freertos-riscv/
└── CMakeLists.txt
```

## 扩展性

### 添加新的 CPU 架构

1. 在 `include/cpu/` 创建头文件
2. 实现 `emu_cpu_ops_t` 接口
3. 在 `src/cpu/` 实现 CPU 逻辑
4. 调用 `emu_cpu_register()` 注册

### 添加新设备

1. 在 `include/devices/` 创建头文件
2. 实现 `emu_device_t` 接口 (read/write/tick)
3. 在 `src/devices/` 实现设备逻辑
4. 通过 `emu_memory_bus_add_region()` 映射到地址空间

## 内存映射示例 (RISC-V 演示)

| 基地址     | 大小 | 设备  |
|-----------|------|-------|
| 0x80000000 | 64KB | RAM   |
| 0x10000000 | 4KB  | UART  |
| 0x10001000 | 4KB  | Timer |

## 已完成的任务

✅ **RISC-V RV32I 完整指令集** - 所有基础指令，47 条  
✅ **UART 设备** - 串口通信，带 FIFO 和中断  
✅ **定时器设备** - RTOS 时钟源，多种模式  
✅ **RISC-V 演示程序** - 可运行的示例应用  
✅ **MCS-51/8051 架构** - 经典 8 位微控制器  

## 待实现功能

- **GDB 远程调试支持** - GDB RSP 协议实现
- **更多 8051 指令** - 扩展指令集覆盖
- **更多外设** - GPIO, SPI, I2C, ADC
- **NES/6502 架构** - 第三个 CPU 架构
- **完整的 FreeRTOS 移植** - 任务调度和 RTOS API

## 技术亮点

1. **架构抽象清晰**: CPU、内存、设备完全解耦
2. **高度可扩展**: 通过注册机制轻松添加新组件
3. **内存映射 I/O**: 统一的地址空间，设备访问透明
4. **测试驱动**: 所有功能都有单元测试保证
5. **实用性**: 可以运行真实的二进制程序

## 性能特点

- 指令级模拟，准确度高
- 设备 tick 机制支持周期性操作
- 高效的内存访问（最近访问缓存）
- 适合教学、原型开发、固件测试

## 使用场景

- **嵌入式系统开发**: 在 PC 上测试固件
- **教学**: 学习 CPU 架构和汇编语言
- **逆向工程**: 分析未知固件
- **原型验证**: 在硬件可用前验证算法
- **自动化测试**: CI/CD 中的固件测试

## 许可证

MIT License

## 贡献者

- Initial implementation by Claude Sonnet 4.6
- Project architecture and design

---

**最后更新**: 2026-06-20  
**版本**: 0.1.0  
**状态**: 活跃开发中
