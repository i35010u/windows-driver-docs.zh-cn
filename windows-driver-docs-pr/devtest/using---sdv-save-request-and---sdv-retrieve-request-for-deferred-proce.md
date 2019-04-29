---
title: 使用 __sdv_save_request 和 __sdv_retrieve_request 延缓的过程调用
description: 对延迟的过程调用使用 __sdv_save_request 和 __sdv_retrieve_request
ms.assetid: 14d3a022-3e74-4526-9bf5-fee1ce36ac9e
keywords:
- __sdv_save_request
- __sdv_retrieve_request
- DeferredRequestCompleted
- AliasWithinTimerDpc
- AliasWithinDispatch
- 分析 dpc 进行标记
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b15e8f76027bc25c168d4d993652bfc671223c6a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341647"
---
# <a name="using-sdvsaverequest-and-sdvretrieverequest-for-deferred-procedure-calls"></a>使用\_ \_sdv\_保存\_请求并\_ \_sdv\_检索\_延迟过程调用的请求


延迟过程调用 (Dpc) 存在挑战到 Static Driver Verifier (SDV)，因为很难跟踪框架请求对象。 一个难点是从全局指针，通常从队列的上下文中，或从工作项，必须检索该请求。 为了克服这个困难，Static Driver Verifier 提供了两个函数：  **\_ \_sdv\_保存\_请求**，以及 **\_ \_sdv\_检索\_请求**。 这些函数将延迟的请求映射到 SDV 可以跟踪的请求。

 **\_ \_Sdv\_保存\_请求**，以及 **\_ \_sdv\_检索\_请求**函数具有以下语法：

```
__sdv_save_request( request ) 
```

```
__sdv_retrieve_request( request ) 
```

其中*请求*可以是任何 framework 请求对象的句柄。

这些函数仅供静态分析工具。 编译器将忽略函数。

下面的代码示例演示如何 **\_ \_sdv\_保存\_请求**并\_  **\_sdv\_检索\_请求**函数用于指导 SDV，以便 SDV 可以映射延迟的请求。 SDV 可以使用此映射来验证[DeferredRequestCompleted](https://msdn.microsoft.com/library/windows/hardware/ff544670)规则。 DeferredRequestCompleted 规则需要 **\_ \_sdv\_保存\_请求**并\_  **\_sdv\_检索\_请求**出现在你的代码。 规则有两个驱动程序属性 (**AliasWithinDispatch**， **AliasWithinTimerDpc**)，查看是否存在 **\_ \_sdv\_保存\_请求**并\_  **\_sdv\_检索\_请求**函数。

在下面的代码示例，该函数*EchoEvtIoRead*是[ *EvtIoRead* ](https://msdn.microsoft.com/library/windows/hardware/ff541776)保存对 framework 请求对象的句柄的事件的回调函数队列的上下文区域。 该函数*EchoEvtTimerFunc*是[ *EvtTimerFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541823)检索它的事件的回调函数。

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

下面的代码示例演示了如何 **\_ \_sdv\_检索\_请求**函数将映射现有请求，以便 SDV 可以跟踪它的完成情况。

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

 

 





