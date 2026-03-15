---
layout: post
title: "Day 97: 涂鸦 T5AI Board 运行 DuckyClaw，可以使用飞书与设备交互，播放网易云音乐"
author: iosdevlog
date: 2026-03-15 21:36:00 +0800
description: "Day 97：在涂鸦 T5AI Board 上运行 DuckyClaw，通过飞书与设备交互并播放网易云音乐。"
category: AI
tags: [AI, OpenClaw, DuckyClaw, Feishu, Tuya, T5AI-Board, NetEaseMusic]
---

## Day 97

跑通了 DuckyClaw 的飞书机器人，可以实现通过飞书消息对设备进行控制与交互，并播放网易云音乐。

涂鸦智能官方已经提供了源码：

- [DuckyClaw 源码](https://github.com/Tuya-Community/DuckyClaw)

## 操作步骤

### 配置环境

```bash
# 安装依赖
sudo apt-get install lcov cmake-curses-gui build-essential ninja-build wget git python3 python3-pip python3-venv libc6-i386 libsystemd-dev

# 克隆仓库

# 安装涂鸦 SDK
git config --global http.postBuffer 524288000
git clone https://github.com/tuya/DuckyClaw.git

# 激活构建环境
cd DuckyClaw
git submodule update --init
. ./TuyaOpen/export.sh
```

这时 *Ubuntu 24.04* 报错了：

```
i@i:~/Code/DuckyClaw$ . ./TuyaOpen/export.sh 
OPEN_SDK_ROOT = 
Current root = /home/i/Code/DuckyClaw
Script name: bash
Script path: /bin/bash
Project files check:
  ✗ Missing export.sh
  ✗ Missing requirements.txt
  ✗ Missing tos.py
Erorr: Can't export!
```

修改：`export.sh`

```diff
(.venv) i@i:~/Code/DuckyClaw/TuyaOpen$ git diff 
diff --git a/export.sh b/export.sh
index fcab3ee2..263e570f 100755
--- a/export.sh
+++ b/export.sh
@@ -11,7 +11,9 @@ fi
 
 # Function to find the project root directory
 pwd_dir="$(pwd)"
-script_dir=$(realpath $(dirname "$0"))
+# Determine the directory of this script. When sourced, $0 is the shell (e.g. /bin/bash),
+# so prefer BASH_SOURCE[0] when available.
+script_dir=$(realpath "$(dirname "${BASH_SOURCE[0]:-$0}")")
```

### 修改 `tuya_app_config.h` 文件

```diff
-#define TUYA_PRODUCT_ID "xxxxxxxxxxxxxxxx"
+#define TUYA_PRODUCT_ID "xxxxxxxxxxxxxxxx"
 #endif
 
 // https://platform.tuya.com/purchase/index?type=6
 #ifndef TUYA_OPENSDK_UUID
-#define TUYA_OPENSDK_UUID    "uuidxxxxxxxxxxxxxxxx"             // Please change the correct uuid
+#define TUYA_OPENSDK_UUID    "uuidxxxxxxxxxxxxxxxx"             // Please change the correct uuid
 #endif
 #ifndef TUYA_OPENSDK_AUTHKEY
-#define TUYA_OPENSDK_AUTHKEY "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" // Please change the correct authkey
+#define TUYA_OPENSDK_AUTHKEY "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" // Please change the correct authkey
```

## 创建飞书应用

第一步：登录飞书开放平台

访问 [飞书开放平台](https://open.feishu.cn/app/)，使用飞书账号登录。

点击 **创建应用**，填写应用信息。

第二步：创建企业自建应用

点击"创建企业自建应用"，填写名称（如"DuckyClaw"）和描述，点击"创建"。

第三步：获取应用凭证

进入"凭证与基础信息"，复制 App ID（格式 cli_xxx）和 App Secret，妥善保存。

第四步：启用机器人能力

进入"添加应用能力" → "机器人"，点击"添加"。

![bot](/assets/images/AI/Day97/bot.png)

> 必须先做这步：否则下一步导入权限时，消息相关权限无法开通。

第五步：配置权限

![permission](/assets/images/AI/Day97/permission.png)

进入"权限管理"，点击"批量导入"，粘贴下方 JSON：

```json
{
  "scopes": {
    "tenant": [
      "application:application:self_manage",
      "application:bot.menu:write",
      "cardkit:card:read",
      "cardkit:card:write",
      "contact:contact.base:readonly",
      "contact:user.employee_id:readonly",
      "docs:document.content:read",
      "docx:document:readonly",
      "event:ip_list",
      "im:chat",
      "im:chat.members:bot_access",
      "im:chat:read",
      "im:chat:update",
      "im:message",
      "im:message.group_at_msg:readonly",
      "im:message.group_msg",
      "im:message.p2p_msg:readonly",
      "im:message.pins:read",
      "im:message.pins:write_only",
      "im:message.reactions:read",
      "im:message.reactions:write_only",
      "im:message:readonly",
      "im:message:recall",
      "im:message:send_as_bot",
      "im:message:send_multi_users",
      "im:message:send_sys_msg",
      "im:message:update",
      "im:resource",
      "sheets:spreadsheet",
      "wiki:wiki:readonly"
    ],
    "user": [
      "base:app:copy",
      "base:app:create",
      "base:app:read",
      "base:app:update",
      "base:field:create",
      "base:field:delete",
      "base:field:read",
      "base:field:update",
      "base:record:create",
      "base:record:delete",
      "base:record:retrieve",
      "base:record:update",
      "base:table:create",
      "base:table:delete",
      "base:table:read",
      "base:table:update",
      "base:view:read",
      "base:view:write_only",
      "board:whiteboard:node:create",
      "board:whiteboard:node:read",
      "calendar:calendar.event:create",
      "calendar:calendar.event:delete",
      "calendar:calendar.event:read",
      "calendar:calendar.event:reply",
      "calendar:calendar.event:update",
      "calendar:calendar.free_busy:read",
      "calendar:calendar:read",
      "contact:contact.base:readonly",
      "contact:user.base:readonly",
      "contact:user.employee_id:readonly",
      "contact:user:search",
      "docs:document.comment:create",
      "docs:document.comment:read",
      "docs:document.comment:update",
      "docs:document.media:download",
      "docs:document:copy",
      "docx:document:create",
      "docx:document:readonly",
      "docx:document:write_only",
      "drive:drive.metadata:readonly",
      "drive:file:download",
      "drive:file:upload",
      "im:chat.members:read",
      "im:chat:read",
      "im:message",
      "im:message.group_msg:get_as_user",
      "im:message.p2p_msg:get_as_user",
      "im:message:readonly",
      "offline_access",
      "search:docs:read",
      "search:message",
      "space:document:delete",
      "space:document:move",
      "space:document:retrieve",
      "task:comment:read",
      "task:comment:write",
      "task:task:read",
      "task:task:write",
      "task:task:writeonly",
      "task:tasklist:read",
      "task:tasklist:write",
      "wiki:node:copy",
      "wiki:node:create",
      "wiki:node:move",
      "wiki:node:read",
      "wiki:node:retrieve",
      "wiki:space:read",
      "wiki:space:retrieve",
      "wiki:space:write_only"
    ]
  }
}
```

第六步：发布应用

进入"版本管理与发布"，点击"创建版本"，填写版本号后提交发布申请。管理员审批通过即生效（你本人是管理员可直接通过）。

这时候可以测试机器人是否正常工作。

```bash
(.venv) i@i:~/Code/DuckyClaw$ tos.py config choice
[INFO]: Running tos.py ...
[INFO]: >>> subprocess >>>
cd /home/i/Code/DuckyClaw/.build && ninja clean_all
[0/2] [TOP] Platform [T5AI] clean:
country code: Japan
get package from [Japan linux_aarch64]
[do subprocess]: export TUYA_TOOLCHAIN_PATH=/home/i/Code/DuckyClaw/TuyaOpen/platform/tools/gcc-arm-none-eabi-10.3-2021.10; cd /home/i/Code/DuckyClaw/TuyaOpen/platform/T5AI/t5_os; make clean
save sdkconfig.h
rm -rf ./build
/home/i/Code/DuckyClaw/TuyaOpen/platform/T5AI
[2/2] cd /home/i/Code/DuckyClaw/.build && /home/i/Code/DuckyClaw/TuyaOpen/.venv/bin/ninja clean
[1/1] Cleaning all built files...
Cleaning... 748 files.
[NOTE]: Clean success.
[INFO]: >>> subprocess >>>
rm -rf "/home/i/Code/DuckyClaw/.build"
[NOTE]: Fullclean success.
```

输入 4 选择 TUYA_T5AI_BOARD_LCD_3.5_CAMERA：

```bash
--------------------
1. ATK_T5AI_MINI_BOARD_2.4LCD_CAMERA.config
2. ESP32S3_BREAD_COMPACT_WIFI.config
3. RaspberryPi.config
4. TUYA_T5AI_BOARD_LCD_3.5_CAMERA.config
--------------------
Input "q" to exit.
Choice config file: 4
[INFO]: Initialing using.config ...
[NOTE]: Choice config: /home/i/Code/DuckyClaw/config/TUYA_T5AI_BOARD_LCD_3.5_CAMERA.config
```

编译与烧录

编译工程：

`tos.py build`

编译成功后烧录固件：

`tos.py flash`

连接串口查看日志：

`tos.py monitor`

预期结果：工程编译通过，固件烧录到 T5-AI Board 后设备正常启动。可通过串口确认进入激活模式，再在 App 中添加设备。

设备激活与配网

使用 Tuya Cloud 功能前，需在 智能生活 App 中添加设备并完成 Wi‑Fi 配网。

下载智能生活 App

从苹果 App Store 或各大安卓应用市场搜索 智能生活 下载，或扫描 Tuya 智能生活 App 页面 上的二维码。

确认设备处于配网状态

在 App 中添加设备前，请确认设备已进入配网（激活）模式。串口日志中可见类似输出（TuyaOpen）：

[01-01 00:00:01 ty D][tuya_iot.c:774] STATE_START
[01-01 00:00:01 ty I][tuya_iot.c:792] Activation data read fail, go activation mode...
[01-01 00:00:01 ty D][tuya_main.c:143] Tuya Event ID:1(TUYA_EVENT_BIND_START)

在 App 中添加设备

1. 打开智能生活 App，点击 添加设备 或右上角 + 进入添加流程。
2. 按提示授予 App Wi‑Fi 与 蓝牙 权限，否则无法发现设备。
3. 按 App 内步骤将设备连接到家庭 Wi‑Fi。
4. 在 首页 或 添加设备 页看到待添加设备后，点击 去添加，按引导完成添加。

第七步：配置事件订阅

进入"事件与回调"，点击"事件配置"。

选择"使用长连接接收事件"

添加事件：**im.message.receive_v1**

![event](/assets/images/AI/Day97/event.png)

## 预览

<video src="https://mpvideo.qpic.cn/0bc3s4coeaaejaacfnvskfuvjf6d4klqjyqa.f0.mp4?dis_k=d1ec8c0fa7fc1c9ea10228a363adcfee&dis_t=1773584794&play_scene=10600&auth_info=Ja3p6TlNI3nIzcffZ3A5TjBdLz00EBkzNFZicG5JcTYeMhsxL10=&auth_key=ed283feb89deb283a8c5926a402e8c97&preview=true" controls></video>
