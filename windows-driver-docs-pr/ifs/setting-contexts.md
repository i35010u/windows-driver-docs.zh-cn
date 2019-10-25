---
title: 设置上下文
description: 设置上下文
ms.assetid: 3daa23e6-14d7-4d35-8bc8-695296cd289d
keywords:
- 上下文 WDK 文件系统微筛选器，设置
- 附加上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eca82bc563401c820a3851c2df20ffce86c86f7f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840965"
---
# <a name="setting-contexts"></a>设置上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


创建新上下文后，微筛选器驱动程序可以通过调用**FltSet***xxx***上下文**将其附加到对象，其中*Xxx*是上下文类型。

如果**FltSet***Xxx***上下文**例程的*Operation*参数设置为 FLT\_设置\_上下文\_保留\_如果\_存在，则**FltSet***Xxx***上下文**会将新分配的上下文附加到仅当微筛选器驱动程序尚未设置对象的上下文时才使用对象。 如果微筛选器驱动程序已设置上下文，则**FltSet***Xxx***上下文**返回状态\_\_FLT 已\_定义\_，这是一个 NTSTATUS 错误代码，并且不会替换现有的上下文。 如果**FltSet***Xxx***上下文**例程的*OldContext*参数为非**NULL**，则它将接收指向现有上下文的指针。 如果不再需要此指针，微筛选器驱动程序必须通过调用[**FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)来释放它。

如果*Operation*参数设置为 FLT\_设置\_CONTEXT\_替换\_如果\_存在，则**FltSet***Xxx***上下文**始终将新上下文附加到对象。 如果微筛选器驱动程序已设置上下文， **FltSet***Xxx***上下文**会删除现有上下文，设置新上下文并递增引用计数。 如果*OldContext*参数为非**NULL**，则它将接收指向已删除上下文的指针。 如果不再需要此指针，微筛选器驱动程序必须通过调用**FltReleaseContext**来释放它。

在以下代码示例中，从 CTX 示例微筛选器驱动程序开始， **CtxInstanceSetup**例程创建并设置实例上下文：

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

请注意，调用[**FltSetInstanceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetinstancecontext)后，将调用**FltReleaseContext**以释放[**FltAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext) （*而非* **FltSetInstanceContext**）设置的引用计数。 这在[发布上下文](releasing-contexts.md)中进行了介绍。

 

 




