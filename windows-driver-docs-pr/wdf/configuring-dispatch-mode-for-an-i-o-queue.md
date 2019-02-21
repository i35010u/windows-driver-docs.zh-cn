---
title: 为 I/O 队列配置调度模式
description: 为 I/O 队列配置调度模式
ms.assetid: 7603c3fd-a4cb-4174-ad14-f57efedfe9de
keywords:
- 同步 WDK UMDF
- 队列调度模式 WDK UMDF
- 调度模式 WDK UMDF
- I/O 队列 WDK UMDF
- 队列 WDK UMDF
- 顺序调度模式 WDK UMDF
- 并行调度模式 WDK UMDF
- 手动调度模式 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36d441a6ad1f7746ec5a3e0efce4a89ef90e88e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526093"
---
# <a name="configuring-dispatch-mode-for-an-io-queue"></a>为 I/O 队列配置调度模式


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

当从应用程序的 I/O 请求到达时，框架会将每个请求放置在相应的 I/O 队列。 如何以及何时将请求传递到驱动程序依赖于驱动程序将调度 I/O 队列的配置以及如何驱动程序[指定的回调函数同步](specifying-a-callback-synchronization-mode.md)。 与即插即用还交互的 I/O 队列和电源管理子系统的 UMDF 来保存 I/O 请求在队列中直到设备达到适当的状态。

**请注意**  与不相关的 I/O 队列的调度模式[同步模式](specifying-a-callback-synchronization-mode.md)。 I/O 队列调度配置控制驱动程序可以接受进行处理，在任何给定时间，而同步控制事件回叫函数，演示或取消请求的同时执行的请求的数。 但是，通过创建多个操作模式[组合调度和同步模式](combining-dispatch-and-synchronization-modes.md)。

 

驱动程序配置时，驱动程序将调用调度 I/O 队列[ **IWDFDevice::CreateIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff557020)方法来配置默认的队列或创建辅助队列。 该驱动程序可以指定的值之一[ **WDF\_IO\_队列\_调度\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff552362)中的枚举类型*DispatchType*的参数**IWDFDevice::CreateIoQueue**确定调度模式。 [I/O 队列对象](framework-i-o-queue-object.md)可以支持以下调度模式：

-   顺序

    使用指定的顺序调度模式**WdfIoQueueDispatchSequential**值。 在调度此模式下，队列中的处理状态引发事件，以便将驱动程序仅一次处理一个请求。 队列延迟任何额外的请求，直到该驱动程序完成处理其当前请求或调用[ **IWDFIoRequest::ForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff559081)方法以将请求重新排队。 当当前请求完成，或转发时，队列将引发事件以提供下一个请求。

-   并行

    使用指定的并行调度模式**WdfIoQueueDispatchParallel**值。 在调度此模式下，队列中的处理状态引发事件，只要输入/输出请求已经可供该驱动程序。 当驱动程序收到的 I/O 请求时，该驱动程序可以通过以下方式之一处理 I/O 请求：

    -   该驱动程序拨打[ **IWDFIoRequest::Complete** ](https://msdn.microsoft.com/library/windows/hardware/ff559070)或[ **IWDFIoRequest::CompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559074)方法以完成立即 I/O 请求。 如果 I/O 请求无效，曾经无法进行维护，或者可以通过将数据从一个缓冲区或缓存数据复制完成，驱动程序将立即完成的 I/O 请求。
    -   驱动程序调用[ **IWDFIoRequest::ForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff559081)方法来重新排队 I/O 请求。
    -   驱动程序调用[ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)方法以将 I/O 请求传递到较低级别驱动程序。
-   Manual

    使用指定的手动调度模式**WdfIoQueueDispatchManual**值。 在调度此模式下，I/O 队列不会自动通知驱动程序的请求到达队列时。 该驱动程序必须调用[ **IWDFIoQueue::RetrieveNextRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff558967)方法来检索手动请求从队列。 这是轮询模型。

    在 UMDF 版本 1.9 及更高版本中，如果您的驱动程序使用手动调度模式下，它可以调用[ **IWDFIoRequest2::Requeue** ](https://msdn.microsoft.com/library/windows/hardware/ff559028) I/O 请求返回到从中驱动程序获取它的 I/O 队列的开头. 在调用**IWDFIoRequest2::Requeue**，驱动程序的下一步调用[ **IWDFIoQueue::RetrieveNextRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff558967)检索重新排队的请求。

对于所有调度模式， [I/O 队列对象](framework-i-o-queue-object.md)接收并跟踪请求，直到该驱动程序处理请求或会取消该请求。

如果该驱动程序将配置为用于串行或并行调度队列，框架将通知请求通过该驱动程序创建的队列或将配置默认的队列时由驱动程序进行注册的回调函数的驱动程序。 有关详细信息，请参阅[I/O 队列事件回调函数](i-o-queue-event-callback-functions.md)。

 

 





