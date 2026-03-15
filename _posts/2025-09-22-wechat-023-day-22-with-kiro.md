---
layout: post
title: "Day 22: 打造自己的离线维基百科 with Kiro"
author: iosdevlog
date: 2025-09-22 23:57:30 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247485830&idx=1&sn=62795e67ba353cb5fe3357572441ecb1&chksm=f95c9201ce2b1b173f42f1c02d5920c9f71c0e6e6d58615e7c1d3ac4b2f750ff615ae04bb156#rd

需求文档

介绍

此功能将为 WiKi 应用添加离线维基百科下载和管理功能。用户可以浏览 Kiwix 镜像站点上可用的 .zim 维基百科文件，下载所需的语言版本，并在本地离线查看维基百科内容。这将使用户能够在没有网络连接的情况下访问维基百科知识。

需求

需求 1

用户故事： 作为用户，我希望能够浏览可用的离线维基百科版本，以便选择我需要的语言和版本进行下载。

验收标准

当用户打开下载页面时，系统应显示从 https://www.mirrorservice.org/sites/download.kiwix.org/zim/wikipedia/ 获取的可用 .zim 文件列表

当系统获取文件列表时，系统应显示每个文件的语言、大小、发布日期和描述信息

当网络连接不可用时，系统应显示适当的错误消息并提供重试选项

当文件列表加载时，系统应显示加载指示器

需求 2

用户故事： 作为用户，我希望能够下载选定的 .zim 维基百科文件，以便离线使用。

验收标准

当用户选择一个 .zim 文件时，系统应开始下载该文件到本地存储

当下载进行中时，系统应显示下载进度条和当前下载速度

当下载完成时，系统应通知用户下载成功并更新文件状态

当下载失败时，系统应显示错误消息并提供重试选项

当用户取消下载时，系统应停止下载并清理部分下载的文件

需求 3

用户故事： 作为用户，我希望能够管理已下载的维基百科文件，以便有效利用设备存储空间。

验收标准

当用户查看下载列表时，系统应显示所有已下载文件的状态（已下载、下载中、暂停、失败）

当用户长按已下载的文件时，系统应提供删除选项

当用户删除文件时，系统应从本地存储中移除该文件并更新列表

当系统检测到存储空间不足时，系统应警告用户并建议删除不需要的文件

需求 4

用户故事： 作为用户，我希望能够搜索和筛选可用的维基百科版本，以便快速找到我需要的内容。

验收标准

当用户在搜索框中输入关键词时，系统应实时筛选显示匹配的 .zim 文件

当用户选择语言筛选器时，系统应只显示该语言的维基百科版本

当用户按文件大小排序时，系统应按升序或降序重新排列文件列表

当没有匹配的搜索结果时，系统应显示"未找到匹配项"的消息

需求 5

用户故事： 作为用户，我希望能够离线查看已下载的维基百科内容，以便在没有网络的情况下获取知识。

验收标准

当用户点击已下载的 .zim 文件时，系统应打开该维基百科的主页

当用户在离线维基百科中搜索时，系统应在本地 .zim 文件中查找匹配的文章

当用户点击文章链接时，系统应在应用内显示该文章内容

当 .zim 文件损坏或无法读取时，系统应显示错误消息并建议重新下载

设计文档

概述

离线维基百科下载器功能将为 WiKi 应用添加完整的离线维基百科管理系统。该功能包括从 Kiwix 镜像站点获取可用文件列表、下载管理、本地存储和离线内容查看。设计采用 MVVM 架构模式，确保代码的可维护性和可测试性。

架构

整体架构

┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐

│   Presentation  │    │    Business     │    │      Data       │

│     Layer       │◄──►│     Logic       │◄──►│     Layer       │

│   (SwiftUI)     │    │   (ViewModels)  │    │ (Repositories)  │

└─────────────────┘    └─────────────────┘    └─────────────────┘

核心组件

DownloadListView

: 主要的下载管理界面

WikipediaFileService

: 处理文件列表获取和下载逻辑

ZimFileManager

: 管理本地 .zim 文件的存储和访问

WikipediaReader

: 处理 .zim 文件的读取和内容展示

组件和接口

1. 数据模型

WikipediaFile

structWikipediaFile: Identifiable, Codable {

let id =UUID()

let name: String

let url: URL

let size: Int64

let language: String

let description: String

let publishDate: Date

var downloadStatus: DownloadStatus= .notDownloaded

var downloadProgress: Double=0.0

}

enumDownloadStatus: String, CaseIterable {

case notDownloaded ="未下载"

case downloading ="下载中"

case paused ="已暂停"

case completed ="已完成"

case failed ="下载失败"

}

DownloadTask

classDownloadTask: ObservableObject {

let file: WikipediaFile

@Publishedvar progress: Double=0.0

@Publishedvar status: DownloadStatus= .notDownloaded

@Publishedvar downloadSpeed: String=""

@Publishedvar error: Error?

privatevar urlSessionTask: URLSessionDownloadTask?

}

2. 服务层

WikipediaFileService

protocolWikipediaFileServiceProtocol {

funcfetchAvailableFiles() asyncthrows -> [WikipediaFile]

funcdownloadFile(_file: WikipediaFile) -> DownloadTask

funccancelDownload(forfile: WikipediaFile)

funcpauseDownload(forfile: WikipediaFile)

funcresumeDownload(forfile: WikipediaFile)

}

classWikipediaFileService: NSObject, WikipediaFileServiceProtocol, URLSessionDownloadDelegate {

privatelet session: URLSession

privatevar activeTasks: [UUID: DownloadTask] = [:]

// 实现网络请求和下载管理

}

ZimFileManager

protocolZimFileManagerProtocol {

funcgetLocalFiles() -> [WikipediaFile]

funcdeleteFile(_file: WikipediaFile) throws

funcgetFileSize(_file: WikipediaFile) -> Int64

funcisFileValid(_file: WikipediaFile) -> Bool

funcgetStorageInfo() -> StorageInfo

}

structStorageInfo {

let totalSpace: Int64

let availableSpace: Int64

let usedSpace: Int64

}

3. 视图模型

DownloadListViewModel

classDownloadListViewModel: ObservableObject {

@Publishedvar availableFiles: [WikipediaFile] = []

@Publishedvar downloadedFiles: [WikipediaFile] = []

@Publishedvar isLoading =false

@Publishedvar searchText =""

@Publishedvar selectedLanguage: String?

@Publishedvar sortOption: SortOption= .name

@Publishedvar errorMessage: String?

privatelet fileService: WikipediaFileServiceProtocol

privatelet zimManager: ZimFileManagerProtocol

// 业务逻辑方法

funcloadAvailableFiles()

funcdownloadFile(_file: WikipediaFile)

funcdeleteFile(_file: WikipediaFile)

funcfilteredFiles() -> [WikipediaFile]

}

enumSortOption: String, CaseIterable {

case name ="名称"

case size ="大小"

case date ="日期"

case language ="语言"

}

4. 用户界面组件

DownloadListView

structDownloadListView: View {

@StateObjectprivatevar viewModel =DownloadListViewModel()

@Stateprivatevar showingDownloaded =false

var body: someView {

NavigationView {

VStack {

SearchAndFilterBar()

SegmentedControl() // 可用文件 / 已下载文件

FileListView()

}

}

}

}

FileRowView

structFileRowView: View {

let file: WikipediaFile

let onDownload: () -> Void

let onDelete: () -> Void

var body: someView {

HStack {

FileInfoView(file: file)

Spacer()

ActionButtonsView(file: file, onDownload: onDownload, onDelete: onDelete)

}

}

}

数据模型

本地存储结构

Documents/

├── WikipediaFiles/

│   ├── downloaded/

│   │   ├── wikipedia_zh_all_2024-01.zim

│   │   └── wikipedia_en_all_2024-01.zim

│   └── metadata/

│       └── files_metadata.json

网络数据解析

从 Kiwix 镜像站点解析 HTML 页面，提取 .zim 文件信息：

文件名和下载链接

文件大小

最后修改日期

通过文件名推断语言和描述

错误处理

网络错误处理

enumNetworkError: LocalizedError {

case noInternetConnection

case serverUnavailable

case invalidResponse

case downloadFailed(Error)

var errorDescription: String? {

switchself {

case .noInternetConnection:

return"网络连接不可用，请检查网络设置"

case .serverUnavailable:

return"服务器暂时不可用，请稍后重试"

case .invalidResponse:

return"服务器响应无效"

case .downloadFailed(let error):

return"下载失败：\(error.localizedDescription)"

}

}

}

存储错误处理

enumStorageError: LocalizedError {

case insufficientSpace

case fileCorrupted

case permissionDenied

case fileNotFound

var errorDescription: String? {

switchself {

case .insufficientSpace:

return"存储空间不足，请删除一些文件后重试"

case .fileCorrupted:

return"文件已损坏，建议重新下载"

case .permissionDenied:

return"没有文件访问权限"

case .fileNotFound:

return"文件未找到"

}

}

}

测试策略

单元测试

WikipediaFileService

: 测试网络请求、下载逻辑

ZimFileManager

: 测试文件管理操作

DownloadListViewModel

: 测试业务逻辑和状态管理

集成测试

网络层集成

: 测试实际的网络请求和响应处理

文件系统集成

: 测试文件下载、存储和删除流程

UI集成

: 测试用户交互和状态更新

UI测试

下载流程

: 测试完整的文件下载用户流程

搜索和筛选

: 测试搜索功能和筛选器

错误处理

: 测试各种错误场景的用户体验

性能测试

大文件下载

: 测试大型 .zim 文件的下载性能

内存使用

: 监控下载过程中的内存使用情况

并发下载

: 测试多个文件同时下载的性能

测试数据

使用模拟的 Kiwix 服务器响应进行单元测试

创建小型测试 .zim 文件用于集成测试

使用真实的网络环境进行端到端测试

实施计划

[x] 1. 建立项目结构和核心数据模型

创建 Models、Services、ViewModels 和 Views 目录结构

实现 WikipediaFile 和 DownloadStatus 数据模型

创建 DownloadTask 类用于管理下载状态

需求: 1.1, 2.1, 3.1

[x] 2. 实现网络服务层

使用 URLSession 实现文件下载

添加下载进度跟踪

实现下载暂停和恢复功能

处理下载失败和重试逻辑

需求: 2.1, 2.2, 2.4, 2.5

创建 HTML 解析器获取 .zim 文件列表

解析文件名、大小、日期等信息

实现语言识别逻辑

编写解析功能的单元测试

需求: 1.1, 1.2

定义网络服务接口

实现基础的网络请求功能

添加错误处理机制

需求: 1.1, 1.3

[x] 2.1 创建 WikipediaFileService 协议和基础实现

[x] 2.2 实现 Kiwix 镜像站点数据解析

[x] 2.3 实现文件下载功能

[x] 3. 创建本地文件管理系统

添加文件删除功能

实现文件完整性验证

创建存储信息查询接口

编写文件管理的单元测试

需求: 3.2, 3.3

创建本地文件存储结构

实现文件元数据管理

添加存储空间检查功能

需求: 3.1, 3.4

[x] 3.1 实现 ZimFileManager

[x] 3.2 实现文件操作功能

[x] 4. 开发核心视图模型

添加下载任务管理

实现下载状态更新

处理并发下载限制

编写视图模型的单元测试

需求: 2.1, 2.2, 2.3

实现文件列表状态管理

添加搜索和筛选逻辑

集成网络服务和文件管理器

需求: 4.1, 4.2, 4.3

[x] 4.1 创建 DownloadListViewModel

[x] 4.2 实现下载管理逻辑

[x] 5. 构建用户界面组件

实现搜索栏组件

添加语言筛选器

创建排序选项界面

需求: 4.1, 4.2, 4.3, 4.4

创建 FileRowView 显示文件信息

添加下载进度条

实现操作按钮（下载/删除/暂停）

需求: 1.2, 2.2, 3.2

实现 DownloadListView 主界面

添加分段控制器（可用/已下载）

创建加载状态指示器

需求: 1.1, 1.4, 3.1

[x] 5.1 创建主要列表视图

[x] 5.2 实现文件行视图组件

[x] 5.3 开发搜索和筛选界面

[x] 6. 实现离线内容查看功能

创建文章显示视图

实现内部链接导航

添加搜索结果显示

处理损坏文件的错误情况

需求: 5.1, 5.3, 5.4

研究和集成 ZIM 文件读取库

实现基础的文件内容提取

添加文章搜索功能

需求: 5.1, 5.2

[x] 6.1 创建 ZIM 文件读取器

[x] 6.2 开发离线维基百科查看器

[-] 7. 添加错误处理和用户反馈

实现下载完成通知

添加存储空间警告

创建操作确认对话框

需求: 2.3, 3.4

创建统一的错误处理机制

添加用户友好的错误消息

实现错误恢复建议

需求: 1.3, 2.4, 3.4, 5.4

[x] 7.1 实现全局错误处理

[-] 7.2 添加用户通知和反馈

[ ] 8. 集成测试和优化

优化大文件下载性能

减少内存使用

测试并发下载场景

修复发现的问题

需求: 2.1, 2.2

测试完整的下载流程

验证文件管理操作

测试网络错误处理

需求: 所有需求

[ ] 8.1 编写集成测试

[ ] 8.2 性能优化和最终调试

[ ] 9. 更新主应用集成

修改 ContentView 集成新的下载功能

更新应用导航结构

确保与现有代码的兼容性

需求: 所有需求

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTTGKmNLQq59ZsjHdbySiaUdB7kXDNJMO9Fx5Bd9DzgyHEOkNFpyUxqHj8wBNcRzC558bb2F5AcicdIw/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)
