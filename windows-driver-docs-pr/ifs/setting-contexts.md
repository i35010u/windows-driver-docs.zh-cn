---
title: 设置上下文
description: 设置上下文
ms.assetid: 3daa23e6-14d7-4d35-8bc8-695296cd289d
keywords:
- 上下文 WDK 文件系统微筛选器，设置
- 附加上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f14427def7d85c90985442f48f3ff8b81218c5ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577171"
---
# <a name="setting-contexts"></a>设置上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


创建新的上下文之后, 微筛选器驱动程序可以将其附加到对象通过调用**FltSet***Xxx***上下文**，其中*Xxx*是上下文类型。

如果*操作*的参数**FltSet***Xxx***上下文**例程设置为 FLT\_设置\_上下文\_保持\_IF\_EXISTS， **FltSet***Xxx***上下文**将新分配的上下文附加到对象，仅当微筛选器驱动程序还未设置对象的上下文。 如果微筛选器驱动程序已将设置上下文**FltSet***Xxx***上下文**返回状态\_FLT\_上下文\_已\_定义，这是NTSTATUS 错误代码，并不会替换现有上下文。 如果*OldContext*的参数**FltSet***Xxx***上下文**例程为非**NULL**，它接收指向现有上下文。 当不再需要此指针时，微筛选器驱动程序必须将其释放通过调用[ **FltReleaseContext**](https://msdn.microsoft.com/library/windows/hardware/ff544314)。

如果*操作*参数设置为 FLT\_设置\_上下文\_替换\_如果\_EXISTS， **FltSet***Xxx***上下文**始终将新的上下文附加到对象。 如果微筛选器驱动程序已将设置上下文**FltSet***Xxx***上下文**删除现有上下文，设置新的上下文中，并增加新的上下文的引用计数。 如果*OldContext*参数为非**NULL**，它接收指向已删除的上下文。 当不再需要此指针时，微筛选器驱动程序必须将其释放通过调用**FltReleaseContext**。

在以下代码示例中，从 CTX 示例微筛选器驱动程序， **CtxInstanceSetup**例程创建并设置实例上下文：

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

请注意，在调用后[ **FltSetInstanceContext**](https://msdn.microsoft.com/library/windows/hardware/ff544521)，没有调用**FltReleaseContext**释放所设置的引用计数[ **FltAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff541710) (*不* **FltSetInstanceContext**)。 对此进行[释放上下文](releasing-contexts.md)。

 

 




