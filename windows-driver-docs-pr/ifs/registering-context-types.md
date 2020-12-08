---
title: 注册上下文类型
description: 注册上下文类型
keywords:
- 上下文 WDK 文件系统微筛选器，注册类型
- 注册上下文类型
- FLT_CONTEXT_REGISTRATION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2dd083e591f447fd1cf7e94075f3244cba22142d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829661"
---
# <a name="registering-context-types"></a>注册上下文类型


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


当微筛选器驱动程序从其 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程调用 [**FltRegisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)时，它必须注册其使用的每种类型的上下文。

若要注册上下文类型，微筛选器驱动程序将创建 [**FLT \_ 上下文 \_ 注册**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_context_registration)结构的可变长度数组，并将指向该数组的指针存储在 [**FLT \_ 注册**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)结构的 **ContextRegistration** 成员中，微筛选器驱动程序在 [**FltRegisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)的 *注册* 参数中传递。 此数组中的元素顺序并不重要。 但是，数组中的最后一个元素必须是 {FLT \_ CONTEXT \_ END}。

对于微筛选器驱动程序使用的每个上下文类型，必须至少提供一个 FLT \_ 上下文注册结构形式的上下文定义 \_ 。 每个 FLT \_ 上下文 \_ 注册结构都定义了上下文的类型、大小和其他信息。

当微筛选器驱动程序通过调用 [**FltAllocateContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)创建新上下文时，筛选器管理器将使用 **FltAllocateContext** 例程的 *size* 参数，以及 FLT 上下文注册结构的 **大小** 和 **标志** 成员 \_ \_ ，以选择要使用的上下文定义。

对于固定大小的上下文，FLT **Size** \_ 上下文注册结构的 size 成员 \_ 指定由微筛选器驱动程序定义的上下文结构部分的大小（以字节为单位）。 上下文的最大大小为 MAXUSHORT (64 KB) 。 零是有效的大小值。 筛选器管理器使用后备链表列表实现固定大小的上下文。 筛选器管理器为每个大小值创建两个后备链表列表：一个分页和一个非分页。

对于可变大小的上下文，必须将 **大小** 成员设置为 FLT 变量大小的 \_ \_ \_ 上下文。 筛选器管理器直接从分页或非分页池分配可变大小上下文。

在 FLT 上下文注册结构的 **Flags** 成员中 \_ ，无法 \_ \_ \_ \_ \_ \_ 指定完全大小的 \_ 匹配标志。 如果微筛选器驱动程序使用固定大小的上下文并且指定了此标志，则筛选器管理器将从后备链表列表分配上下文（如果上下文的大小大于或等于请求的大小）。 否则，上下文的大小必须等于请求的大小。

对于给定的上下文类型，微筛选器驱动程序最多可以提供三个固定大小的上下文定义，每个定义有不同的大小和一个可变大小的定义。 有关详细信息，请参阅 [**FLT \_ CONTEXT \_ REGISTRATION**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_context_registration)。

微筛选器驱动程序可以选择提供要在释放上下文之前调用的上下文清理回调例程。 有关详细信息，请参阅 [**PFLT \_ 上下文 \_ 清理 \_ 回调**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_cleanup_callback)。

微筛选器驱动程序可以有选择地定义自己的用于分配和释放上下文的回调例程，而不是依靠筛选器管理器来执行这些任务。 但这种情况很少需要。 有关详细信息，请参阅 [**PFLT \_ 上下文 \_ 分配 \_ 回调**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_allocate_callback) 和 [**PFLT \_ context \_ FREE \_ 回呼**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_free_callback)。

下面的代码示例摘自 CTX 示例微筛选器驱动程序，显示了一个 FLT \_ 上下文 \_ 注册结构数组，这些结构用于注册实例、文件、流和文件对象 (流句柄) 上下文。

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

 

