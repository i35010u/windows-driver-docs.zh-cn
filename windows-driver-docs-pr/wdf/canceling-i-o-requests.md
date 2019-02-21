---
title: 取消 I/O 请求
description: 取消 I/O 请求
ms.assetid: 9a486fa4-7fd3-4433-88aa-34a54d9b1e16
keywords:
- 请求处理 WDK KMDF、 取消请求
- I/O 请求 WDK KMDF，取消
- 取消 I/O 请求 WDK KMDF
- 未交付的 I/O 请求 WDK KMDF
- 转发 I/O 请求 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b6859211afb123d3bc10039a67a203fe4490892
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543153"
---
# <a name="canceling-io-requests"></a>取消 I/O 请求





应用程序、 系统或驱动程序可以取消的设备正在进行 I/O 操作 （例如，若要从磁盘读取的多个块的请求）。 如果设备的 I/O 操作已取消，I/O 管理器将尝试取消与 I/O 操作相关联的所有未处理的 I/O 请求。 可以注册设备的驱动程序 I/O 管理器尝试取消 I/O 请求，驱动程序可以取消由他们拥有的请求时通知[完成](completing-i-o-requests.md)且完成状态的状态对其\_已取消。

该框架将处理一些基于框架的驱动程序的取消工作。 如果设备的 I/O 操作已取消，由框架完成以下的 I/O 请求 (且完成状态的状态\_已取消) 与已取消操作相关联的：

-   未交付的 I/O 请求，该框架已放置在驱动程序的默认 I/O 队列。

-   未发送的 I/O 请求的框架已转发给另一个队列，因为该驱动程序调用[ **WdfDeviceConfigureRequestDispatching**](https://msdn.microsoft.com/library/windows/hardware/ff545920)。

框架将取消这些请求，因为它不会向驱动程序中提供它们。

该框架已传递到驱动程序，该驱动程序的 I/O 请求后[拥有](request-ownership.md)请求和 framework 无法取消。 在此情况下，只有驱动程序可以取消 I/O 请求，但框架必须通知该驱动程序应取消请求。 驱动程序收到此通知，从而[ *EvtRequestCancel* ](https://msdn.microsoft.com/library/windows/hardware/ff541817)回调函数。

有时一个驱动程序从 I/O 队列接收的 I/O 请求，但，而不是处理请求，该驱动程序请求对相同或另一个请求供以后处理的 I/O 队列。 这种情况的示例包括：

-   框架将 I/O 请求传递到的驱动程序之一[请求处理程序](request-handlers.md)，，并且该驱动程序随后调用任一[ **WdfRequestForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff549958) （或[**WdfRequestForwardToParentDeviceIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549959)) 将请求放在其他队列或[ **WdfRequestRequeue** ](https://msdn.microsoft.com/library/windows/hardware/ff550012)放置请求返回到同一个队列。

-   该框架将 I/O 请求传递到驱动程序的[ *EvtIoInCallerContext* ](https://msdn.microsoft.com/library/windows/hardware/ff541764)回调函数、 驱动程序调用[ **WdfDeviceEnqueueRequest**](https://msdn.microsoft.com/library/windows/hardware/ff545945)传递请求重新至框架，和框架随后将请求放入驱动程序的 I/O 队列之一。

在这些情况下，框架可以取消 I/O 请求，因为请求 I/O 队列中。 但是，如果该驱动程序已注册[ *EvtIoCanceledOnQueue* ](https://msdn.microsoft.com/library/windows/hardware/ff541756)请求所在的 I/O 队列的回调函数，框架将调用的回调函数，而不是取消正在取消关联的 I/O 操作时请求。 如果框架将调用的驱动程序*EvtIoCanceledOnQueue*回调函数，该驱动程序必须[完整](completing-i-o-requests.md)请求。

总之，取消 I/O 操作时，框架始终会取消所有关联的 I/O 请求永远不会传递到驱动程序。 如果该驱动程序收到的请求，然后请求该框架将取消请求 （如果请求在队列中） 除非驱动程序提供了[ *EvtIoCanceledOnQueue* ](https://msdn.microsoft.com/library/windows/hardware/ff541756)回调函数I/O 队列中。

### <a name="calling-wdfrequestmarkcancelable-or-wdfrequestmarkcancelableex"></a>调用 WdfRequestMarkCancelable 或 WdfRequestMarkCancelableEx

驱动程序可以调用[ **WdfRequestMarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff549983)或[ **WdfRequestMarkCancelableEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549984)注册[ *EvtRequestCancel* ](https://msdn.microsoft.com/library/windows/hardware/ff541817)回调函数。 如果该驱动程序已调用**WdfRequestMarkCancelable**或**WdfRequestMarkCancelableEx**，和如果与请求关联的 I/O 操作已取消，框架将调用在驱动程序*EvtRequestCancel*回调函数，该驱动程序可以取消 I/O 请求。

驱动程序应调用[ **WdfRequestMarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff549983)或[ **WdfRequestMarkCancelableEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549984)如果它将拥有的请求相对长时间。 例如，驱动程序可能需要等待设备响应，或者它可能会等待较低的驱动程序来完成的请求的驱动程序创建一组收到一个请求。

如果驱动程序不会调用[ **WdfRequestMarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff549983)或[ **WdfRequestMarkCancelableEx**](https://msdn.microsoft.com/library/windows/hardware/ff549984)，或如果驱动程序调用[ **WdfRequestUnmarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff550035)后调用**WdfRequestMarkCancelable**或者**WdfRequestMarkCancelableEx**，驱动程序不能识别的取消操作并因此将和往常一样处理该请求。

### <a name="calling-wdfrequestiscanceled"></a>调用 WdfRequestIsCanceled

如果驱动程序已不调用[ **WdfRequestMarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff549983)或[ **WdfRequestMarkCancelableEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549984)注册[*EvtRequestCancel* ](https://msdn.microsoft.com/library/windows/hardware/ff541817)回调函数，它可以调用[ **WdfRequestIsCanceled** ](https://msdn.microsoft.com/library/windows/hardware/ff549976)以确定是否已尝试在 I/O 管理器取消 I/O 请求。 如果**WdfRequestIsCanceled**返回**TRUE**和驱动程序拥有该请求，该驱动程序应取消请求。 如果该驱动程序不拥有该请求，则不应调用**WdfRequestIsCanceled**。

但调用的驱动程序[ **WdfRequestMarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff549983)或[ **WdfRequestMarkCancelableEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549984)可能调用[**WdfRequestIsCanceled** ](https://msdn.microsoft.com/library/windows/hardware/ff549976)在以下情况下：

-   等待设备中断可能会调用一个驱动程序[ **WdfRequestIsCanceled** ](https://msdn.microsoft.com/library/windows/hardware/ff549976)从其[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)回调函数。

-   轮询其设备的驱动程序可能会调用[ **WdfRequestIsCanceled** ](https://msdn.microsoft.com/library/windows/hardware/ff549976)从它的轮询线程。

-   驱动程序，可断开[DMA 事务](dma-transactions-and-dma-transfers.md)多个较小的传送到可能会调用[ **WdfRequestIsCanceled** ](https://msdn.microsoft.com/library/windows/hardware/ff549976)每次传输完成之后。

-   接收一个较大的驱动程序读取或写入它分解成多个较小的请求的请求可能会调用[ **WdfRequestIsCanceled** ](https://msdn.microsoft.com/library/windows/hardware/ff549976)驱动程序的 I/O 目标完成每个较小的请求后如果该驱动程序已不调用[ **WdfRequestMarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff549983)或[ **WdfRequestMarkCancelableEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549984)的接收请求。

### <a name="canceling-the-request"></a>正在取消请求

正在取消 I/O 请求可能涉及以下任一项：

-   正在停止正在进行 I/O 操作。

-   不将请求转发到 I/O 目标。

-   调用[ **WdfRequestCancelSentRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff549941)尝试取消该驱动程序之前必须提交到 I/O 目标的请求。

如果驱动程序正在取消从框架驱动程序收到一个请求对象的 I/O 请求，该驱动程序始终必须通过调用完成请求[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)， [**WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)，或[ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)，与*状态*参数的状态\_已取消。 (如果该驱动程序调用[ **WdfRequestCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff549951)若要创建一个请求对象，驱动程序调用[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)而不是完成请求。）

### <a name="synchronizing-cancellation"></a>正在取消同步

有关同步取消 I/O 请求的代码的信息，请参阅：

-   [同步取消和完成代码](synchronizing-cancel-and-completion-code.md)

-   [同步发送的请求取消](synchronizing-cancellation-of-sent-requests.md)

 

 





