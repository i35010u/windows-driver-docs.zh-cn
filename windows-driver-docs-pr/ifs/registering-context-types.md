---
title: 注册上下文类型
description: 注册上下文类型
ms.assetid: ddf03426-5c49-4621-b81d-59d1cb002ae9
keywords:
- 上下文 WDK 文件系统微筛选器，注册类型
- 注册上下文类型
- FLT_CONTEXT_REGISTRATION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 242c3363cdcb79f479bd13360ad623be53b57740
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522362"
---
# <a name="registering-context-types"></a>注册上下文类型


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


当微筛选器驱动程序调用[ **FltRegisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544305)从其[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程，必须注册每种类型的上下文，它使用。

若要注册上下文类型，微筛选器驱动程序创建的变量长度数组[ **FLT\_上下文\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff544629)结构和存储到数组中的指针**ContextRegistration**的成员[ **FLT\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff544811)微筛选器驱动程序中传递的结构*注册*的参数[ **FltRegisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544305)。 此数组中元素的顺序不重要。 但是，数组中的最后一个元素必须是 {FLT\_上下文\_最终}。

对于微筛选器驱动程序将使用每个上下文类型，它必须提供至少一个上下文定义形式的 FLT\_上下文\_注册结构。 每个 FLT\_上下文\_注册结构定义类型、 大小和其他上下文信息。

当微筛选器驱动程序通过调用创建新的上下文[ **FltAllocateContext**](https://msdn.microsoft.com/library/windows/hardware/ff541710)，筛选器管理器使用*大小*参数**FltAllocateContext**例程，并将**大小**并**标志**FLT 成员\_上下文\_注册结构选择要使用的上下文定义。

对于固定大小上下文**大小**FLT 成员\_上下文\_注册结构指定的大小，以字节为单位定义微筛选器驱动程序的上下文结构的一部分。 上下文的最大大小是 MAXUSHORT (64 KB)。 有效大小值为零。 筛选器管理器实现使用后备链列表的大小固定的上下文。 筛选器管理器创建的每个大小值的两个后备链列表： 一个分页，另一个非分页。

大小可变的上下文**大小**成员必须设置为 FLT\_变量\_调整\_上下文。 筛选器管理器直接从分页或非分页缓冲池分配大小可变的上下文。

在中**标志**FLT 成员\_上下文\_注册结构，FLTFL\_上下文\_注册\_否\_EXACT\_大小\_可以指定匹配项标志。 如果微筛选器驱动程序将使用固定大小的上下文，并且指定此标志，筛选器管理器分配从后备链列表上下文，上下文的大小是否大于或等于请求的大小。 否则，上下文的大小必须等于请求的大小。

对于给定的上下文类型，微筛选器驱动程序可以提供最多三个固定大小上下文定义，其中每个不同的大小和一个可变大小定义。 有关详细信息，请参阅[ **FLT\_上下文\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff544629)。

微筛选器驱动程序可以根据需要提供上下文清理回调例程之前释放上下文调用。 有关详细信息，请参阅[ **PFLT\_上下文\_清理\_回调**](https://msdn.microsoft.com/library/windows/hardware/ff551078)。

微筛选器驱动程序可以选择定义其自己的分配和释放上下文，而不是依赖于要执行这些任务的筛选器管理器的回调例程。 但是，这是很少需要。 有关详细信息，请参阅[ **PFLT\_上下文\_分配\_回调**](https://msdn.microsoft.com/library/windows/hardware/ff551075)并[ **PFLT\_上下文\_免费\_回调**](https://msdn.microsoft.com/library/windows/hardware/ff551082)。

下面的代码示例摘自 CTX 示例微筛选器驱动程序，显示了一个数组 FLT\_上下文\_注册结构用来注册实例、 文件、 流和文件 （流句柄） 对象上下文。

```cpp
const FLT_CONTEXT_REGISTRATION contextRegistration[] =
{
    { FLT_INSTANCE_CONTEXT,              //ContextType
      0,                                 //Flags
      CtxContextCleanup,                 //ContextCleanupCallback
      CTX_INSTANCE_CONTEXT_SIZE,         //Size
      CTX_INSTANCE_CONTEXT_TAG           //PoolTag
    },
    { FLT_FILE_CONTEXT,                  //ContextType
      0,                                 //Flags
      CtxContextCleanup,                 //ContextCleanupCallback
      CTX_FILE_CONTEXT_SIZE,             //Size
      CTX_FILE_CONTEXT_TAG               //PoolTag
    },
    { FLT_STREAM_CONTEXT,                //ContextType
      0,                                 //Flags
      CtxContextCleanup,                 //ContextCleanupCallback
      CTX_STREAM_CONTEXT_SIZE,           //Size
      CTX_STREAM_CONTEXT_TAG             //PoolTag
    },
    { FLT_STREAMHANDLE_CONTEXT,          //ContextType
      0,                                 //Flags
      CtxContextCleanup,                 //ContextCleanupCallback
      CTX_STREAMHANDLE_CONTEXT_SIZE,     //Size
      CTX_STREAMHANDLE_CONTEXT_TAG       //PoolTag
    },
    { FLT_CONTEXT_END }
};
```

 

 




