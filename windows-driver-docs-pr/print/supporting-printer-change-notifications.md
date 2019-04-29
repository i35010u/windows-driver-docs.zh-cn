---
title: 支持打印机更改通知
description: 支持打印机更改通知
ms.assetid: e75c6f89-9cef-4900-af89-edf1f7f786c7
keywords:
- 打印提供程序 WDK，打印机更改通知
- 网络打印提供商 WDK、 打印机更改通知
- 通知 WDK 打印机
- 打印机更改通知 WDK
- 事件 WDK 打印机
- 打印队列 WDK，打印机更改通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd69e755e959b38879d8b19a14f916d3f934dd41
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354783"
---
# <a name="supporting-printer-change-notifications"></a>支持打印机更改通知





应用程序可以通过调用后台处理程序的请求通知的打印队列事件的出现次数**FindFirstPrinterChangeNotification**， **FindNextPrinterChangeNotification**，和**FindClosePrinterChangeNotification**函数，所有这些 Microsoft Windows SDK 文档中所述。 如果您认为应用程序编写器需要请求支持的部分的打印提供程序的打印队列的事件通知，则必须按如下所示支持提供程序中的事件通知：

-   提供[ **FindFirstPrinterChangeNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff548837)函数。

    后台处理程序调用此函数可提供以下信息的打印提供程序：

    -   一组标志，指示应用程序已为其请求通知的打印机事件的类型。
    -   正在为其请求通知的打印队列句柄。
    -   列表类型的信息的应用程序已请求在事件发生时提供。

    该函数必须返回标志值，该值指示是否应轮询该提供程序以确定是否已发生更改。 （nonpolled 提供程序发送信号到客户端每次更改发生时。 发生更改时，必须要轮询的提供程序不信号发送到客户端。 后台处理程序而是按固定间隔，指示客户端或不是否发生更改。)

    （请注意，在提供程序级别，此函数具有不同参数，而在 Win32 级别）。

-   跟踪的所有调用时指定的应用程序的打印队列事件**FindFirstPrinterChangeNotification**。

    (有关一系列类型的通知应用程序可以请求，并可以用来描述事件的信息类型的列表，请参阅 Windows SDK 文档的说明的 Win32 **FindFirstPrinterChangeNotification**函数。 类型的应用程序可以为其请求通知的事件包括添加或删除打印作业或窗体。 类型的应用程序可以请求的信息包括作业或窗体参数。）

    必须调用不对轮询的打印提供商[ **PartialReplyPrinterChangeNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff559739)或[ **ReplyPrinterChangeNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff561959)发生更改时，后台处理程序提供的信息描述所做的更改。 **ReplyPrinterChangeNotification**必须是函数调用在某一时刻，因为它会导致后台处理程序，以指示应用程序，而**PartialReplyPrinterChangeNotification**函数不。 当应用程序收到来自信号**ReplyPrinterChangeNotification**，它应调用**FindNextPrinterChangeNotification**。 这后一种功能提供了具有后台处理程序的打印提供程序从以前接收的事件信息的应用程序。

    轮询的打印提供商应只需跟踪的更改。 后台处理程序发出信号时间间隔来定期的应用程序。 当应用程序收到信号时，它应调用的后台处理程序**FindNextPrinterChangeNotification**函数。 对于轮询提供程序，此函数将调用提供程序的**RefreshPrinterChangeNotification**函数。

-   提供[ **RefreshPrinterChangeNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff561930)函数。

    此函数必须返回指定的打印队列的所有受监视打印队列选项的当前状态。 后台处理程序调用此函数，当应用程序调用**FindNextPrinterChangeNotification**与打印机\_通知\_选项\_设置刷新标志，如 Windows SDK 中所述文档。 (应用程序应设置此标志，如果以前调用**FindNextPrinterChangeNotification**返回打印机\_通知\_信息结构与打印机\_通知\_信息\_丢弃标志设置。)轮询和 nonpolled 提供程序必须支持**RefreshPrinterChangeNotification**。

-   提供**FindClosePrinterChangeNotification**函数 （Windows SDK 文档中所述）。

 

 




