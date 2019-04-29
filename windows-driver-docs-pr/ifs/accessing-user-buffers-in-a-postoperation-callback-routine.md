---
title: 访问后操作回调例程中的用户缓冲区
description: 访问后操作回调例程中的用户缓冲区
ms.assetid: a980f302-6fde-461e-8b11-313530aff350
keywords:
- postoperation 回调例程 WDK 文件系统微筛选器，缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39741d70ed2e6e1aff05b67550911b7bf5588a11
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323241"
---
# <a name="accessing-user-buffers-in-a-postoperation-callback-routine"></a>访问后操作回调例程中的用户缓冲区


## <span id="ddk_accessing_user_buffers_in_a_postoperation_callback_routine_if"></span><span id="DDK_ACCESSING_USER_BUFFERS_IN_A_POSTOPERATION_CALLBACK_ROUTINE_IF"></span>


微筛选器驱动程序[ **postoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551107)应将缓冲区的基于 IRP 的 I/O 操作，如下所示：

-   检查缓冲区是否存在 MDL。 可在 MDL 指针*MdlAddress*或*OutputMdlAddress*中的参数[ **FLT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff544673)为该操作。 微筛选器驱动程序可以调用[ **FltDecodeParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff541956) MDL 指针的查询。

    一种方法可以获取有效 MDL 所查找 IRP\_MN\_MDL 标志**MinorFunction** I/O 参数块，成员[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)中的回调数据。 下面的示例演示如何检查 IRP\_MN\_MDL 标志。

    ```ManagedCPlusPlus
    NTSTATUS status;
    PMDL *ReadMdl = NULL;
    PVOID ReadAddress = NULL;

    if (FlagOn(CallbackData->Iopb->MinorFunction, IRP_MN_MDL))
    {
        ReadMdl = &CallbackData->Iopb->Parameters.Read.MdlAddress;
    }
    ```

    但是，IRP\_MN\_MDL 标志可设置仅为读取和写入操作。 最好是使用[ **FltDecodeParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff541956)检索 MDL，因为该例程检查有效 MDL 的任何操作。 在以下示例中，如果有效，则返回仅 MDL 参数。

    ```ManagedCPlusPlus
    NTSTATUS status;
    PMDL *ReadMdl = NULL;
    PVOID ReadAddress = NULL;

    status = FltDecodeParameters(CallbackData, &ReadMdl, NULL, NULL, NULL);
    ```

-   如果 MDL 缓冲区存在，则调用[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559)获取缓冲区的系统地址，然后使用此地址来访问缓冲区。 (**MmGetSystemAddressForMdlSafe**可以在 IRQL 调用&lt;= 调度\_级别。)

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

-   如果没有 MDL 缓冲区，检查是否系统缓冲区标志设置为该操作通过使用[ **FLT\_IS\_系统\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff544663)宏。

    -   如果 FLT\_IS\_系统\_缓冲区宏将返回**TRUE**，该操作使用缓冲的 I/O 和缓冲区可以安全地访问在 IRQL = 调度\_级别。

    -   如果 FLT\_IS\_系统\_缓冲区宏将返回**FALSE**，缓冲区无法安全地访问在 IRQL = 调度\_级别。 如果可以在调度调用 postoperation 回调例程\_级别，它必须调用[ **FltDoCompletionProcessingWhenSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff542047)挂起操作之前可以处理在 IRQL &lt;= APC\_级别。 指向回调例程*SafePostCallback*的参数**FltDoCompletionProcessingWhenSafe**应先调用[ **FltLockUserBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff543371)锁定缓冲区，然后调用[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559)获取缓冲区的系统地址。

Postoperation 回调例程应将缓冲区的快速 I/O 操作，如下所示：

-   使用的缓冲区地址来访问缓冲区 （因为快速 I/O 操作不能具有 MDL）。

-   若要确保用户空间缓冲区地址是否有效，微筛选器驱动程序必须使用一个例程如[ **ProbeForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559876)或[ **ProbeForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559879)，封闭中的所有缓冲区引用**尝试**/**除**块。

-   快速的 I/O 操作的 postoperation 回调例程保证在正确的线程上下文中调用。

-   快速 I/O 操作的 postoperation 回调例程保证调用在 IRQL &lt;= APC\_级别，因此如可以安全地调用例程[ **FltLockUserBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff543371)。

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

 

 




