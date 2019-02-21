---
title: 完成 I/O 请求
description: 完成 I/O 请求
ms.assetid: ec5aef7a-110e-430c-902d-669ccc7095ac
keywords:
- I/O 请求 WDK KMDF，完成
- 完成 I/O 请求 WDK KMDF
- 请求处理 WDK KMDF，完成请求
- WDK KMDF，完成 I/O 请求的状态信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad08ed5b761578950db69174323bd4d7c2e3c2de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519360"
---
# <a name="completing-io-requests"></a>完成 I/O 请求





每个基于 framework 的驱动程序最终必须完成从框架接收的每个 I/O 请求。 驱动程序通过调用 request 对象的完成请求[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)， [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)，或[ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949)方法。

### <a name="when-to-complete-a-request"></a>何时完成请求

确定在以下情况之一为 true，驱动程序必须完成一个请求：

-   已成功完成请求的 I/O 操作。

-   请求的 I/O 操作已启动，但它完成之前失败。

-   请求的 I/O 操作不受支持，或在它接收的并且无法启动的时间无效。

-   请求的 I/O 操作已取消。

如果该驱动程序服务在设备上创建的 I/O 活动的 I/O 请求，该驱动程序通常会调用[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)从其[ *EvtInterruptDpc*](https://msdn.microsoft.com/library/windows/hardware/ff541721)或[ *EvtDpcFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541683)回调函数。

如果该驱动程序收到不受支持或无效请求，则通常会调用[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)从[请求处理程序](request-handlers.md)接收请求。

如果 I/O 操作[取消](canceling-i-o-requests.md)，该驱动程序通常会调用[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)从其[ *EvtRequestCancel*](https://msdn.microsoft.com/library/windows/hardware/ff541817)回调函数。

如果该驱动程序[转发](forwarding-i-o-requests.md)对的 I/O 请求[I/O 目标](using-i-o-targets.md)，驱动程序请求完成之后完成的 I/O 目标请求，按如下所示：

-   如果您的驱动程序将 I/O 请求转发[以同步方式](sending-i-o-requests-synchronously.md)到 I/O 目标，对 I/O 目标的驱动程序的调用后才会返回较低级驱动程序已完成请求 （除非出现错误）。 您的驱动程序 I/O 目标返回后，必须调用[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)。

-   如果您的驱动程序将 I/O 请求转发[异步](sending-i-o-requests-asynchronously.md)，想将您的驱动程序的较低级驱动程序完成请求时收到通知。 如果您的驱动程序注册[ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)回调函数，I/O 目标完成请求后框架调用此回调函数。 *CompletionRoutine*回调函数通常会调用[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)。

若要注册[ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)回调函数，该驱动程序必须调用[ **WdfRequestSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff550030)之前将转发到 I/O 的目标的 I/O 请求。

如果您的驱动程序不需要的 I/O 目标完成以异步方式转发的 I/O 请求时收到通知，该驱动程序无需注册[ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)回调函数。 相反，该驱动程序可以设置[ **WDF\_请求\_发送\_选项\_发送\_AND\_忘记**](https://msdn.microsoft.com/library/windows/hardware/ff552493)标记时调用[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)。 在这种情况下，驱动程序不会调用[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)。

驱动程序不会完成它已通过调用创建的 I/O 请求[ **WdfRequestCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff549951)或[ **WdfRequestCreateFromIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549953)。 相反，该驱动程序必须调用[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734) I/O 目标完成请求后通常删除请求对象。

例如，驱动程序可能会收到读取或写入请求的数据大于驱动程序的 I/O 目标可以处理一次。 该驱动程序必须将数据划分为多个较小请求，并将这些较小的请求发送到一个或多个 I/O 目标。 处理这种情况的方法包括：

-   调用[ **WdfRequestCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff549951)来创建一个额外的请求对象表示的较小的请求。

    该驱动程序可以向 I/O 目标以同步方式发送此请求。 较小请求[ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)回调函数可以调用[ **WdfRequestReuse** ](https://msdn.microsoft.com/library/windows/hardware/ff550026) ，以便可以重复使用该驱动程序请求并再次将其发送到 I/O 目标。 I/O 目标完成的较小的请求，最后一个后*CompletionRoutine*回调函数可以调用[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)删除驱动程序创建请求对象，该驱动程序可以调用[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)完成原始请求。

-   调用[ **WdfRequestCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff549951)来创建多个额外的请求对象，表示较小的请求。

    驱动程序的 I/O 目标可以以异步方式处理这些多个较小的请求。 该驱动程序可以注册[ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)为每个较小的请求的回调函数。 每次*CompletionRoutine*调用回调函数，它可以调用[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)删除驱动程序创建请求对象。 该驱动程序 I/O 目标完成所有较小的请求后，可以调用[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)完成原始请求。

### <a href="" id="providing-completion-information"></a> 提供完成信息

驱动程序完成请求，它可以根据需要提供其他驱动程序可以访问某些其他信息。 例如，驱动程序可能会提供已读取或写入请求传输的字节数。 若要提供此信息，该驱动程序可以执行以下任一操作：

-   调用[ **WdfRequestSetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff550032)之前调用[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)。

-   调用[ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)。

### <a href="" id="obtaining-completion-information"></a> 获取完成信息

若要获取有关另一个驱动程序已完成的 I/O 请求的信息，请将驱动程序可以：

-   调用[ **WdfRequestGetStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff549974)以获取它的调用时，较低级别驱动程序指定的完成状态值[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945).

-   调用[ **WdfRequestGetCompletionParams** ](https://msdn.microsoft.com/library/windows/hardware/ff549961)若要获取[ **WDF\_请求\_完成\_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552454)结构，其中包含有关已完成的请求，例如指向内存的句柄的其他信息对象，表示请求的缓冲区或特定于总线的信息。

    驱动程序可以调用[ **WdfRequestGetCompletionParams** ](https://msdn.microsoft.com/library/windows/hardware/ff549961)仅调用后[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)发送 I/O 请求同步或异步 I/O 目标。 该驱动程序不能调用**WdfRequestGetCompletionParams**它调用只能以同步方式将 I/O 请求发送到 I/O 目标的方法之一后 (如[ **WdfIoTargetSendReadSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548669)).

-   调用[ **WdfRequestGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549965)要获得它的调用时的较低级驱动程序指定的其他 I/O 完成信息[ **WdfRequestSetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff550032)或[ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)，如果驱动程序堆栈中的驱动程序提供此类信息。

如果驱动程序将以同步方式发送的 I/O 请求，则通常会调用[ **WdfRequestGetStatus**](https://msdn.microsoft.com/library/windows/hardware/ff549974)， [ **WdfRequestGetCompletionParams** ](https://msdn.microsoft.com/library/windows/hardware/ff549961)，并[ **WdfRequestGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549965)同步调用返回后。 如果驱动程序将以异步方式发送的 I/O 请求，则通常内会调用这些方法[ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)回调函数。

有关如何完成 I/O 请求的详细信息，请参阅[同步取消和完成代码](synchronizing-cancel-and-completion-code.md)。

 

 





