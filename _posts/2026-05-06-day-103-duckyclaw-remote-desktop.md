---
layout: post
title: "Day 103: DuckyClaw 图鸦智能桌面搭子：远程桌面助手"
author: iosdevlog
date: 2026-05-06 00:00:00 +0800
category: [AI, IoT]
tags: [DuckyClaw, T5AIBoard, RemoteDesktop, MJPEG, WebSocket, TuyaOpen, 远程桌面]
---

# Day 103: DuckyClaw 图鸦智能桌面搭子：远程桌面助手 🖥️


## 视频

b站视频：<https://www.bilibili.com/video/BV1B1RJBREcn/>

将 T5 AIBoard 变身为智能远程桌面显示器！通过语音控制启动服务，实时投射 PC 屏幕到 480x854 LCD，支持触摸控制鼠标操作。基于 MJPEG 硬件解码和 WebSocket 通信，延迟低至 100ms。

![Remote Desktop Demo](/assets/images/AI/Day103/remote_desktop_demo.jpg)

## 功能亮点 ✨

- 📺 **实时屏幕投射**：PC 桌面画面实时传输到 T5 LCD 屏幕
- 🖱️ **触摸控制**：通过触摸屏控制电脑鼠标移动和点击
- 🎯 **硬件加速**：使用 T5 芯片的 MJPEG 硬件解码器
- 🗣️ **语音控制**：语音命令启动/停止远程桌面服务
- 📡 **WiFi 连接**：基于 WebSocket 协议的局域网通信
- ⚡ **低延迟**：端到端延迟 < 100ms

## 技术参数 📊

| 参数 | 规格 |
|------|------|
| 显示分辨率 | 480 x 854 像素 |
| 色彩深度 | RGB565 (16-bit) |
| 目标帧率 | 10-15 FPS |
| 视频编码 | MJPEG |
| 网络协议 | WebSocket (端口 18789) |
| 延迟 | < 100ms (局域网) |

## 快速开始 🚀

### 1. 启动 T5 远程桌面服务

**语音启动（推荐）：**

```
"你好涂鸦，打开远程桌面"
```

**串口命令：**

```bash
rd_start
```

### 2. 获取 T5 IP 地址

**语音查询：**

```
"你好涂鸦，查询 WiFi 信息"
```

T5 会报告 IP 地址，例如：`192.168.3.117`

### 3. 启动 PC 客户端

```bash
cd pc_client
pip install -r requirements.txt
python main.py --ip 192.168.3.117 --fps 15 --quality 75
```

**参数说明：**
- `--ip`：T5 开发板的 IP 地址
- `--fps`：目标帧率（建议 10-15）
- `--quality`：JPEG 压缩质量（50-90，默认 75）

### 4. 开始使用

启动成功后：
- T5 LCD 屏幕显示您的电脑桌面
- 可以通过触摸屏控制鼠标移动和点击
- PC 终端显示实时传输统计信息

```
Stats: 74 frames sent, 0 failed, 14.8 FPS
```

## 系统架构 🏗️

```
┌─────────────────┐         WebSocket          ┌──────────────────┐
│   PC 客户端      │◄──────────────────────────►│  T5 AIBoard      │
│                 │                             │                  │
│ - 屏幕截图      │  ──► MJPEG 视频流 ──►      │ - MJPEG 解码     │
│ - 图像压缩      │                             │ - LCD 显示       │
│ - 鼠标/键盘控制 │  ◄── 触摸事件 ◄──          │ - 触摸输入       │
└─────────────────┘                             └──────────────────┘
```

### T5 端核心模块

- `remote_desktop.c`：主控制器，协调各模块
- `rd_video_decoder.c`：MJPEG 解码和 LCD 显示
- `rd_touch_handler.c`：触摸输入处理和坐标映射
- `rd_protocol.c`：WebSocket 消息解析
- `ws_server.c`：WebSocket 服务器（端口 18789）

### PC 端核心模块

- `main.py`：主程序入口和协调
- `screen_capture.py`：屏幕截图和 JPEG 编码
- `input_controller.py`：鼠标/键盘控制
- `websocket_client.py`：WebSocket 通信

## 通信协议 📡

### PC → T5 消息

**配置消息：**
```json
{
  "type": "config",
  "screen_width": 1920,
  "screen_height": 1080,
  "quality": 75,
  "fps": 15
}
```

**视频帧消息：**
```json
{
  "type": "video_frame",
  "width": 480,
  "height": 854,
  "frame_id": 12345,
  "data": "<base64-encoded-mjpeg>"
}
```

### T5 → PC 消息

**触摸事件消息：**
```json
{
  "type": "touch_event",
  "action": "down|move|up",
  "x": 240,
  "y": 427,
  "screen_x": 1920,
  "screen_y": 1080
}
```

**状态消息：**
```json
{
  "type": "status",
  "status": "started|stopped|configured"
}
```

## 性能优化 ⚡

### 低延迟模式（适合交互操作）

```bash
python main.py --ip 192.168.3.117 --fps 15 --quality 70
```

### 高质量模式（适合观看内容）

```bash
python main.py --ip 192.168.3.117 --fps 10 --quality 85
```

### 省带宽模式（适合弱网环境）

```bash
python main.py --ip 192.168.3.117 --fps 5 --quality 60
```

## 故障排查 🔧

### 问题 1：PC 客户端连接失败

**症状：** `Connection refused` 或 `Connection timeout`

**解决方案：**
1. 确认 T5 远程桌面服务已启动
2. 检查 IP 地址是否正确
3. 确认 PC 和 T5 在同一局域网
4. 检查防火墙是否阻止端口 18789
5. 尝试 ping T5 的 IP 地址

### 问题 2：画面卡顿或延迟高

**症状：** FPS 低于 5 或延迟超过 200ms

**解决方案：**
1. 降低帧率：`--fps 10`
2. 降低质量：`--quality 60`
3. 检查 WiFi 信号强度
4. 减少网络中其他设备的流量

### 问题 3：触摸控制不响应

**症状：** 触摸屏无法控制鼠标

**解决方案：**
1. 检查触摸屏是否正常工作
2. 确认配置中启用了触摸支持
3. 查看串口日志中的触摸事件
4. 重启远程桌面服务

## 技术实现细节 🔍

### MJPEG 硬件解码

使用 TuyaOpen 的 `tkl_jpeg_codec` 抽象层：

```c
// 获取 JPEG 信息
TKL_JPEG_CODEC_INFO_T jpeg_info = {0};
tkl_jpeg_codec_img_info_get(mjpeg_data, data_len, &jpeg_info);

// 解码到 RGB565
tkl_jpeg_codec_convert(mjpeg_data, rgb565_out, &jpeg_info, JPEG_DEC_OUT_RGB565);
```

### 触摸坐标映射

```c
// 将 480x854 触摸坐标映射到 PC 屏幕分辨率
pc_x = (touch_x * pc_screen_width) / 480;
pc_y = (touch_y * pc_screen_height) / 854;
```

### 动态缓冲区分配

```c
// 根据 base64 长度动态分配解码缓冲区
size_t max_decoded_len = (base64_len * 3) / 4 + 4;
frame->data = tal_psram_malloc(max_decoded_len);
```

### WebSocket 大帧支持

```c
// 动态分配 64KB 接收缓冲区（从 PSRAM）
client->rx_buf = tal_psram_malloc(65536);
client->rx_buf_size = 65536;
```

## 语音控制命令 🗣️

| 语音命令 | 功能 | 示例回复 |
|---------|------|---------|
| "打开远程桌面" | 启动服务 | "远程桌面服务已启动" |
| "关闭远程桌面" | 停止服务 | "远程桌面服务已停止" |
| "查询 WiFi 信息" | 获取 IP 地址 | "当前 IP 地址是 192.168.3.117" |
| "远程桌面状态" | 查询运行状态 | "远程桌面正在运行" |

## 串口命令参考 💻

```bash
# 启动远程桌面服务
rd_start

# 停止远程桌面服务
rd_stop

# 查询服务状态
rd_status

# 查询 WiFi 连接信息
wifi_info
```

## 开发者指南 👨‍💻

### 编译固件

```bash
# 初始化环境
cd TuyaOpen && . ./export.sh && cd ..

# 选择配置
cp config/TUYA_T5AI_BOARD_LCD_3.5_CAMERA.config app_default.config

# 编译
cd TuyaOpen && python3 tos.py build

# 烧录
python3 tos.py flash

# 监控日志
python3 tos.py monitor
```

### 关键技术点

1. **内存优化**：使用 PSRAM 存储大缓冲区，避免 RAM 溢出
2. **双缓冲显示**：避免画面撕裂，提供流畅体验
3. **动态分配**：根据实际帧大小分配解码缓冲区
4. **硬件加速**：利用 T5 芯片的 MJPEG 解码器
5. **协议设计**：JSON over WebSocket，易于扩展

## 未来计划 🚀

- [ ] 支持 H.264 编码（更高压缩率）
- [ ] 多点触控手势（双指缩放、滚动）
- [ ] 音频传输
- [ ] 文件拖放传输
- [ ] 多客户端支持
- [ ] 互联网远程访问
- [ ] 会话录制功能

## 常见问题 FAQ ❓

**Q：支持哪些操作系统？**

A：PC 端支持 Windows、macOS 和 Linux。T5 端运行 TuyaOpen 固件。

**Q：可以同时连接多个 PC 吗？**

A：当前版本仅支持单个 PC 连接。多客户端支持在未来版本中实现。

**Q：触摸屏支持多点触控吗？**

A：当前版本仅支持单点触控。多点触控手势在未来版本中实现。

**Q：可以通过互联网远程连接吗？**

A：当前版本仅支持局域网连接。互联网远程访问需要配置端口转发或 VPN。

**Q：延迟有多少？**

A：在良好的局域网环境下，端到端延迟通常在 50-100ms 之间。

## 项目地址 📦

- **GitHub**: [DuckyClaw_RemoteDesktop](hhttps://github.com/jiaxianhua/DuckyClaw_RemoteDesktop)
- **完整文档**: [远程桌面使用指南](https://github.com/jiaxianhua/DuckyClaw_RemoteDesktop/blob/master/docs/远程桌面使用指南.md)

## 致谢 🙏

感谢以下开源项目：

- **TuyaOpen SDK**：提供底层硬件抽象
- **mss**：跨平台屏幕截图
- **Pillow**：图像处理
- **websockets**：WebSocket 通信
- **pynput**：输入设备控制

---

**更新日期：** 2026年5月6日  
**版本：** v1.0.0  
**适用固件：** DuckyClaw_RemoteDesktop v1.0.0+

## 总结 📝

通过 T5 AIBoard 的远程桌面功能，我们实现了：

1. ✅ 实时屏幕投射（10-15 FPS）
2. ✅ 触摸控制鼠标
3. ✅ 语音启动/停止服务
4. ✅ 硬件 MJPEG 解码
5. ✅ 低延迟通信（< 100ms）

这个功能展示了 T5 AIBoard 作为智能桌面搭子的潜力，未来还将支持更多高级特性！

#DuckyClaw #T5AIBoard #RemoteDesktop #IoT #TuyaOpen #智能硬件
