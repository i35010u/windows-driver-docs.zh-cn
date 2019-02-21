---
title: 取消 I/O 请求在 UMDF
description: 取消 I/O 请求在 UMDF
ms.assetid: 4f69903b-00ef-4b47-a564-aaa7d076481b
keywords:
- I/O 请求 WDK UMDF，取消
- 请求处理 WDK UMDF，取消请求
- 取消 I/O 请求 WDK UMDF
- 正在进行的请求 WDK UMDF
- I/O 请求 WDK UMDF，状态
- 请求处理 WDK UMDF，状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dae2371b14dac04042f3fa0b13291a698d064acc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543861"
---
# <a name="canceling-io-requests-in-umdf"></a>取消 I/O 请求在 UMDF


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

应用程序、 系统或驱动程序可以取消的设备正在进行 I/O 操作 （例如，若要从磁盘读取的多个块的请求）。 如果设备的 I/O 操作已取消，I/O 管理器将尝试取消与 I/O 操作相关联的所有未处理的 I/O 请求。 可以注册设备的驱动程序 I/O 管理器尝试取消 I/O 请求，驱动程序可以取消由他们拥有的请求时通知[完成](completing-i-o-requests.md)它们且完成状态的 HRESULT\_FROM\_WIN32 (错误\_操作\_ABORTED)。

该框架将处理一些基于框架的驱动程序的取消工作。 如果设备的 I/O 操作已取消，由框架完成-且完成状态的 HRESULT\_FROM\_WIN32 (错误\_操作\_ABORTED)-以下与关联的 I/O 请求已取消的操作：

-   未交付的 I/O 请求，该框架已放置在驱动程序的默认 I/O 队列。

-   未发送的 I/O 请求的框架已转发给另一个队列，因为该驱动程序调用[ **IWDFIoQueue::ConfigureRequestDispatching**](https://msdn.microsoft.com/library/windows/hardware/ff558946)。

框架将取消这些请求，因为它不会向驱动程序中提供它们。

框架已传递到驱动程序的 I/O 请求后，该驱动程序拥有该请求，框架不能取消。 在此情况下，只有驱动程序可以取消 I/O 请求，但框架必须通知该驱动程序应取消请求。 驱动程序收到此通知，从而[ **IRequestCallbackCancel::OnCancel** ](https://msdn.microsoft.com/library/windows/hardware/ff556903)回调函数。

有时一个驱动程序从 I/O 队列接收的 I/O 请求，但，而不是处理请求，该驱动程序请求对相同或另一个请求供以后处理的 I/O 队列。 例如，框架可能会将 I/O 请求传递到的一个驱动程序的请求处理程序，并且该驱动程序可能会随后调用[ **IWDFIoRequest::ForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff559081)以发出请求在其他队列或[ **IWDFIoRequest2::Requeue** ](https://msdn.microsoft.com/library/windows/hardware/ff559028)将请求放回同一个队列。

在这些情况下，框架可以取消 I/O 请求，因为请求 I/O 队列中。 但是，如果该驱动程序已注册的请求所在的 I/O 队列的回调函数，框架将调用的回调函数，而不是取消请求，正在取消关联的 I/O 操作时。 如果框架调用驱动程序的回调函数，该驱动程序必须取消请求。

总之，取消 I/O 操作时，框架始终会取消所有关联的 I/O 请求永远不会传递到驱动程序。 如果驱动程序收到的请求，然后请求该框架将取消请求 （如果请求在队列中） 除非驱动程序的 I/O 队列提供的回调函数。

### <a name="calling-markcancelable"></a>调用 MarkCancelable

驱动程序可以调用[ **IWDFIoRequest::MarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff559146)注册[ **IRequestCallbackCancel::OnCancel** ](https://msdn.microsoft.com/library/windows/hardware/ff556903)回调函数。 如果该驱动程序已调用**MarkCancelable**，和如果与请求关联的 I/O 操作已取消，框架将调用的驱动程序**OnCancel**回调函数，以便可以取消该驱动程序I/O 请求。

驱动程序应调用**MarkCancelable**如果它将拥有一个请求相对较长时间。 例如，驱动程序可能需要等待设备响应，或者它可能需要等待完成的请求的驱动程序创建一组的低级驱动程序收到一个请求。

如果驱动程序不会调用**MarkCancelable**，或如果驱动程序调用[ **IWDFIoRequest::UnmarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff559163)后调用**MarkCancelable**、 驱动程序并不知道的取消和因此句柄作为其请求通常的做法。

### <a name="calling-iscanceled"></a>调用 IsCanceled

如果驱动程序已不调用**MarkCancelable**注册**OnCancel**回调函数，它可以调用[ **IWDFIoRequest2::IsCanceled** ](https://msdn.microsoft.com/library/windows/hardware/ff559018)以确定 I/O 管理器已尝试取消 I/O 请求。 如果**IsCanceled**返回**TRUE**，驱动程序应取消请求。

例如，接收一个较大的驱动程序读取或它分解成多个较小的请求的写入请求可能会调用**IsCanceled**驱动程序的 I/O 目标完成的每个较小的请求，如果该驱动程序已不调用后**MarkCancelable**为收到的请求。

### <a name="canceling-the-request"></a>正在取消请求

正在取消 I/O 请求可能涉及以下任一项：

-   正在停止正在进行 I/O 操作。

-   不将请求转发到 I/O 目标。

-   调用[ **IWDFIoRequest::CancelSentRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559067)尝试取消该驱动程序之前必须提交到 I/O 目标的请求。

如果驱动程序正在取消从框架驱动程序收到一个请求对象的 I/O 请求，该驱动程序始终必须通过调用完成请求[ **IWDFIoRequest::Complete** ](https://msdn.microsoft.com/library/windows/hardware/ff559070)或[ **IWDFIoRequest::CompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff559074)，与*CompletionStatus* HRESULT 参数\_FROM\_WIN32(ERROR\_操作\_已中止)。 (如果该驱动程序调用[ **IWDFDevice::CreateRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff557021)若要创建一个请求对象，驱动程序调用[ **IWDFObject::DeleteWdfObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560210)而不是完成请求。)

 

 





