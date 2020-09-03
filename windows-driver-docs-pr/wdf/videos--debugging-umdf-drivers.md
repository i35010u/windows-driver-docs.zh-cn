---
title: 视频调试 UMDF 驱动程序
description: 本主题包含一系列视频，通过 Abhishek Ram 演示如何调试用户模式驱动程序框架 (UMDF) 驱动程序。
Search.SourceType: Video
ms.assetid: 969FD292-5D92-4257-8E15-F2129B832E22
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17835194219d93e56579058d2fad6576a3d97200
ms.sourcegitcommit: 057b72e8a44ba8f4282e072edc7be0b7e9341d2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89412492"
---
# <a name="videos-debugging-umdf-drivers"></a>视频：调试 UMDF 驱动程序


本主题包含一系列视频，通过 Abhishek Ram 演示如何调试用户模式驱动程序框架 (UMDF) 驱动程序。

观看视频后，你将熟悉 UMDF 调试器扩展，并了解如何在基本调试方案中使用它们。

尽管视频演示了在较早版本的 Windows 上调试 UMDF 版本1驱动程序，但仍可使用与当前版本的 Windows 上运行的 UMDF 版本2驱动程序相同的技术。

**注意**   此视频介绍 Wudfext.dll 中的调试程序扩展命令，你可以使用这些命令仅调试 UMDF 版本1驱动程序。 若要调试在 UMDF 版本2.0 中启动的 UMDF 驱动程序，你必须改用 Wdfkd.dll 调试程序扩展库。 在 Wdfkd.dll 中，Wudfext.dll 中的所有扩展都有等效项。 有关详细信息，请参阅 [中的调试器扩展摘要 Wudfext.dll](using-umdf-debugger-extensions.md) 和 [Wdfkd.dll中调试器扩展的摘要 ](debugger-extensions-for-kmdf-drivers.md)。

 

有关调试 UMDF 的详细信息，请参阅 [调试 WDF 驱动程序](accessing-umdf-metadata-in-wer-reports.md)中列出的主题。

## <a name="prerequisites"></a>先决条件


若要充分利用此内容，您应该具有 UMDF 和 Windows 调试工具方面的知识。 由于每个会话都是在上一个会话中生成的，因此我们建议你按列出的顺序查看这些演示。

## <a name="basics-and-setup"></a>基础知识和设置


讨论如何使用 WDK 示例和 OSR USB-FX2 学习工具包。

>[!VIDEO https://www.microsoft.com/videoplayer/embed/d1040a16-81ec-40bb-a2d5-05021a37a144]

在此视频中，你将了解有关 UMDF 调试基础知识的信息，包括准备测试计算机，使用 Devcon 工具安装 UMDF 回送示例驱动程序，使用您尚未 wdfverifier 识别承载给定 UMDF 驱动程序的主机进程，并使用您尚未 wdfverifier 将宿主进程及时附加到调试器以调试初始化代码。 此视频还演示了如何在任务管理器中列出正在运行的主机进程，以及如何在设备管理器中查看正在运行的驱动程序。

## <a name="examining-the-object-hierarchy-with-debugger-extensions"></a>检查包含调试器扩展的对象层次结构

>[!VIDEO https://www.microsoft.com/videoplayer/embed/da033b03-b965-40cc-9697-ecb97430006a]

在此部分中，你将了解如何启动 UMDF 驱动程序调试。 该视频介绍了如何设置 OSR USB-FX2 driver 示例和应用程序示例，以便应用程序的三个实例将读取、写入和设备 i/o 控制请求发送到驱动程序。 你将看到，请求首先流向反射器，然后才流向用户模式驱动程序主机进程。 此视频介绍了 FX2 驱动程序示例的 WDF 对象层次结构，并讨论了如何使用以下 UMDF 调试器扩展来遍历 UMDF 对象层次结构：

-   [**!wudfext.umdevstacks**](../debugger/-wudfext-umdevstacks.md)
-   [**!wudfext.wudfdriverinfo**](../debugger/-wudfext-wudfdriverinfo.md)
-   [**!wudfext.wudfdevice**](../debugger/-wudfext-wudfdevice.md)
-   [**!wudfext.wudfdevicequeues**](../debugger/-wudfext-wudfdevicequeues.md)

有关 UMDF 2 的详细概述，请参阅 [Wdfkd.dll中的调试器扩展的摘要 ](debugger-extensions-for-kmdf-drivers.md)，例如 [**！ wdfkd. wdfumdevstacks**](../debugger/-wdfkd-wdfumdevstacks.md)。

## <a name="accessing-framework-usb-objects"></a>访问框架 USB 对象

>[!VIDEO https://www.microsoft.com/videoplayer/embed/f22577ab-1da0-47ae-b12b-ed3d586cde9e]

在这里，你将了解如何检查驱动程序的框架 USB 对象。 为此，你将浏览 WDF 对象种层次结构以到达 USB 管道对象、USB 接口对象和 USB i/o 目标对象。

##  <a name="io-requests-and-queues"></a>I/o 请求和队列

>[!VIDEO https://www.microsoft.com/videoplayer/embed/48165551-a75d-4855-b0c8-3e55826f4f5e]

在此视频中，您将使用调试器来检查驱动程序的框架 i/o 请求对象和框架队列对象。

## <a name="file-objects-and-callback-objects"></a>文件对象和回调对象

>[!VIDEO https://www.microsoft.com/videoplayer/embed/39c05ac7-3e20-4b8d-bcc9-37f450ddf507]

在此部分中，你将了解如何检查框架文件对象以及驱动程序的回调对象。

##  <a name="tracking-io-requests-sent-by-a-umdf-driver"></a>跟踪 UMDF 驱动程序发送的 i/o 请求

>[!VIDEO https://www.microsoft.com/videoplayer/embed/8d1aa0a2-4360-4d68-9b09-310851a6087f]

在这里，你将学习如何使用应用程序验证器工具来帮助你进行调试。 你还将了解如何调试驱动程序初始化代码，以及如何跟踪从 UMDF 驱动程序发送到下面的内核堆栈的请求。

##  <a name="driver-does-not-complete-an-io-request"></a>驱动程序未完成 i/o 请求

>[!VIDEO https://www.microsoft.com/videoplayer/embed/ddf4eff2-73f9-44a9-8602-adb08fc48373]

在最后的视频中，当 UMDF 驱动程序未完成收到的请求时，你将调查其情况，你将了解框架的对象跟踪和引用跟踪功能。

 

