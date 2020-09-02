---
title: 对延迟的过程调用使用 __sdv_save_request 和 __sdv_retrieve_request
description: 对延迟的过程调用使用 __sdv_save_request 和 __sdv_retrieve_request
ms.assetid: 14d3a022-3e74-4526-9bf5-fee1ce36ac9e
keywords:
- __sdv_save_request
- __sdv_retrieve_request
- DeferredRequestCompleted
- AliasWithinTimerDpc
- AliasWithinDispatch
- 分析 Dpc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e49d7f6cb061003d1f694b0cd3c493f86abaf75
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382171"
---
# <a name="using-__sdv_save_request-and-__sdv_retrieve_request-for-deferred-procedure-calls"></a>使用 \_ \_ sdv \_ save \_ Request 和 \_ \_ sdv \_ 检索 \_ 延迟过程调用的请求


延迟过程调用 (Dpc) 静态驱动程序验证程序 (SDV) 面临的难题，因为这很难跟踪 framework 请求对象。 一种难点是，必须从全局指针（通常是从队列上下文）或从工作项检索请求。 为了克服这一困难，静态驱动程序验证程序提供了两个函数： ** \_ \_ sdv \_ save \_ request**和** \_ \_ sdv \_ 检索 \_ 请求**。 这些函数将延迟请求映射到 SDV 可以跟踪的请求。

** \_ \_ Sdv \_ save \_ 请求**和** \_ \_ sdv \_ 检索 \_ 请求**函数具有以下语法：

```
__sdv_save_request( request ) 
```

```
__sdv_retrieve_request( request ) 
```

其中， *request* 可以是任何框架请求对象的句柄。

这些函数仅供静态分析工具使用。 编译器将忽略这些函数。

下面的代码示例演示如何使用** \_ \_ sdv \_ save \_ 请求**和 \_ ** \_ sdv \_ 检索 \_ 请求**函数来指导 sdv，以便 sdv 可以映射延迟的请求。 SDV 可以使用此映射来验证 [DeferredRequestCompleted](./kmdf-deferredrequestcompleted.md) 规则。 DeferredRequestCompleted 规则要求** \_ \_ sdv \_ save \_ request**和 \_ ** \_ sdv \_ 检索 \_ 请求**出现在你的代码中。 有两个驱动程序属性规则 (**AliasWithinDispatch**， **AliasWithinTimerDpc**) 查找** \_ \_ sdv \_ save \_ 请求**和 \_ ** \_ sdv \_ 检索 \_ 请求**函数的存在。

在下面的代码示例中，函数 *EchoEvtIoRead* 是 [*EvtIoRead*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read) 事件回调函数，它将句柄保存到队列上下文区域中的框架请求对象。 函数 *EchoEvtTimerFunc* 是用于检索它的 [*EvtTimerFunc*](/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer) 事件回调函数。

```
VOID
EchoEvtIoRead(
 )in WDFQUEUE   Queue,
 __in WDFREQUEST Request,
 __in size_t      Length
    )
{
/* ..................... */
    // Mark the request as cancelable
    WdfRequestMarkCancelable(Request, EchoEvtRequestCancel);
 
 
    // Defer the completion to another thread from the timer DPC and save the handle to the framework request object by using the __sdv_save_request function. 
    queueContext->CurrentRequest = Request;    
 __sdv_save_request(Request);

    queueContext->CurrentStatus  = Status;

    return;
}
```

下面的代码示例演示** \_ \_ sdv \_ 检索 \_ 请求**函数如何映射现有请求，以便 sdv 可以跟踪该请求以完成。

```
VOID
EchoEvtTimerFunc(
    IN WDFTIMER     Timer
    )
{...................................................
    queue = WdfTimerGetParentObject(Timer);
    queueContext = QueueGetContext(queue);

    //
    // The DPC is automatically synchronized to the queue lock,
    // so this prevents race conditions from occurring without explicit driver-managed locking. The __sdv_retrieve_request function is used so that SDV can restore the deferred request in the timer DPC. Because we know that this deferred request is valid (because it has been previously saved), the __analysis_assume function is used to suppress false defects that might otherwise result in this code path.

    //
 __sdv_retrieve_request(queueContext->CurrentRequest);
    Request = queueContext->CurrentRequest;
 __analysis_assume(Request != NULL);
    if( Request != NULL ) {

        //
        // Try to remove cancel status from the request.
        //
        // The request is not completed if it is already canceled
        // because the EchoEvtIoCancel function has run, or is about to run,
        // and we are racing with it. 

        Status = WdfRequestUnmarkCancelable(Request);
// Because we know that the request is not NULL in this code path and that the request is no longer marked cancelable, we can use the __analysis_assume function to suppress the reporting of a false defect. 

 __analysis_assume(Status != STATUS_CANCELLED);
        if( Status != STATUS_CANCELLED ) {

            queueContext->CurrentRequest = NULL;
            Status = queueContext->CurrentStatus;

            KdPrint(("CustomTimerDPC Completing request 0x%p, Status 0x%x \n", Request,Status));

            WdfRequestComplete(Request, Status);
        }
        else {
            KdPrint(("CustomTimerDPC Request 0x%p is STATUS_CANCELLED, not completing\n",
                                Request));
        }
    }

    return;
}
```

 

