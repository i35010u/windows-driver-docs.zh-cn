---
title: 调试 UMDF 驱动程序的视频
description: 本主题包含一系列由 Abhishek Ram 的视频演示如何调试用户模式驱动程序框架 (UMDF) 驱动程序。
Search.SourceType: Video
ms.assetid: 969FD292-5D92-4257-8E15-F2129B832E22
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2556a921a2be332e50be8ddc0bb55651fdf90f9c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372135"
---
# <a name="videos-debugging-umdf-drivers"></a>视频：调试 UMDF 驱动程序


本主题包含一系列由 Abhishek Ram 的视频演示如何调试用户模式驱动程序框架 (UMDF) 驱动程序。

观看视频之后, 将熟悉 UMDF 调试器扩展并知道如何在基本的调试方案中使用它们。

尽管这些视频演示调试在旧版本的 Windows 版本 1 UMDF 驱动程序，您仍可以通过当前版本的 Windows 上运行 UMDF 版本 2 驱动程序使用的相同技术。

**请注意**  此视频介绍了 Wudfext.dll，可用于调试 UMDF 版本 1 驱动程序中的调试器扩展命令。 若要调试 UMDF 驱动程序从 UMDF 2.0 版开始，必须改为使用 Wdfkd.dll 调试器扩展库。 所有 Wudfext.dll 中的扩展 Wdfkd.dll 中没有等效项。 有关详细信息，请参阅[摘要的调试器扩展中 Wudfext.dll](using-umdf-debugger-extensions.md)并[摘要的调试器扩展中 Wdfkd.dll](debugger-extensions-for-kmdf-drivers.md)。

 

有关调试 UMDF 的详细信息，请参阅中列出的主题[调试 WDF 驱动程序](debugging-a-wdf-driver.md)。

## <a name="prerequisites"></a>系统必备


若要充分利用此内容应具有 UMDF 和调试工具的 Windows 的应用知识。 由于每个会话建立在上一基础之上，我们建议按所列顺序查看这些演示。

## <a name="basics-and-setup"></a>基础知识和安装程序


讨论使用 WDK 示例和 OSR USB FX2 学习工具包。

>[!VIDEO https://www.microsoft.com/videoplayer/embed/d1040a16-81ec-40bb-a2d5-05021a37a144]

在此视频中，你将了解 UMDF 调试基础知识，包括准备你的测试计算机，使用 Devcon 工具安装 UMDF Echo 示例驱动程序，使用 WdfVerifier 来识别托管给定的 UMDF 驱动程序，以及使用 WdfVerifier 要附加的主机进程在时间中的调试器来调试初始化代码到主机进程。 此视频中还显示了如何列出正在运行的主机进程在任务管理器和视图运行设备管理器中的驱动程序。

## <a name="examining-the-object-hierarchy-with-debugger-extensions"></a>检查调试器扩展的对象层次结构

>[!VIDEO https://www.microsoft.com/videoplayer/embed/da033b03-b965-40cc-9697-ecb97430006a]

在此部分中，将学习如何启动调试 UMDF 驱动程序。 该视频介绍如何设置 OSR USB FX2 驱动程序示例和应用程序示例，以便应用程序的三个实例将读取、 写入和设备 I/O 控制请求发送到该驱动程序。 你将看到如何请求流第一次该发送程序，然后到用户模式驱动程序主机进程。 此视频介绍 FX2 驱动程序示例，WDF 对象层次结构，并讨论如何使用以下 UMDF 调试器扩展来遍历 UMDF 对象层次结构：

-   [ **!wudfext.umdevstacks**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-umdevstacks)
-   [ **!wudfext.wudfdriverinfo**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-wudfdriverinfo)
-   [ **!wudfext.wudfdevice**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-wudfdevice)
-   [ **!wudfext.wudfdevicequeues**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-wudfdevicequeues)

对于 UMDF 2，请参阅[摘要的调试器扩展中 Wdfkd.dll](debugger-extensions-for-kmdf-drivers.md)，例如[ **！ wdfkd.wdfumdevstacks**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstacks)。

## <a name="accessing-framework-usb-objects"></a>访问 framework USB 对象

>[!VIDEO https://www.microsoft.com/videoplayer/embed/f22577ab-1da0-47ae-b12b-ed3d586cde9e]

在这里，您将了解如何检查驱动程序的框架 USB 对象。 为此，请将浏览 WDF 对象层次结构变为 USB 管道对象、 USB 接口对象，并且 USB I/O 目标对象。

##  <a name="io-requests-and-queues"></a>I/O 请求和队列

>[!VIDEO https://www.microsoft.com/videoplayer/embed/48165551-a75d-4855-b0c8-3e55826f4f5e]

在本视频中，您将使用调试器来检查驱动程序的框架 I/O 请求对象和 framework 队列对象。

## <a name="file-objects-and-callback-objects"></a>文件对象和回调对象

>[!VIDEO https://www.microsoft.com/videoplayer/embed/39c05ac7-3e20-4b8d-bcc9-37f450ddf507]

在此部分中，将学习如何检查 framework 文件对象，以及驱动程序的回调对象。

##  <a name="tracking-io-requests-sent-by-a-umdf-driver"></a>跟踪由 UMDF 驱动程序发送的 I/O 请求

>[!VIDEO https://www.microsoft.com/videoplayer/embed/8d1aa0a2-4360-4d68-9b09-310851a6087f]

在这里，您将了解如何使用应用程序验证程序工具来帮助你调试。 此外将学习如何调试驱动程序初始化代码，以及如何跟踪请求发送到下面的内核堆栈 UMDF 驱动程序。

##  <a name="driver-does-not-complete-an-io-request"></a>驱动程序未完成 I/O 请求

>[!VIDEO https://www.microsoft.com/videoplayer/embed/ddf4eff2-73f9-44a9-8602-adb08fc48373]

在最终的视频中，在 UMDF 驱动程序不会完成它收到的请求时，您将研究一种情况，并你将了解有关框架的对象跟踪和跟踪功能的参考。

 

 





