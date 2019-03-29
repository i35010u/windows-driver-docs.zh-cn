---
title: 移动宽带类驱动程序日志事件跟踪日志跟踪
description: 本主题提供信息以帮助工程师使用移动宽带类驱动程序事件跟踪日志来查看和解决问题。
ms.assetid: 9742BFCA-CC22-497A-B11F-D3E89F0B4FE6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c54fd625e34cba642b3bd6f2288e36f33c13c510
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576164"
---
# <a name="mobile-broadband-class-driver-logs-event-trace-log-tracing"></a>移动宽带类驱动程序日志：事件跟踪日志跟踪


本主题提供信息以帮助工程师使用移动宽带类驱动程序事件跟踪日志来查看和解决问题。

本主题中的信息适用于：

-   Windows 8

## <a name="etl-tracing"></a>ETL 跟踪


以下过程介绍如何查看事件跟踪日志 (ETL):

1.  通过单击打开事件查看器**启动** &gt; **运行** &gt; **EventVwr**。
2.  在左窗格中，导航到**应用程序和服务日志** &gt; **Microsoft** &gt; **Windows**。

    ![显示导航到 windows 文件夹的步骤的屏幕截图](images/mbcdlogs1.png)

3.  导航下进一步**Windows**到**wmbclass。**

    ![打开 wmbclass 文件夹，显示 windows 移动宽带类驱动程序通道](images/mbcdlogs2.png)

4.  右键单击**Windows 移动宽带类驱动程序通道**然后单击**启用日志**。 如果您看到**禁用日志**，已启用日志。

    ![上下文菜单中显示的屏幕截图启用日志并刷新选项](images/mbcdlogs3.png)

5.  重现此问题并按**刷新**。 之后**刷新**，日志显示在中央窗格中。

    ![日志，其中上部窗格中选择事件的屏幕截图。 下部窗格显示常规选项卡上，并提供说明和的详细信息选项卡上，未选择](images/mbcdlogs4.png)

6.  可以使用日志进行筛选**操作窗格**在右侧。

    ![在操作窗格中使用筛选当前日志，示例显示了按事件 id 和事件级别筛选当前日志。 在这种情况下事件级别是错误，而事件 id 是-105。](images/mbcdlogs5.png)

## <a name="mobile-broadband-logs"></a>移动宽带日志


具体取决于问题和方案，不同片段是信息的为了确定一个解决方案，包括以下必需的：

**控制路径**

如果遇到连接问题，发送或接收短信、 发送或接收 USSD 消息，或使用配置文件，请收集以下信息：

1.  **netsh 跟踪启动 wwan\_dbg**
2.  执行将导致意外行为的系统的任务
3.  **netsh trace stop**
4.  上传下的所有文件 `%localappdata%\temp\nettraces\`

**IP 配置**

如果你有与 IP 地址配置的问题，请执行以下：

1.  1. **netsh 跟踪启动 wwan\_dbg**
2.  2. &lt;执行将导致意外行为的系统的任务
3.  3。**netsh trace stop**
4.  4. 上传以下信息：

    • 下的所有文件 `%localappdata%\temp\nettraces\`

    • 输出**ipconfig /all**

**数据路径**

如果要解决与数据数据包删除相关的问题，重试次数、 吞吐量问题或连接受到限制，请执行以下：

1.  **netsh 跟踪启动 wwan\_dbg，InternetClient，nid\_wpp 提供程序 = {c5aa495b-8432-4de5-9d7c-8afc7d3b522a} 0xFFFFFFFF 255**
2.  移动宽带卡上启动 netmon 跟踪。
3.  执行将导致意外行为的系统的任务
4.  停止 netmon 跟踪并保存 netmon 捕获。
5.  **netsh trace stop**
6.  上传以下信息：
    -   下的所有文件 `%localappdata%\temp\nettraces\`
    -   上传 netmon 捕获。

**设备枚举**

如果进行故障排除与在 USB 层设备枚举相关的问题，包括驱动程序加载问题 （不驱动程序无法启动），请执行以下：

1.  **logman start USBTrace -p Microsoft-Windows-USB-USBPORT -ets -nb 128 640 -bs 128 -o USBTrace.etl**
2.  **logman update USBTrace -p Microsoft-Windows-USB-USBHUB -ets -nb 128 640 -bs 128**
3.  **logman 更新跟踪 USBTrace-p {bc6c9364-fc67-42c5-acf7-abed3b12ecc6} 0xFFFFFFFF 255 – ets**
4.  执行将导致意外行为的系统的任务
5.  **Logman stop USBTrace ets**
6.  上传以下信息：
    -   `USBTrace.etl` 使用 logman 创建
    -   `c:\windows\inf\setupapi.dev.log`
    -   输出**devcon hwids"USB\\VID\_DeviceVendorID\*"**
        -   Devcon.exe 的最新版本是 WDK 的一部分。
        -   在存在较旧版本 http://support.microsoft.com/kb/311272

 

 





