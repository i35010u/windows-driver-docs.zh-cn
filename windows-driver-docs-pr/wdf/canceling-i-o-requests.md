---
title: 取消 I/O 请求
description: 取消 I/O 请求
ms.assetid: 9a486fa4-7fd3-4433-88aa-34a54d9b1e16
keywords:
- 请求处理 WDK KMDF，取消请求
- I/o 请求 WDK KMDF，取消
- 取消 i/o 请求 WDK KMDF
- 未发送的 i/o 请求 WDK KMDF
- 转发 i/o 请求 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b5a0467edb6de7b1a65b41eab107d8ad9bba447
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187071"
---
# <a name="canceling-io-requests"></a>取消 I/O 请求





设备的正在进行的 i/o 操作 (如从磁盘读取多个块的请求) 可以由应用程序、系统或驱动程序取消。 如果设备的 i/o 操作被取消，则 i/o 管理器会尝试取消与 i/o 操作关联的所有未处理的 i/o 请求。 当 i/o 管理器尝试取消 i/o 请求时，设备的驱动程序可以注册通知，并且驱动程序可以通过完成状态为 "已取消" 的 [请求来取消](completing-i-o-requests.md) 它们所拥有的请求 \_ 。

框架处理基于框架的驱动程序的一些取消工作。 如果设备的 i/o 操作被取消，则框架将完成以下 i/o 请求，这些请求的完成状态为 \_ "已) 取消"、"已取消"、"已取消" (状态：

-   未传递的 i/o 请求，框架已置于驱动程序的默认 i/o 队列中。

-   由于驱动程序名为 [**WdfDeviceConfigureRequestDispatching**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)，框架已转发到另一个队列的未送达 i/o 请求。

由于框架会取消这些请求，因此它不会将这些请求传递给驱动程序。

在框架向驱动程序提供了 i/o 请求后，该驱动程序将 [拥有](request-ownership.md) 该请求，并且框架将无法取消该请求。 此时，只有驱动程序可以取消 i/o 请求，但框架必须通知驱动程序应取消请求。 驱动程序通过提供 [*EvtRequestCancel*](/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel) 回调函数接收此通知。

有时，驱动程序从 i/o 队列接收 i/o 请求，而不是处理该请求，驱动程序会将请求会到同一个或另一个 i/o 队列，以供以后处理。 这种情况的示例包括：

-   该框架将 i/o 请求传递给某个驱动程序的 [请求处理程序](request-handlers.md)，驱动程序随后调用 [**WdfRequestForwardToIoQueue**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue) (或 [**WdfRequestForwardToParentDeviceIoQueue**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoparentdeviceioqueue)) 将请求放在不同的队列或 [**WdfRequestRequeue**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestrequeue) 中，以便将请求放回同一队列。

-   此框架向驱动程序的 [*EvtIoInCallerContext*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context) 回调函数提供 i/o 请求，驱动程序调用 [**WdfDeviceEnqueueRequest**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest) 将该请求传递回框架，然后框架会将该请求放入驱动程序的一个 i/o 队列。

在这些情况下，框架可以取消 i/o 请求，因为该请求在 i/o 队列中。 但是，如果驱动程序为请求所在的 i/o 队列注册了 [*EvtIoCanceledOnQueue*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue) 回调函数，则在取消关联的 i/o 操作时，框架将调用回调函数，而不是取消该请求。 如果框架调用驱动程序的 *EvtIoCanceledOnQueue* 回调函数，则驱动程序必须 [完成](completing-i-o-requests.md) 该请求。

概括而言，当 i/o 操作被取消时，框架始终会取消从未传递到该驱动程序的所有关联 i/o 请求。 如果驱动程序收到请求，然后将其会，则框架将取消请求 (如果该请求在队列中) ，除非该驱动程序为 i/o 队列提供 [*EvtIoCanceledOnQueue*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue) 回调函数。

### <a name="calling-wdfrequestmarkcancelable-or-wdfrequestmarkcancelableex"></a>调用 WdfRequestMarkCancelable 或 WdfRequestMarkCancelableEx

驱动程序可以调用 [**WdfRequestMarkCancelable**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable) 或 [**WdfRequestMarkCancelableEx**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex) 来注册 [*EvtRequestCancel*](/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel) 回调函数。 如果驱动程序调用了 **WdfRequestMarkCancelable** 或 **WdfRequestMarkCancelableEx**，并且与该请求关联的 i/o 操作被取消，则框架将调用该驱动程序的 *EvtRequestCancel* 回调函数，以便驱动程序可以取消 i/o 请求。

如果驱动程序将拥有相对较长时间的请求，则应调用 [**WdfRequestMarkCancelable**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable) 或 [**WdfRequestMarkCancelableEx**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex) 。 例如，驱动程序可能需要等待设备响应，或者等待较低的驱动程序完成收到单个请求时驱动程序创建的一组请求。

如果驱动程序没有调用[**WdfRequestMarkCancelable**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)或[**WdfRequestMarkCancelableEx**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)，或者如果驱动程序在调用**WdfRequestMarkCancelable**或**WdfRequestMarkCancelableEx**后调用[**WdfRequestUnmarkCancelable**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable) ，则驱动程序将不知道取消操作，因此会像往常一样处理请求。

### <a name="calling-wdfrequestiscanceled"></a>调用 WdfRequestIsCanceled

如果驱动程序没有调用 [**WdfRequestMarkCancelable**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable) 或 [**WdfRequestMarkCancelableEx**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex) 来注册 [*EvtRequestCancel*](/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel) 回调函数，它可以调用 [**WdfRequestIsCanceled**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestiscanceled) 来确定 i/o 管理器是否已尝试取消 i/o 请求。 如果 **WdfRequestIsCanceled** 返回 **TRUE** ，并且驱动程序拥有请求，则驱动程序应取消请求。 如果驱动程序没有该请求，则不应调用 **WdfRequestIsCanceled**。

未调用 [**WdfRequestMarkCancelable**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable) 或 [**WdfRequestMarkCancelableEx**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex) 的驱动程序在以下情况下可能会调用 [**WdfRequestIsCanceled**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestiscanceled) ：

-   等待设备中断的驱动程序可能会从其[*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数调用[**WdfRequestIsCanceled**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestiscanceled) 。

-   轮询其设备的驱动程序可能会从它的轮询线程中调用 [**WdfRequestIsCanceled**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestiscanceled) 。

-   在每次传输完成后，将 [DMA 事务](dma-transactions-and-dma-transfers.md) 分为多个较小的传输的驱动程序可能会调用 [**WdfRequestIsCanceled**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestiscanceled) 。

-   当驱动程序的 i/o 目标完成每个较小的请求时，如果驱动程序没有为收到的请求调用[**WdfRequestMarkCancelable**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)或[**WdfRequestMarkCancelableEx**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex) ，则接收到多个较小的请求的请求可能会在驱动程序的 i/o 目标完成每个较小的请求后调用[**WdfRequestIsCanceled**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestiscanceled) 。

### <a name="canceling-the-request"></a>正在取消请求

取消 i/o 请求可能需要执行以下任一操作：

-   正在停止正在进行的 i/o 操作。

-   不要将请求转发到 i/o 目标。

-   调用 [**WdfRequestCancelSentRequest**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcancelsentrequest) ，尝试取消驱动程序之前已提交到 i/o 目标的请求。

如果驱动程序取消了驱动程序从框架收到的请求对象的 i/o 请求，则驱动程序必须始终通过调用 [**WdfRequestComplete**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)、 [**WdfRequestCompleteWithInformation**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)或 [**WdfRequestCompleteWithPriorityBoost**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)来完成请求， *状态* 参数为 "已 \_ 取消"。  (如果驱动程序调用 [**WdfRequestCreate**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate) 来创建请求对象，则驱动程序将调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) ，而不是完成请求。 ) 

### <a name="synchronizing-cancellation"></a>正在同步取消

有关对取消 i/o 请求的代码进行同步的信息，请参阅：

-   [同步取消和完成代码](synchronizing-cancel-and-completion-code.md)

-   [将取消已发送请求的操作同步](synchronizing-cancellation-of-sent-requests.md)

 

