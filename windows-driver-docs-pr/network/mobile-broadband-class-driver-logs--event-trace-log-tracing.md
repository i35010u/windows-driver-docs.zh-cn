---
title: 移动宽带类驱动程序日志事件跟踪日志跟踪
description: 本主题提供的信息可帮助工程师使用 Mobile 宽带类驱动程序事件跟踪日志来查看和解决问题。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 559173ee488e7e0bdb5cf5fbf03178517aaf0e50
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831337"
---
# <a name="mobile-broadband-class-driver-logs-event-trace-log-tracing"></a>移动宽带类驱动程序日志：事件跟踪日志跟踪


本主题提供的信息可帮助工程师使用 Mobile 宽带类驱动程序事件跟踪日志来查看和解决问题。

本主题中的信息适用于：

-   Windows 8

## <a name="etl-tracing"></a>ETL 跟踪


下面的过程介绍如何 (ETL) 查看事件跟踪日志：

1.  通过单击 " **开始** &gt; **运行** &gt; **eventvwr.msc**" 打开 EventViewer。
2.  在左窗格中，导航到 " **应用程序和服务日志**" " &gt; **Microsoft** &gt; **Windows**"。

    ![显示导航到 windows 文件夹的步骤的屏幕截图](images/mbcdlogs1.png)

3.  在 **Windows** 下进一步导航到 **wmbclass。**

    ![正在打开 wmbclass 文件夹，其中显示 windows mobile 宽带类驱动程序通道](images/mbcdlogs2.png)

4.  右键单击 " **Windows Mobile 宽带类驱动程序通道** "，然后单击 " **启用日志**"。 如果看到 " **禁用日志**"，则已启用日志。

    ![显示 "启用日志和刷新" 选项的上下文菜单的屏幕截图](images/mbcdlogs3.png)

5.  重现此问题并按 " **刷新**"。 **刷新** 后，日志将显示在中央窗格中。

    ![日志的屏幕截图，在上部窗格中选择事件。 下方窗格显示 "常规" 选项卡，"描述" 和 "详细信息" 选项卡，未选中](images/mbcdlogs4.png)

6.  可以使用右侧的 "操作" **窗格** 筛选日志。

    ![使用 "操作" 窗格中的 "筛选当前日志"，示例显示按事件 id 和事件级别筛选的当前日志。 在这种情况下，事件级别为 error，事件 id 为-105。](images/mbcdlogs5.png)

## <a name="mobile-broadband-logs"></a>移动宽带日志


根据问题和方案，需要不同的信息片段来确定解决方案，其中包括以下各项：

**控制路径**

如果在连接、发送或接收短信、发送或接收 USSD 消息或使用配置文件时遇到问题，请收集以下信息：

1.  **netsh trace 启动 wwan \_ dbg**
2.  执行导致系统意外行为的任务 () 
3.  **netsh 跟踪停止**
4.  上传所有文件 `%localappdata%\temp\nettraces\`

**IP 配置**

如果你在 IP 地址配置时遇到问题，请执行以下操作：

1. **netsh trace 启动 wwan \_ dbg**
2. &lt;执行导致系统意外行为的任务 () 
3. **netsh 跟踪停止**
4. 上传以下信息：

    - 下的所有文件 `%localappdata%\temp\nettraces\`

    - **Ipconfig/all** 的输出

**数据路径**

如果要解决与数据包丢弃、重试、吞吐量问题或连接受限相关的问题，请执行以下操作：

1.  **netsh trace 开始 wwan \_ dbg，InternetClient，nid \_ wpp provider = {C5aa495b-8432-4de5-9d7c-8afc7d3b522a} 0xffffffff 255**
2.  在移动宽带适配器上启动 netmon 跟踪。
3.  执行导致系统意外行为的任务 () 
4.  停止 netmon 跟踪并保存 netmon 捕获。
5.  **netsh 跟踪停止**
6.  上传以下信息：
    -   下的所有文件 `%localappdata%\temp\nettraces\`
    -   上传 netmon 捕获。

**设备枚举**

如果正在排查 USB 层上与设备枚举相关的问题，包括驱动程序加载问题 (驱动程序未能启动) ，请执行以下操作：

1.  **logman start USBTrace-p USBPORT-ets 128 640---bs.1770 128-o USBTrace**
2.  **logman update USBTrace-p USBHUB-ets-bs.1770 128 640-128**
3.  **logman update trace USBTrace-p {bc6c9364-fc67-42c5-acf7-abed3b12ecc6} 0xFFFFFFFF 255 – ets**
4.  执行导致系统意外行为的任务 () 
5.  **Logman stop USBTrace-ets**
6.  上传以下信息：
    -   `USBTrace.etl` 使用 logman 创建
    -   `c:\windows\inf\setupapi.dev.log`
    -   **Devcon hwid "USB \\ VID \_ DeviceVendorID \* "** 的输出
        -   最新版本的 Devcon.exe 是 WDK 的一部分。
        -   旧版本存在于 https://support.microsoft.com/kb/311272

 

 





