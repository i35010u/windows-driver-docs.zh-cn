---
title: 同步取消和完成代码
description: 同步取消和完成代码
ms.assetid: 4c302fc5-cb14-46e5-80c8-8dbf62486905
keywords:
- 请求处理 WDK KMDF，取消请求
- I/o 请求 WDK KMDF，取消
- 同步 WDK KMDF
- 完成 i/o 请求 WDK KMDF
- 请求处理 WDK KMDF，同步
- I/o 请求 WDK KMDF，同步
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03e37cf0ea5e71db85410bc0c594a749f5d4b132
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831662"
---
# <a name="synchronizing-cancel-and-completion-code"></a>同步取消和完成代码





如果你的驱动程序调用[**WdfRequestMarkCancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)或[**WdfRequestMarkCancelableEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)来取消 i/o 请求，则可能存在同步问题。 例如，驱动程序和设备可能通过[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)和[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数以异步方式执行设备 I/o 操作，并且*EvtInterruptDpc*和[*EvtRequestCancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)回调函数可能包含对[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)的调用。

驱动程序只能调用一次[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) ，以完成或取消请求。 但是，如果[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)和[*EvtRequestCancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)回调函数不彼此同步，则框架可以调用另一个函数，而不是另一个执行。

如果驱动程序使用框架的[自动同步](using-automatic-synchronization.md)，则可轻松避免此问题，因为自动同步可确保每次调用一个回调函数。

如果你的驱动程序未使用框架的自动同步，则它可以使用[框架锁](using-framework-locks.md)来同步取消和完成代码。

无论驱动程序使用框架的自动同步还是提供自己的同步，驱动程序的[*EvtRequestCancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)回调函数都必须调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)来取消请求。 驱动程序的[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数应调用[**WdfRequestUnmarkCancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable) ，如下所示：

```cpp
Status = WdfRequestUnmarkCancelable(Request);
if( Status != STATUS_CANCELLED ) {
    WdfRequestComplete(Request, RequestStatus);
    }
```

此代码可确保当驱动程序已调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)来取消请求时，驱动程序不会调用来完成请求。

有关当驱动程序调用**WdfRequestUnmarkCancelable**时必须遵循的规则的详细信息，请参阅[**WdfRequestUnmarkCancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable)。

 

 





