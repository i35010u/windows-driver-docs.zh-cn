---
title: 释放上下文
description: 释放上下文
ms.assetid: 29d855cd-cca6-486b-86d9-f74810ae12c1
keywords:
- 上下文 WDK 文件系统微筛选器，释放
- 释放上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd7f28a6421bfbd784f0b276cbee9a1578be7408
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548094"
---
# <a name="releasing-contexts"></a>释放上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


微筛选器驱动程序通过调用释放上下文[ **FltReleaseContext**](https://msdn.microsoft.com/library/windows/hardware/ff544314)。 下面的例程之一的每个成功调用最终必须匹配通过调用**FltReleaseContext**:

[**FltAllocateContext**](https://msdn.microsoft.com/library/windows/hardware/ff541710)

[**FltGetInstanceContext**](https://msdn.microsoft.com/library/windows/hardware/ff543058)

[**FltGetFileContext**](https://msdn.microsoft.com/library/windows/hardware/ff543025)

[**FltGetStreamContext**](https://msdn.microsoft.com/library/windows/hardware/ff543144)

[**FltGetStreamHandleContext**](https://msdn.microsoft.com/library/windows/hardware/ff543155)

[**FltGetTransactionContext**](https://msdn.microsoft.com/library/windows/hardware/ff543175)

[**FltGetVolumeContext**](https://msdn.microsoft.com/library/windows/hardware/ff543189)

[**FltReferenceContext**](https://msdn.microsoft.com/library/windows/hardware/ff544291)

请注意， *OldContext*返回指针**FltSet***Xxx***上下文**并*上下文*返回指针[**FltDeleteContext** ](https://msdn.microsoft.com/library/windows/hardware/ff541960)在不再需要时还必须发布。

在以下代码示例中，从 CTX 示例微筛选器驱动程序， **CtxInstanceSetup**例程创建和设置的实例上下文，然后调用[ **FltReleaseContext** ](https://msdn.microsoft.com/library/windows/hardware/ff544314):

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

请注意， [ **FltReleaseContext** ](https://msdn.microsoft.com/library/windows/hardware/ff544314)调用而不管是否对[ **FltSetInstanceContext** ](https://msdn.microsoft.com/library/windows/hardware/ff544521)成功。 在这两种情况下，调用方必须调用**FltReleaseContext**来释放由设置该引用[ **FltAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff541710) (不**FltSetInstanceContext**).

如果实例已成功设置的上下文[ **FltSetInstanceContext** ](https://msdn.microsoft.com/library/windows/hardware/ff544521)添加其自己的实例上下文的引用。 因此，设置引用[ **FltAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff541710)不再需要以及对调用[ **FltReleaseContext** ](https://msdn.microsoft.com/library/windows/hardware/ff544314)将其删除。

如果在调用[ **FltSetInstanceContext** ](https://msdn.microsoft.com/library/windows/hardware/ff544521)失败，实例上下文具有只有一个引用，即的项目设置[ **FltAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff541710). 当[ **FltReleaseContext** ](https://msdn.microsoft.com/library/windows/hardware/ff544314)返回时，实例上下文具有引用计数为零，并且筛选器管理器释放它。

 

 




