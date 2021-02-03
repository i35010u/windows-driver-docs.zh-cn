---
title: 创建上下文
description: 创建上下文
keywords:
- 上下文 WDK 文件系统微筛选器，创建
ms.date: 01/22/2021
ms.localizationpriority: medium
ms.openlocfilehash: 486e70c8a5069fee2ac5857c5332dfec08ceade9
ms.sourcegitcommit: 204ed37ede1cd462ef6f6c9211a223fd304da4a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2021
ms.locfileid: "99502040"
---
# <a name="creating-contexts"></a>创建上下文

一旦微筛选器注册了它使用的上下文类型，它就可以通过调用 [**FltAllocateContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)来创建上下文。 此例程根据 [注册上下文类型](registering-context-types.md)中所述的条件来选择要使用的适当上下文定义。

在分配上下文和尝试设置上下文之前，微筛选器可以调用以下例程来确定基础文件系统是否支持文件、流或流句柄上下文：
- [**FltSupportsFileContexts**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsupportsfilecontexts)或 [ **FltSupportsFileContextsEx**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsupportsfilecontextsex)
- [**FltSupportsStreamContexts**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsupportsstreamcontexts)
- [**FltSupportsStreamHandleContexts**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsupportsstreamhandlecontexts)

在以下代码示例中，从 [CTX 示例微筛选](https://github.com/microsoft/Windows-driver-samples/tree/master/filesys/miniFilter/ctx) 器驱动程序开始， **CtxInstanceSetup** 例程调用 [**FltAllocateContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext) 来创建实例上下文：

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

上下文定义的大小是固定的，因为 **size** 成员是 CTX_INSTANCE_CONTEXT_SIZE (与 FLT_VARIABLE_SIZED_CONTEXTS，后者用于指示大小可变的上下文) 定义。 请注意， **标志** 成员中未设置 FLTFL_CONTEXT_REGISTRATION_NO_EXACT_SIZE_MATCH 标志。 在这种情况下，如果 [**FltAllocateContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)的 **ContextSize** 参数的值与上下文定义的 **Size** 成员的值匹配，则 **FltAllocateContext** 将从相应的非分页后备链表列表中分配实例上下文。 如果值不匹配， **FltAllocateContext** 将失败，返回值为 STATUS_FLT_CONTEXT_ALLOCATION_NOT_FOUND。

成功后， [**FltAllocateContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext) 会将新上下文中的引用计数初始化为一个。 如果不再需要该上下文，则微筛选器驱动程序必须释放此引用。 因此，每次调用 **FltAllocateContext** 时，必须通过对 [**FltReleaseContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)的后续调用来匹配。

创建上下文后，可以通过微筛选器 [将其设置为对象](setting-contexts.md)。
