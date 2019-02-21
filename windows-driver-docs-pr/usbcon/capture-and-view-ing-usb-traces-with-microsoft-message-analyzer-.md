---
Description: You can use Microsoft Message Analyzer (MMA) to capture and view live USB traces, or view an existing trace.
Search.SourceType: Video
title: 捕获和查看使用 Microsoft Message Analyzer 的 USB 跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc3db2a968525f1e93672b68e82cc90ba054bdd2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545878"
---
# <a name="capture-and-view-usb-traces-with-microsoft-message-analyzer"></a>捕获和查看使用 Microsoft Message Analyzer 的 USB 跟踪


**摘要**

-   Microsoft Message Analyzer 安装和设置
-   捕获和查看实时 USB 跟踪

可以使用 Microsoft 消息分析器 (MMA) 来捕获和查看实时 USB 跟踪，或查看现有跟踪。

而不是通过使用命令行工具，logman，，然后将它们解析 Netmon 3.4 中捕获跟踪，可以从单个 GUI 执行所有这些任务。

## <a name="install-and-launch-microsoft-message-analyzer"></a>安装并启动 Microsoft Message Analyzer


1.  [下载 Microsoft Message Analyzer](https://www.microsoft.com/download/details.aspx?id=44226)并按照安装工具**安装说明**下载页上。 下载后，遵照安装提示并选择**更新项**。

2.  安装完成后，该工具将启动并显示起始页。

## <a name="set-up-a-trace-session-and-capture-usb-events"></a>设置跟踪会话，并捕获 USB 事件


此视频演示如何通过添加特定列中设置的 USB 跟踪 Microsoft Message Analyzer。 它还演示如何以实时跟踪捕获开始和停止会话。

**请注意**  下**设备**，USB 2 或 USB 3 跟踪方案之间进行选择。 请注意，USB 3 跟踪选项仅适用于 Windows 8 和更高版本。 请选择基于主机控制器连接到设备，不是设备的速度。 例如，如果具有较高的速度设备连接到 xHCI 控制器中，选择 USB 3 跟踪方案。

>[!VIDEO https://www.microsoft.com/videoplayer/embed/e5300401-351e-4dcc-bcc2-edd07079d7fa]

## <a name="analyze-a-usb-trace"></a>分析 USB 跟踪


Microsoft Message Analyzer 动态分析信息，因为它捕获，并在用户可读的窗体中显示它们。 所示的大部分信息都会**摘要**列。 该列将显示有关该事件，例如，请求将发送到设备的 USB 驱动程序堆栈的详细的信息。 通过添加所需的筛选器可以查看这些请求的结果。

此视频演示如何确定设备枚举故障的根本原因。

>[!VIDEO https://www.microsoft.com/videoplayer/embed/29cb1d44-a38a-4105-9513-256e69e9f6a0]

## <a name="related-topics"></a>相关主题
[博客：捕获 USB ETW 跟踪与 Microsoft 消息分析器 (MMA)](http://blogs.msdn.com/b/usbcoreblog/archive/2013/11/09/capturing-usb-etw-traces-with-microsoft-message-analyzer-mma.aspx)  
[USB Windows 事件跟踪](usb-event-tracing-for-windows.md)  



