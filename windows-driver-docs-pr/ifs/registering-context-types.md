---
title: 注册上下文类型
description: 注册上下文类型
keywords:
- 上下文 WDK 文件系统微筛选器，注册类型
- 注册上下文类型
- FLT_CONTEXT_REGISTRATION
ms.date: 01/22/2021
ms.localizationpriority: medium
ms.openlocfilehash: 5e2bbd560c14cdda6c91372f2cb211952d338305
ms.sourcegitcommit: 204ed37ede1cd462ef6f6c9211a223fd304da4a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2021
ms.locfileid: "99502046"
---
# <a name="registering-context-types"></a>注册上下文类型

微筛选器驱动程序必须注册其使用的每种类型的上下文。

## <a name="steps-to-register-a-context-type"></a>注册上下文类型的步骤

微筛选器调用 [**FltRegisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter) 的 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程来注册其使用的每种类型的上下文。 在调用 **FltRegisterFilter** 之前，微筛选器驱动程序会执行以下操作：

- 创建 [**FLT_CONTEXT_REGISTRATION**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_context_registration) 结构的可变长度数组。 此数组中的元素顺序并不重要;但是，数组中的最后一个元素必须是 {FLT_CONTEXT_END}。
- 在 [**FLT_REGISTRATION**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)结构的 **ContextRegistration** 成员中存储指向所创建的数组的指针。 微筛选器将此结构传递到 [**FltRegisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)的 *注册* 参数。

对于微筛选器驱动程序使用的每个上下文类型，必须至少提供一个上下文定义。 定义采用 [**FLT_CONTEXT_REGISTRATION**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_context_registration) 结构的形式，其中每个结构定义上下文的类型、大小和其他信息。

当微筛选器驱动程序调用 [**FltAllocateContext**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext) 来创建新上下文时，筛选器管理器将使用 **size** 参数，以及 FLT_CONTEXT_REGISTRATION 结构的 **大小** 和 **标志** 成员，以选择要使用的上下文定义：

- 对于固定大小的上下文，FLT_CONTEXT_REGISTRATION 结构的 **size** 成员指定由微筛选器驱动程序定义的上下文结构部分的大小（以字节为单位）。 上下文的最大大小为 MAXUSHORT (64 KB) 。 零是有效的大小值。 筛选器管理器使用后备链表列表实现固定大小的上下文。 筛选器管理器为每个大小值创建两个后备链表列表：一个分页和一个非分页。

- 对于可变大小的上下文，必须将 **大小** 成员设置为 FLT_VARIABLE_SIZED_CONTEXTS。 筛选器管理器直接从分页或非分页池分配可变大小上下文。

在 FLT_CONTEXT_REGISTRATION 结构的 **Flags** 成员中，可以指定 FLTFL_CONTEXT_REGISTRATION_NO_EXACT_SIZE_MATCH 标志。 如果微筛选器驱动程序使用固定大小的上下文并且指定了此标志，则筛选器管理器将从后备链表列表分配上下文（如果上下文的大小大于或等于请求的大小）。 否则，上下文的大小必须等于请求的大小。

对于给定的上下文类型，微筛选器驱动程序最多可以提供三个固定大小的上下文定义，每个定义有不同的大小和一个可变大小的定义。 有关详细信息，请参阅 [**FLT_CONTEXT_REGISTRATION**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_context_registration)。

## <a name="minifilter-callback-routines-for-context-management"></a>上下文管理的微筛选器回调例程

微筛选器驱动程序可以选择提供以下上下文相关的回调例程，它们存储在作为参数传递给 [**FltRegisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)的 [**FLT_REGISTRATION**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)结构中：

| 回调例程 | 说明 |
| ---------------- | ----------- |
| [**PFLT_CONTEXT_ALLOCATE_CALLBACK**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_allocate_callback) | 在极少数情况下，微筛选器可能需要定义自己的回调例程来分配上下文，而不是依赖于筛选器管理器。 |
|  [**PFLT_CONTEXT_CLEANUP_CALLBACK**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_cleanup_callback) | 要在释放上下文之前调用的微筛选器清理例程。 |
| [**PFLT_CONTEXT_FREE_CALLBACK**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_free_callback) | 在极少数情况下，微筛选器可能需要定义自己的回调例程来释放上下文，而不是依赖于筛选器管理器。 |

## <a name="context-registration-code-example"></a>上下文注册代码示例

下面的代码示例摘自 [CTX 示例微筛选器驱动程序](https://github.com/microsoft/Windows-driver-samples/tree/master/filesys/miniFilter/ctx)，其中显示了一个 **FLT_CONTEXT_REGISTRATION** 结构的数组，这些结构用于将实例、文件、流和文件对象 (流句柄注册) 上下文。

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
