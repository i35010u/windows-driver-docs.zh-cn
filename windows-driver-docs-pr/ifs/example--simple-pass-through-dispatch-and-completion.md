---
title: 示例简单传递调度和完成
description: 示例简单传递调度和完成
ms.assetid: dae3a450-37b1-470b-a0f3-4108075e06ac
keywords:
- IRP 完成例程 WDK 文件系统，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3856021d75e23bdf78bf2034bbd113a2d57ae697
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386090"
---
# <a name="example-simple-pass-through-dispatch-and-completion"></a>例如：简单传递调度和完成


## <span id="ddk_example_simple_pass_through_dispatch_and_completion_if"></span><span id="DDK_EXAMPLE_SIMPLE_PASS_THROUGH_DISPATCH_AND_COMPLETION_IF"></span>


若要为 IRP 设置完成例程，并将向下传递 IRP，调度例程必须执行以下操作：

-   调用[ **IoCopyCurrentIrpStackLocationToNext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)将参数从当前的堆栈位置复制到的下一步低级驱动程序。

-   调用[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)来针对 IRP 指定完成例程。

-   调用[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)要传递到下一步低级驱动程序 IRP。

下面的代码示例说明了这种方法：

### <a name="span-iddispatchroutinespanspan-iddispatchroutinespanspan-iddispatchroutinespandispatch-routine"></a><span id="Dispatch_Routine"></span><span id="dispatch_routine"></span><span id="DISPATCH_ROUTINE"></span>调度例程

```cpp
IoCopyCurrentIrpStackLocationToNext( Irp ); 
IoSetCompletionRoutine( Irp,                                 // Irp
                        MyLegacyFilterPassThroughCompletion, // CompletionRoutine
                        (PVOID)recordList,                   // Context
                        TRUE,                                // InvokeOnSuccess
                        TRUE,                                // InvokeOnError
                        TRUE);                               // InvokeOnCancel
return IoCallDriver ( NextLowerDriverDeviceObject, Irp ); 
```

在此示例中，在调用[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine) IRP 设置完成例程。

对的调用中的前两个参数[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)是一个指向 IRP 和完成例程的名称。 第三个参数是指向驱动程序定义的结构，将传递给完成例程的指针。 此结构包含在它对 IRP 的执行完成处理时，将需要完成例程的上下文信息。 上下文结构必须分配从非分页缓冲池，因为可以在 IRQL 调度调用完成例程\_级别。

最后三个参数传递给[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)是标志，用于指定是否在 I/O 请求成功、 失败，或取消时调用完成例程。

### <a name="span-idcompletionroutinespanspan-idcompletionroutinespanspan-idcompletionroutinespancompletion-routine"></a><span id="Completion_Routine"></span><span id="completion_routine"></span><span id="COMPLETION_ROUTINE"></span>完成例程

如果调度例程设置完成例程，并立即返回之后调用[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) （如上面的调度例程所示），必须检查相应的完成例程IRP 的 PendingReturned 标记，并设置，如果调用**IoMarkIrpPending**。 然后它应返回状态\_成功后，如下面的示例中所示：

```cpp
if (Irp->PendingReturned) {
    IoMarkIrpPending( Irp );
}
return STATUS_SUCCESS;
```

### <a name="span-idadvantagesofthisapproachspanspan-idadvantagesofthisapproachspanspan-idadvantagesofthisapproachspanadvantages-of-this-approach"></a><span id="Advantages_of_This_Approach"></span><span id="advantages_of_this_approach"></span><span id="ADVANTAGES_OF_THIS_APPROACH"></span>此方法的优点

设置完成例程允许进一步处理 IRP，较低级别的驱动程序处理后的驱动程序。 完成例程可以决定如何处理 IRP 基于请求的 I/O 操作的结果。

### <a name="span-iddisadvantagesofthisapproachspanspan-iddisadvantagesofthisapproachspanspan-iddisadvantagesofthisapproachspandisadvantages-of-this-approach"></a><span id="Disadvantages_of_This_Approach"></span><span id="disadvantages_of_this_approach"></span><span id="DISADVANTAGES_OF_THIS_APPROACH"></span>这种方法的缺点

因为它在 IRQL 在任意线程上下文中运行&lt;= 调度\_级别，完成例程可以执行有限的处理 IRP。

 

 




