---
title: 支持打印机更改通知
description: 支持打印机更改通知
ms.assetid: e75c6f89-9cef-4900-af89-edf1f7f786c7
keywords:
- 打印提供程序 WDK，打印机更改通知
- 网络打印提供程序 WDK，打印机更改通知
- 通知 WDK 打印机
- 打印机更改通知 WDK
- 事件 WDK 打印机
- 打印队列 WDK，打印机更改通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fffb3726a62b847da4320b06416715eb3065fcb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838788"
---
# <a name="supporting-printer-change-notifications"></a>支持打印机更改通知





应用程序可以通过调用后台处理程序的**FindFirstPrinterChangeNotification**、 **FindNextPrinterChangeNotification**和**FindClosePrinterChangeNotification**请求出现打印队列事件的通知。函数，它们都在 Microsoft Windows SDK 文档中进行了介绍。 如果你认为应用程序编写器将需要为部分打印提供程序支持的打印队列请求事件通知，则必须在提供程序中支持事件通知，如下所示：

-   提供[**FindFirstPrinterChangeNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/nf-winspool-findfirstprinterchangenotification)函数。

    后台处理程序将调用此函数以向打印提供程序提供以下信息：

    -   指示应用程序已请求通知的打印机事件类型的一组标志。
    -   正在为其请求通知的打印队列的句柄。
    -   事件发生时应用程序请求提供的信息类型的列表。

    函数必须返回一个标志值，该值指示是否应轮询提供程序以确定是否发生了更改。 （Nonpolled 提供程序将在发生更改时向客户端发送信号。 发生更改时，必须轮询的提供程序不会向客户端发送信号。 相反，后台处理程序会定期向客户端发出信号，无论是否发生了更改。）

    （请注意，在提供程序级别，此函数具有与 Win32 级别不同的参数。）

-   跟踪应用程序在调用**FindFirstPrinterChangeNotification**时指定的所有打印队列事件。

    （有关应用程序可以请求的通知类型的列表，以及可用于描述事件的信息类型的列表，请参阅 Windows SDK 文档 Win32 **FindFirstPrinterChangeNotification**的说明才能. 应用程序可能请求通知的事件类型，包括添加或删除打印作业或窗体。 应用程序可能请求的信息类型包括作业或窗体参数。）

    在发生更改时，不轮询的打印提供程序必须调用[**PartialReplyPrinterChangeNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-partialreplyprinterchangenotification)或[**ReplyPrinterChangeNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-replyprinterchangenotification) ，以便为后台处理程序提供描述更改的信息。 必须在某个时间点调用**ReplyPrinterChangeNotification**函数，因为它会导致后台处理程序对应用程序发出信号，而**PartialReplyPrinterChangeNotification**函数则不会。 当应用程序从**ReplyPrinterChangeNotification**收到信号时，应调用**FindNextPrinterChangeNotification**。 后一种函数为应用程序提供了以前从打印提供程序收到的事件信息。

    轮询的打印提供程序只应跟踪更改。 后台处理程序会定期通知应用程序。 当应用程序收到信号时，应调用后台处理程序的**FindNextPrinterChangeNotification**函数。 对于轮询式提供程序，此函数将调用提供程序的**RefreshPrinterChangeNotification**函数。

-   提供[**RefreshPrinterChangeNotification**](https://docs.microsoft.com/previous-versions/ff561930(v=vs.85))函数。

    此函数必须返回指定打印队列的所有受监视打印队列选项的当前状态。 当应用程序使用打印机调用**FindNextPrinterChangeNotification**时，后台处理程序将调用此函数，\_\_通知设置\_刷新标志，如 Windows SDK 文档中所述。 （如果之前对**FindNextPrinterChangeNotification**的调用返回打印机，则应用程序应设置此标志\_\_\_通知通知\_信息\_丢弃标志集。）轮询式和 nonpolled 提供程序都必须支持**RefreshPrinterChangeNotification**。

-   提供**FindClosePrinterChangeNotification**函数（如 Windows SDK 文档中所述）。

 

 




