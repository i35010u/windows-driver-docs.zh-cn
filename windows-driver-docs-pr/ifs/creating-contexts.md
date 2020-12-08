---
title: 创建上下文
description: 创建上下文
keywords:
- 上下文 WDK 文件系统微筛选器，创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f3de6930672dbda99c1c3fea9ca1002038a826f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837277"
---
# <a name="creating-contexts"></a>创建上下文


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


微筛选器驱动程序注册它所使用的上下文类型后，可以通过调用 [**FltAllocateContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)创建上下文。 此例程根据 [注册上下文类型](registering-context-types.md)中所述的条件来选择要使用的适当上下文定义。

在以下代码示例中，从 CTX 示例微筛选器驱动程序开始， **CtxInstanceSetup** 例程调用 [**FltAllocateContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext) 来创建实例上下文：

```cpp
status = FltAllocateContext(
 FltObjects->Filter,           //Filter
           FLT_INSTANCE_CONTEXT,         //ContextType
           CTX_INSTANCE_CONTEXT_SIZE,    //ContextSize
 NonPagedPool,                 //PoolType
           &instanceContext);            //ReturnedContext
```

在 CTX 示例中，为实例上下文注册了以下上下文定义：

```cpp
{ FLT_INSTANCE_CONTEXT,              //ContextType
  0,                                 //Flags
 CtxContextCleanup,                 //ContextCleanupCallback
  CTX_INSTANCE_CONTEXT_SIZE,         //Size
  CTX_INSTANCE_CONTEXT_TAG },        //PoolTag
```

这是一个固定大小的上下文定义，因为 **大小** 成员是常数。  (如果 **Size** 成员是 FLT 变量大小的 \_ \_ \_ 上下文，则它将是可变大小的上下文定义。 ) 请注意， \_ \_ \_ \_ \_ \_ **标志** 成员中未设置完全大小匹配标志。 在这种情况下，如果 [**FltAllocateContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)的 *size* 参数值与上下文定义的 **size** 成员的值相匹配，则 **FltAllocateContext** 将从相应的非分页后备链表列表中分配实例上下文。 如果值不匹配，则 **FltAllocateContext** 将失败，返回值为 " \_ FLT \_ \_ 未找到上下文分配" \_ \_ 。

[**FltAllocateContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext) 将新上下文的引用计数初始化为一个。 如果不再需要该上下文，则微筛选器驱动程序必须释放此引用。 因此，每次调用 **FltAllocateContext** 时，必须通过对 [**FltReleaseContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)的后续调用来匹配。

 

