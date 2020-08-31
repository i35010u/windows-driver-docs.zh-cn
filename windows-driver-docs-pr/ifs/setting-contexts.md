---
title: 设置上下文
description: 设置上下文
ms.assetid: 3daa23e6-14d7-4d35-8bc8-695296cd289d
keywords:
- 上下文 WDK 文件系统微筛选器，设置
- 附加上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8522934b3545efacc153edf58e0bcbf1c5fbee94
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89062986"
---
# <a name="setting-contexts"></a>设置上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


创建新上下文后，微筛选器驱动程序可以通过调用 **FltSet***xxx***上下文**将其附加到对象，其中 *Xxx* 是上下文类型。

如果**FltSet***Xxx***上下文**例程的*Operation*参数设置为 FLT \_ ，则 \_ \_ \_ 如果 \_ 存在， **FltSet***Xxx***上下文**将仅在微筛选器驱动程序尚未设置对象的上下文时将新分配的上下文附加到对象。 如果微筛选器驱动程序已设置上下文，则 **FltSet***Xxx***上下文** 返回状态 \_ FLT \_ 上下文 \_ 已 \_ 定义，这是一个 NTSTATUS 错误代码，并且不会替换现有的上下文。 如果**FltSet***Xxx***上下文**例程的*OldContext*参数为非**NULL**，则它将接收指向现有上下文的指针。 如果不再需要此指针，微筛选器驱动程序必须通过调用 [**FltReleaseContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)来释放它。

如果 *Operation* 参数设置为 FLT \_ \_ \_ \_ \_ ，如果存在，则 **FltSet***Xxx***上下文** 始终将新上下文附加到对象。 如果微筛选器驱动程序已设置上下文， **FltSet***Xxx***上下文** 会删除现有上下文，设置新上下文并递增引用计数。 如果 *OldContext* 参数为非**NULL**，则它将接收指向已删除上下文的指针。 如果不再需要此指针，微筛选器驱动程序必须通过调用 **FltReleaseContext**来释放它。

在以下代码示例中，从 CTX 示例微筛选器驱动程序开始， **CtxInstanceSetup** 例程创建并设置实例上下文：

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

请注意，调用 [**FltSetInstanceContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetinstancecontext)后，调用 **FltReleaseContext** ，以释放 ([**FltAllocateContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext) 设置的引用计数，而 *不*是 **FltSetInstanceContext**) 。 这在 [发布上下文](releasing-contexts.md)中进行了介绍。

 

