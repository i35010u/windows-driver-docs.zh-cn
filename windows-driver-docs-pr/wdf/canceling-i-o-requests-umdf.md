---
title: 在 UMDF 中取消 i/o 请求
description: 在 UMDF 中取消 i/o 请求
ms.assetid: 4f69903b-00ef-4b47-a564-aaa7d076481b
keywords:
- I/o 请求 WDK UMDF，取消
- 请求处理 WDK UMDF，取消请求
- 取消 i/o 请求 WDK UMDF
- 正在进行的请求 WDK UMDF
- I/o 请求 WDK UMDF，状态
- 请求处理 WDK UMDF，状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b472620cccfccbc652e8d024c91fcdbc49b02a60
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210235"
---
# <a name="canceling-io-requests-in-umdf"></a>在 UMDF 中取消 i/o 请求


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

设备的正在进行的 i/o 操作（如从磁盘读取多个块的请求）可以被应用程序、系统或驱动程序取消。 如果设备的 i/o 操作被取消，则 i/o 管理器会尝试取消与 i/o 操作关联的所有未处理的 i/o 请求。 当 i/o 管理器尝试取消 i/o 请求时，设备的驱动程序可以注册以获得通知，并且驱动程序可以通过完成状态为 "HRESULT\_\_" 的完成状态（错误\_操作\_"已中止"）[来取消其](completing-i-o-requests.md)所需的请求。

框架处理基于框架的驱动程序的一些取消工作。 如果某个设备的 i/o 操作被取消，则该框架将完成：从\_WIN32 完成状态为 HRESULT\_（错误\_操作\_已中止）--与取消的操作关联的以下 i/o 请求：

-   未传递的 i/o 请求，框架已置于驱动程序的默认 i/o 队列中。

-   由于驱动程序名为[**IWDFIoQueue：： ConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfioqueue-configurerequestdispatching)，框架已转发到另一个队列的未送达 i/o 请求。

由于框架会取消这些请求，因此它不会将这些请求传递给驱动程序。

在框架向驱动程序提供了 i/o 请求后，该驱动程序将拥有该请求，并且框架将无法取消该请求。 此时，只有驱动程序可以取消 i/o 请求，但框架必须通知驱动程序应取消请求。 驱动程序通过提供[**IRequestCallbackCancel：： OnCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackcancel-oncancel)回调函数接收此通知。

有时，驱动程序从 i/o 队列接收 i/o 请求，而不是处理该请求，驱动程序会将请求会到同一个或另一个 i/o 队列，以供以后处理。 例如，该框架可能会向某个驱动程序的请求处理程序提供 i/o 请求，驱动程序随后可以调用[**IWDFIoRequest：： ForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-forwardtoioqueue)将该请求放在不同的队列中，或使用[**IWDFIoRequest2：：重新排队**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-requeue)将请求放回同一队列。

在这些情况下，框架可以取消 i/o 请求，因为该请求在 i/o 队列中。 但是，如果驱动程序为请求所在的 i/o 队列注册了一个回调函数，则在取消关联的 i/o 操作时，框架将调用回调函数，而不是取消该请求。 如果框架调用驱动程序的回调函数，则驱动程序必须取消该请求。

概括而言，当 i/o 操作被取消时，框架始终会取消从未传递到该驱动程序的所有关联 i/o 请求。 如果驱动程序收到请求，然后将其会，则框架将取消请求（如果请求在队列中），除非驱动程序为 i/o 队列提供回调函数。

### <a name="calling-markcancelable"></a>调用 MarkCancelable

驱动程序可以调用[**IWDFIoRequest：： MarkCancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-markcancelable)来注册[**IRequestCallbackCancel：： OnCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackcancel-oncancel)回调函数。 如果驱动程序调用了**MarkCancelable**，并且与该请求关联的 i/o 操作被取消，则框架将调用驱动程序的**OnCancel**回调函数，以便驱动程序可以取消 i/o 请求。

如果驱动程序将拥有相对较长时间的请求，则应调用**MarkCancelable** 。 例如，驱动程序可能需要等待设备响应，或者可能需要等待较低的驱动程序来完成收到单个请求时驱动程序创建的一组请求。

如果驱动程序未调用**MarkCancelable**，或者如果驱动程序在调用**MarkCancelable**后调用[**IWDFIoRequest：： UnmarkCancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-unmarkcancelable) ，则驱动程序将无法识别取消，因此处理请求的方式通常为。

### <a name="calling-iscanceled"></a>调用 T.iscanceled

如果驱动程序没有调用**MarkCancelable**来注册**OnCancel**回调函数，它可以调用[**IWDFIoRequest2：： T.iscanceled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-iscanceled)来确定 i/o 管理器是否已尝试取消 i/o 请求。 如果**t.iscanceled**返回**TRUE**，则驱动程序应取消请求。

例如，当驱动程序的 i/o 目标完成了每个较小的请求时，如果驱动程序没有为收到的请求调用**MarkCancelable** ，则接收到多个较小的请求的驱动程序将会调用**t.iscanceled** 。

### <a name="canceling-the-request"></a>正在取消请求

取消 i/o 请求可能需要执行以下任一操作：

-   正在停止正在进行的 i/o 操作。

-   不要将请求转发到 i/o 目标。

-   调用[**IWDFIoRequest：： CancelSentRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-cancelsentrequest)可尝试取消驱动程序之前已提交到 i/o 目标的请求。

如果驱动程序取消了驱动程序从框架收到的请求对象的 i/o 请求，则驱动程序必须始终通过调用[**IWDFIoRequest：： complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete)或[**IWDFIoRequest：： CompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)来完成请求，并通过\_WIN32 中的*CompletionStatus*参数\_\_操作\_中止）。 （如果驱动程序调用[**IWDFDevice：： CreateRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest)来创建请求对象，则驱动程序将调用[**IWDFObject：:D eletewdfobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject) ，而不是完成请求。）

 

 





