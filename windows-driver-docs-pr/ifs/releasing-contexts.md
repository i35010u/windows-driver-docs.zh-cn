---
title: 释放上下文
description: 释放上下文
keywords:
- 上下文 WDK 文件系统微筛选器，发布
- 释放上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: edc896f3fe871d5ee63446d883ee80b3c374fd1a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840719"
---
# <a name="releasing-contexts"></a>释放上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


微筛选器驱动程序通过调用 [**FltReleaseContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)来释放上下文。 对以下例程之一的每个成功调用最终必须通过调用 **FltReleaseContext** 进行匹配：

[**FltAllocateContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)

[**FltGetInstanceContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetinstancecontext)

[**FltGetFileContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetfilecontext)

[**FltGetStreamContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetstreamcontext)

[**FltGetStreamHandleContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetstreamhandlecontext)

[**FltGetTransactionContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgettransactioncontext)

[**FltGetVolumeContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetvolumecontext)

[**FltReferenceContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreferencecontext)

请注意， **FltSet**_Xxx_*_上下文_* 返回的 *OldContext* 指针和 [**FltDeleteContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletecontext)返回的 *上下文* 指针也必须在不再需要时释放。

在以下代码示例中，从 CTX 示例微筛选器驱动程序开始， **CtxInstanceSetup** 例程创建并设置实例上下文，然后调用 [**FltReleaseContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)：

```cpp
status = FltAllocateContext(
           FltObjects->Filter,           //Filter
           FLT_INSTANCE_CONTEXT,         //ContextType
           CTX_INSTANCE_CONTEXT_SIZE,    //ContextSize
           NonPagedPool,                 //PoolType
           &instanceContext);            //ReturnedContext
...
status = FltSetInstanceContext(
           FltObjects->Instance,              //Instance
           FLT_SET_CONTEXT_KEEP_IF_EXISTS,    //Operation
           instanceContext,                   //NewContext
           NULL);                             //OldContext

if (instanceContext != NULL) {
  FltReleaseContext(instanceContext);
}
return status;
```

请注意，无论调用 [**FltSetInstanceContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetinstancecontext)是否成功，都将调用 [**FltReleaseContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext) 。 在这两种情况下，调用方必须调用 **FltReleaseContext** 来释放由 [**FltAllocateContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext) (不 **FltSetInstanceContext**) 集的引用集。

如果已成功为实例设置上下文，则 [**FltSetInstanceContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetinstancecontext) 会将其自己的引用添加到实例上下文中。 因此，不再需要由 [**FltAllocateContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext) 设置的引用，并且对 [**FltReleaseContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext) 的调用会将其删除。

如果对 [**FltSetInstanceContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetinstancecontext) 的调用失败，则实例上下文只有一个引用，即 [**FltAllocateContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)设置的一个引用。 当 [**FltReleaseContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext) 返回时，实例上下文的引用计数为零，并由筛选器管理器释放。

 

