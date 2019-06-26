---
title: 访问后操作回调例程中的用户缓冲区
description: 访问后操作回调例程中的用户缓冲区
ms.assetid: a980f302-6fde-461e-8b11-313530aff350
keywords:
- postoperation 回调例程 WDK 文件系统微筛选器，缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73faf5545cbd8db2a4240324e972a0d00eff3213
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381737"
---
# <a name="accessing-user-buffers-in-a-postoperation-callback-routine"></a>访问后操作回调例程中的用户缓冲区


## <span id="ddk_accessing_user_buffers_in_a_postoperation_callback_routine_if"></span><span id="DDK_ACCESSING_USER_BUFFERS_IN_A_POSTOPERATION_CALLBACK_ROUTINE_IF"></span>


微筛选器驱动程序[ **postoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)应将缓冲区的基于 IRP 的 I/O 操作，如下所示：

-   检查缓冲区是否存在 MDL。 可在 MDL 指针*MdlAddress*或*OutputMdlAddress*中的参数[ **FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)为该操作。 微筛选器驱动程序可以调用[ **FltDecodeParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdecodeparameters) MDL 指针的查询。

    一种方法可以获取有效 MDL 所查找 IRP\_MN\_MDL 标志**MinorFunction** I/O 参数块，成员[ **FLT\_IO\_参数\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)中的回调数据。 下面的示例演示如何检查 IRP\_MN\_MDL 标志。

    ```ManagedCPlusPlus
    NTSTATUS status;
    PMDL *ReadMdl = NULL;
    PVOID ReadAddress = NULL;

    if (FlagOn(CallbackData->Iopb->MinorFunction, IRP_MN_MDL))
    {
        ReadMdl = &CallbackData->Iopb->Parameters.Read.MdlAddress;
    }
    ```

    但是，IRP\_MN\_MDL 标志可设置仅为读取和写入操作。 最好是使用[ **FltDecodeParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdecodeparameters)检索 MDL，因为该例程检查有效 MDL 的任何操作。 在以下示例中，如果有效，则返回仅 MDL 参数。

    ```ManagedCPlusPlus
    NTSTATUS status;
    PMDL *ReadMdl = NULL;
    PVOID ReadAddress = NULL;

    status = FltDecodeParameters(CallbackData, &ReadMdl, NULL, NULL, NULL);
    ```

-   如果 MDL 缓冲区存在，则调用[ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)获取缓冲区的系统地址，然后使用此地址来访问缓冲区。 (**MmGetSystemAddressForMdlSafe**可以在 IRQL 调用&lt;= 调度\_级别。)

    继续执行上一示例中，使用以下代码获取系统地址。

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

-   如果没有 MDL 缓冲区，检查是否系统缓冲区标志设置为该操作通过使用[ **FLT\_IS\_系统\_缓冲区**](https://docs.microsoft.com/previous-versions/ff544663(v=vs.85))宏。

    -   如果 FLT\_IS\_系统\_缓冲区宏将返回**TRUE**，该操作使用缓冲的 I/O 和缓冲区可以安全地访问在 IRQL = 调度\_级别。

    -   如果 FLT\_IS\_系统\_缓冲区宏将返回**FALSE**，缓冲区无法安全地访问在 IRQL = 调度\_级别。 如果可以在调度调用 postoperation 回调例程\_级别，它必须调用[ **FltDoCompletionProcessingWhenSafe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe)挂起操作之前可以处理在 IRQL &lt;= APC\_级别。 指向回调例程*SafePostCallback*的参数**FltDoCompletionProcessingWhenSafe**应先调用[ **FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltlockuserbuffer)锁定缓冲区，然后调用[ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)获取缓冲区的系统地址。

Postoperation 回调例程应将缓冲区的快速 I/O 操作，如下所示：

-   使用的缓冲区地址来访问缓冲区 （因为快速 I/O 操作不能具有 MDL）。

-   若要确保用户空间缓冲区地址是否有效，微筛选器驱动程序必须使用一个例程如[ **ProbeForRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)或[ **ProbeForWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)，封闭中的所有缓冲区引用**尝试**/**除**块。

-   快速的 I/O 操作的 postoperation 回调例程保证在正确的线程上下文中调用。

-   快速 I/O 操作的 postoperation 回调例程保证调用在 IRQL &lt;= APC\_级别，因此如可以安全地调用例程[ **FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltlockuserbuffer)。

下面的示例代码段检查系统缓冲区或快速 I/O 目录控制操作标记，并将延迟完成处理，如有必要。

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

可以是任一快速 I/O 的操作或基于 IRP 的所有缓冲区引用应都括在**尝试**/**除**块。 尽管无需将使用缓冲的 I/O 的 IRP 基于操作的引用**尝试**/**除**块是一项安全预防措施。

 

 




