---
description: 可以使用 Microsoft Message Analyzer (MMA) 来捕获和查看实时 USB 跟踪，或查看现有跟踪。
Search.SourceType: Video
title: 使用 Microsoft Message Analyzer 捕获和查看 USB 跟踪
ms.date: 08/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5acaa0c016e7af154d753479acb2ecfdd13a4cb0
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969548"
---
# <a name="capture-and-view-usb-traces-with-microsoft-message-analyzer"></a>使用 Microsoft Message Analyzer 捕获和查看 USB 跟踪

>[!IMPORTANT]
>Microsoft Message Analyzer 工具已停用。 我们将离开此页面，适用于先前已下载工具的用户。

可以使用 Microsoft Message Analyzer (MMA) 来捕获和查看实时 USB 跟踪，或查看现有跟踪。

无需使用命令行工具（logman）来捕获跟踪，然后在 Netmon 3.4 中对其进行分析，只需从一个 GUI 即可执行所有这些任务。

## <a name="install-and-launch-microsoft-message-analyzer"></a>安装和启动 Microsoft Message Analyzer

1.  [下载 Microsoft Message Analyzer](https://www.microsoft.com/download/details.aspx?id=44226) 并按照 "下载" 页上的 **安装说明** 安装该工具。 下载后，请按照安装提示进行操作并选择 " **更新项目**"。

2.  安装完成后，将启动工具并显示起始页。

## <a name="set-up-a-trace-session-and-capture-usb-events"></a>设置跟踪会话并捕获 USB 事件

此视频演示如何通过添加特定列为 USB 跟踪设置 Microsoft Message Analyzer。 它还演示了如何通过启动和停止会话来捕获实时跟踪。

> [!NOTE]
> 在 " **设备**" 下，选择 "usb 2" 或 "usb 3" 跟踪方案。 请注意，USB 3 跟踪仅适用于 Windows 8 及更高版本。 根据设备连接到的主机控制器进行选择，而不是设备的速度。 例如，如果已将高速设备连接到 xHCI 控制器，请选择 "USB 3" 跟踪方案。

>[!VIDEO https://www.microsoft.com/videoplayer/embed/e5300401-351e-4dcc-bcc2-edd07079d7fa]

## <a name="analyze-a-usb-trace"></a>分析 USB 跟踪

Microsoft Message Analyzer 会在捕获信息时动态分析该信息并以用户可读的形式显示信息。 其中的大多数信息都显示在 " **摘要** " 列中。 此列显示有关事件的详细信息，例如，请求将 USB 驱动程序堆栈发送到设备。 通过添加所需的筛选器，您可以查看这些请求的结果。

此视频演示如何确定设备枚举失败的根本原因。

>[!VIDEO https://www.microsoft.com/videoplayer/embed/29cb1d44-a38a-4105-9513-256e69e9f6a0]

## <a name="related-topics"></a>相关主题
[博客：通过 Microsoft Message Analyzer 捕获 USB ETW 跟踪 (MMA) ](https://techcommunity.microsoft.com/t5/Microsoft-USB-Blog/bg-p/MicrosoftUSBBlog/archive/2013/11/09/capturing-usb-etw-traces-with-microsoft-message-analyzer-mma.aspx)  
[Windows 的 USB 事件跟踪](usb-event-tracing-for-windows.md)  



