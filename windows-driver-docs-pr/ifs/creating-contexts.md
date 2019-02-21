---
title: 创建上下文
description: 创建上下文
ms.assetid: da62d79d-064b-4ea4-abed-ffb13a9cc13d
keywords:
- 上下文 WDK 文件系统微筛选器，创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae2d6d8bff653c96d1c5d44a41312b8c8224ab1e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554173"
---
# <a name="creating-contexts"></a>创建上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


一旦微筛选器驱动程序已注册它使用的上下文类型，它可以通过调用创建上下文[ **FltAllocateContext**](https://msdn.microsoft.com/library/windows/hardware/ff541710)。 此例程选择适当的上下文定义用于根据条件中所述[上下文类型注册](registering-context-types.md)。

在以下代码示例中，从 CTX 示例微筛选器驱动程序， **CtxInstanceSetup**例程调用[ **FltAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff541710)若要创建的实例上下文:

```cpp
status = FltAllocateContext(
 FltObjects->Filter,           //Filter
           FLT_INSTANCE_CONTEXT,         //ContextType
           CTX_INSTANCE_CONTEXT_SIZE,    //ContextSize
 NonPagedPool,                 //PoolType
           &instanceContext);            //ReturnedContext
```

在 CTX 示例中，以下上下文定义为实例上下文注册：

```cpp
{ FLT_INSTANCE_CONTEXT,              //ContextType
  0,                                 //Flags
 CtxContextCleanup,                 //ContextCleanupCallback
  CTX_INSTANCE_CONTEXT_SIZE,         //Size
  CTX_INSTANCE_CONTEXT_TAG },        //PoolTag
```

这是一个固定大小上下文定义，因为**大小**成员是一个常量。 (如果**大小**成员已 FLT\_变量\_调整\_上下文，它将是一个可变大小上下文定义。)请注意，FLTFL\_上下文\_注册\_否\_EXACT\_大小\_匹配项标志未设置**标志**成员。 在这种情况下，如果的值*大小*的参数[ **FltAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff541710)的对应项匹配**大小**上下文的成员定义中， **FltAllocateContext**从相应的非分页后备链列表分配实例上下文。 如果值不匹配， **FltAllocateContext**失败，并返回值的状态\_FLT\_上下文\_分配\_不\_找到。

[**FltAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff541710)初始化到一个新的上下文的引用计数。 当不再需要上下文时，微筛选器驱动程序必须释放此引用。 因此，每次调用**FltAllocateContext**的后续调用必须匹配[ **FltReleaseContext**](https://msdn.microsoft.com/library/windows/hardware/ff544314)。

 

 




