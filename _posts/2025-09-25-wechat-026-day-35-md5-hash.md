---
layout: post
title: "Day 35: 文件 md5 Hash"
author: iosdevlog
date: 2025-09-25 23:53:10 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247485858&idx=1&sn=c0c0dff1a5114b1b32572df41fc9d3a7&chksm=f95c9225ce2b1b33df85c28000de0c3fd4b41b71bb41214abf05f2c077c0c46cf91e7a0c6db1#rd

Hash

简体中文

A concise and efficient macOS hash calculation tool that supports multiple hash algorithms and batch file processing.

Features

🔐 Multiple Hash Algorithm Support: MD5, SHA-1, CRC32

📁 Batch File Processing: Calculate hash values for multiple files simultaneously

🎯 Drag & Drop Operation: Simply drag files to the application window to start calculation

📋 One-Click Copy: Click to copy hash values to clipboard

📊 File Information Display: Shows file size, version info, modification date, etc.

🌍 Multilingual Support: Supports 22 languages including Chinese, English, Japanese, Korean, German, French, Spanish, Russian, Arabic, etc.

🎨 Modern Interface: Native macOS app built with SwiftUI

⚡ High Performance Computing: Asynchronous processing with support for large files

Screenshots

Main interface of the Hash application, showcasing file selection, hash calculation, and result display features

System Requirements

macOS 11.0 or later

Xcode 13.0 or later (for development)

Installation

Build from Source

Clone the repository:

git clone https://github.com/build-your-own-x-with-ai/Hash

cd Hash

Open the project with Xcode:

open Hash.xcodeproj

Build and run the project in Xcode (⌘+R)

Usage

Basic Operations

Launch the Application: Double-click the app icon or launch from Launchpad

Add Files:

Click the "Select Files" button to choose files

Or drag files directly to the application window

Select Hash Algorithm:

Check the desired hash algorithms in the right panel

Supports MD5, SHA-1, CRC32

Start Calculation:

Click the "Start Calculation" button

Or calculation starts automatically after adding files

Copy Results:

Click any hash value to copy to clipboard

Supports copying individual hash values or all results

Advanced Features

Batch Processing

: Add multiple files for simultaneous batch calculation

Progress Display

: Real-time calculation progress display

File Management

: Support for clearing individual files or all files

Result Export

: Copy all calculation results

Technical Architecture

Core Technologies

SwiftUI

: Modern user interface framework

CryptoKit

: Apple's official cryptographic framework for SHA-1 calculation

Foundation

: For MD5 and file operations

UniformTypeIdentifiers

: File type identification

Project Structure

Hash/

├── Hash/

│   ├── ContentView.swift          # Main interface view

│   ├── HashApp.swift              # Application entry point

│   ├── Assets.xcassets/           # Application resources

│   │   └── AppIcon.appiconset/    # Application icon

│   ├── Hash.entitlements          # Application permissions

│   └── *.lproj/                   # Multilingual localization files

├── HashTests/                     # Unit tests

└── HashUITests/                   # UI tests

Hash Algorithm Implementation

MD5

: Implemented using CommonCrypto framework

SHA-1

: Implemented using CryptoKit framework

CRC32

: Custom implementation using standard CRC32 polynomial

Development

Environment Setup

Install Xcode 13.0 or later

Ensure macOS version is 11.0 or later

Clone the project and open in Xcode

Build Project

# Build using Xcode command line toolsxcodebuild -project Hash.xcodeproj -scheme Hash -configuration Debug build# Or use shortcut ⌘+B in Xcode

Run Tests

# Run unit testsxcodebuild test -project Hash.xcodeproj -scheme Hash -destination 'platform=macOS'# Or use shortcut ⌘+U in Xcode

Localization

The application supports the following 22 languages:

Asian Languages

🇨🇳 中文（简体）(Chinese Simplified)

🇹🇼 中文（繁体）(Chinese Traditional)

🇯🇵 日本語 (Japanese)

🇰🇷 한국어 (Korean)

🇹🇭 ไทย (Thai)

🇻🇳 Tiếng Việt (Vietnamese)

🇮🇳 हिन्दी (Hindi)

🇮🇩 Bahasa Indonesia (Indonesian)

🇲🇾 Bahasa Melayu (Malay)

European Languages

🇺🇸 English

🇩🇪 Deutsch (German)

🇫🇷 Français (French)

🇪🇸 Español (Spanish)

🇮🇹 Italiano (Italian)

🇵🇹 Português (Portuguese)

🇳🇱 Nederlands (Dutch)

🇸🇪 Svenska (Swedish)

🇳🇴 Norsk (Norwegian)

🇩🇰 Dansk (Danish)

🇫🇮 Suomi (Finnish)

🇵🇱 Polski (Polish)

🇨🇿 Čeština (Czech)

🇭🇺 Magyar (Hungarian)

🇬🇷 Ελληνικά (Greek)

🇹🇷 Türkçe (Turkish)

🇺🇦 Українська (Ukrainian)

🇷🇴 Română (Romanian)

🇧🇬 Български (Bulgarian)

🇸🇰 Slovenčina (Slovak)

🇸🇮 Slovenščina (Slovenian)

🇭🇷 Hrvatski (Croatian)

🇷🇸 Српски (Serbian)

🇷🇺 Русский (Russian)

Middle Eastern Languages

🇸🇦 العربية (Arabic)

🇮🇱 עברית (Hebrew)

Adding New Languages

Select the project in Xcode

Add a new language in the "Localizations" section

Translate the strings in the Localizable.strings file

Contributing

Issues and Pull Requests are welcome!

Contribution Guidelines

Fork the project

Create a feature branch (git checkout -b feature/AmazingFeature)

Commit your changes (git commit -m 'Add some AmazingFeature')

Push to the branch (git push origin feature/AmazingFeature)

Create a Pull Request

License

This project is licensed under the MIT License - see the LICENSE file for details.

Changelog

v1.0.0

✨ Initial release

🔐 Support for MD5, SHA-1, CRC32 hash algorithms

📁 Support for batch file processing

🎯 Support for drag & drop operations

🌍 Support for multilingual interface

🎨 Modern SwiftUI interface

Contact

For questions or suggestions, please contact us through:

Submit Issues: GitHub Issues

Project Homepage: GitHub Repository

Hash - Making file hash calculation simple and efficient 🚀

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTRCViaDc0qm7sPSIdIqicv4YLsOWW2IAibILb9zZrycFslcudtBvtlk6iaACrdkgAjBNiaJ15bgyYUo06A/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)
