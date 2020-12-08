---
title: 访问后操作回调例程中的用户缓冲区
description: 访问后操作回调例程中的用户缓冲区
keywords:
- postoperation 回调例程 WDK 文件系统微筛选器，缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 040d6046594e91c04390984bffed7466b9c03ca3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816295"
---
# <a name="accessing-user-buffers-in-a-postoperation-callback-routine"></a>访问后操作回调例程中的用户缓冲区


## <span id="ddk_accessing_user_buffers_in_a_postoperation_callback_routine_if"></span><span id="DDK_ACCESSING_USER_BUFFERS_IN_A_POSTOPERATION_CALLBACK_ROUTINE_IF"></span>


微筛选器驱动程序 [**postoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback) 应在基于 IRP 的 i/o 操作中处理缓冲区，如下所示：

-   检查缓冲区是否存在 MDL。 可以在操作的 [**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)的 *MdlAddress* 或 *OutputMdlAddress* 参数中找到 MDL 指针。 微筛选器驱动程序可以调用 [**FltDecodeParameters**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdecodeparameters) 来查询 MDL 指针。

    获取有效 MDL 的一种方法是在 \_ \_ 回调数据的 i/o 参数块 [**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)的 **MinorFunction** 成员中查找 IRP MN MDL 标志。 下面的示例演示如何检查 IRP \_ MN \_ MDL 标志。

    ```ManagedCPlusPlus
    NTSTATUS status;
    PMDL *ReadMdl = NULL;
    PVOID ReadAddress = NULL;

    if (FlagOn(CallbackData->Iopb->MinorFunction, IRP_MN_MDL))
    {
        ReadMdl = &CallbackData->Iopb->Parameters.Read.MdlAddress;
    }
    ```

    但是，只能 \_ \_ 为读写操作设置 IRP MN MDL 标志。 最好使用 [**FltDecodeParameters**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdecodeparameters) 检索 MDL，因为例程检查任何操作是否有有效的 mdl。 在以下示例中，如果有效，则仅返回 MDL 参数。

    ```ManagedCPlusPlus
    NTSTATUS status;
    PMDL *ReadMdl = NULL;
    PVOID ReadAddress = NULL;

    status = FltDecodeParameters(CallbackData, &ReadMdl, NULL, NULL, NULL);
    ```

-   如果缓冲区存在 MDL，请调用 [**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md) 获取缓冲区的系统地址，然后使用此地址访问缓冲区。 可以 **MmGetSystemAddressForMdlSafe** 在 IRQL &lt; = 调度级别调用 (MmGetSystemAddressForMdlSafe \_ 。 ) 

    继续前面的示例，下面的代码获取系统地址。

    ```ManagedCPlusPlus
    if (*ReadMdl != NULL)
    {
        ReadAddress = MmGetSystemAddressForMdlSafe(*ReadMdl, NormalPagePriority);
        if (ReadAddress == NULL)
        {
            CallbackData->IoStatus.Status = STATUS_INSUFFICIENT_RESOURCES;
            CallbackData->IoStatus.Information = 0;
        }
    }
    ```

-   如果缓冲区没有 MDL，请使用 [**FLT \_ 为 \_ 系统 \_ 缓冲区**](/previous-versions/ff544663(v=vs.85)) 宏检查是否为操作设置了系统缓冲区标志。

    -   如果 FLT \_ 是 \_ 系统 \_ 缓冲区宏，则返回 **TRUE**，则操作将使用缓冲 i/o，并且可以安全地访问缓冲区（IRQL = 调度 \_ 级别）。

    -   如果 FLT \_ 是 \_ 系统 \_ 缓冲区宏，则返回 **FALSE**，不能安全地访问该缓冲区，因为 IRQL = 调度 \_ 级别。 如果可以在调度级别调用 postoperation 回调例程 \_ ，则它必须调用 [**FltDoCompletionProcessingWhenSafe**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe) 来挂起操作，直到可以在 IRQL &lt; = APC 级别处理该操作 \_ 。 **FltDoCompletionProcessingWhenSafe** 的 *SafePostCallback* 参数指向的回调例程应该首先调用 [**FltLockUserBuffer**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)锁定缓冲区，然后调用 [**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md)以获取缓冲区的系统地址。

Postoperation 回调例程应按如下所示在快速 i/o 操作中处理缓冲区：

-   使用缓冲区地址访问缓冲区 (因为快速 i/o 操作不能具有 MDL) 。

-   若要确保用户空间缓冲区的地址有效，微筛选器驱动程序必须使用 [**ProbeForRead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)或 [**ProbeForWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)等例程，并在 **try** / **except** 块中包含所有缓冲区引用。

-   可保证快速 i/o 操作的 postoperation 回调例程在正确的线程上下文中调用。

-   可保证快速 i/o 操作的 postoperation 回调例程在 IRQL &lt; = APC \_ 级别调用，因此它可以安全调用例程，如 [**FltLockUserBuffer**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)。

下面的示例代码片段检查是否存在用于目录控制操作的系统缓冲区或快速 i/o 标志，并在必要时使完成处理延迟。

```CSS
if (*DirectoryControlMdl == NULL)
{
    if (FLT_IS_SYSTEM_BUFFER(CallbackData) || FLT_IS_FASTIO_OPERATION(CallbackData))
    {
        dirBuffer = CallbackData->Iopb->Parameters.DirectoryControl.QueryDirectory.DirectoryBuffer;
    }
    else
    {
        // Defer processing until safe.
        if (!FltDoCompletionProcessingWhenSafe(CallbackData, FltObjects, CompletionContext, Flags, ProcessPostDirCtrlWhenSafe, &retValue))
        {
            CallbackData->IoStatus.Status = STATUS_UNSUCCESSFUL;
            CallbackData->IoStatus.Information = 0;
        }
    }
}
```

对于可以是快速 i/o 或基于 IRP 的操作，所有缓冲区引用应包含在 **try** / **except** 块中。 尽管不需要将这些引用包含在使用缓冲 i/o 的基于 IRP 的操作中，但 **try** / **except** 块是一项安全预防措施。

 

