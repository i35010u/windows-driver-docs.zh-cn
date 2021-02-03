---
title: 设置上下文
description: 设置上下文
keywords:
- 上下文 WDK 文件系统微筛选器，设置
- 附加上下文
ms.date: 01/22/2021
ms.localizationpriority: medium
ms.openlocfilehash: b5c4ace5a5b81ff4f200cb8c1226bc45d7c09b87
ms.sourcegitcommit: 204ed37ede1cd462ef6f6c9211a223fd304da4a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2021
ms.locfileid: "99502052"
---
# <a name="setting-contexts"></a>设置上下文

[创建新上下文](creating-contexts.md)后，微筛选器驱动程序可以通过调用以下 set 例程之一将其附加到对象：

- [**FltSetFileContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetfilecontext)
- [**FltSetInstanceContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetinstancecontext)
- [**FltSetStreamContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetstreamcontext)
- [**FltSetStreamHandleContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetstreamhandlecontext)
- [**FltSetTransactionContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsettransactioncontext)
- [**FltSetVolumeContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetvolumecontext)

设置例程根据 *Operation* 参数的值执行以下操作：

- 如果 **操作**  ==  **FLT_SET_CONTEXT_KEEP_IF_EXISTS**：
  - 如果微筛选器尚未设置对象的相同类型的上下文，则设置例程：
    - 将新分配的上下文附加到对象。
    - 递增引用计数。
  - 否则，如果微筛选器已设置上下文，则设置例程：
    - 返回)  (NTSTATUS 错误代码 STATUS_FLT_CONTEXT_ALREADY_DEFINED。
    - 不会替换现有的上下文。
    - 不递增引用计数。
    - 如果 *OldContext* 参数为非 **NULL**，则存储指向其现有上下文的指针。 如果不再需要此指针，微筛选器驱动程序必须通过调用 [**FltReleaseContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)来释放它。

- 如果 **操作**  ==  **FLT_SET_CONTEXT_REPLACE_IF_EXISTS**：
  - 设置例程始终将新上下文附加到对象。
  - 如果微筛选器驱动程序已设置上下文，则设置例程：
    - 删除现有上下文，设置新上下文，并递增新上下文上的引用计数。
    - 如果 *OldContext* 参数为非 **NULL**，则它将接收指向已删除上下文的指针。 如果不再需要此指针，微筛选器驱动程序必须通过调用 **FltReleaseContext** 来释放它。

设置上下文类型后，微筛选器可以在后续 i/o 操作期间 [获取上下文](getting-contexts.md))  (s，以确定是否需要执行任何操作。

最终必须 [删除](deleting-contexts.md)每个成功的上下文集。

在以下代码示例中，从 [CTX 示例微筛选](https://github.com/microsoft/Windows-driver-samples/tree/master/filesys/miniFilter/ctx)器中获取， **CtxInstanceSetup** 例程创建并设置实例上下文：

```cpp
status = FltAllocateContext(
           FltObjects->Filter,              //in: Filter
           FLT_INSTANCE_CONTEXT,            //in: ContextType
           CTX_INSTANCE_CONTEXT_SIZE,       //in: ContextSize
           NonPagedPool,                    //in: PoolType
           &instanceContext);               //out: ReturnedContext
...
status = FltSetInstanceContext(
           FltObjects->Instance,            //in: Instance
           FLT_SET_CONTEXT_KEEP_IF_EXISTS,  //in: Operation
           instanceContext,                 //in: NewContext
           NULL);                           //out: OldContext

if (instanceContext != NULL) {
  FltReleaseContext(instanceContext);
}
return status;
```

请注意，调用 [**FltSetInstanceContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetinstancecontext)后，调用 **FltReleaseContext** ，以释放 ([**FltAllocateContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext) 设置的引用计数，而 *不* 是 **FltSetInstanceContext**) 。 这在 [发布上下文](releasing-contexts.md)中进行了介绍。
