---
title: 访问预操作回调例程中的用户缓冲区
description: 访问预操作回调例程中的用户缓冲区
ms.assetid: 16e6a9e0-3a92-471f-98e6-9a4e8eb7d4a6
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fc8ab417505dac51cdf72f2df33ce7cabc0d384
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841503"
---
# <a name="accessing-user-buffers-in-a-preoperation-callback-routine"></a>访问预操作回调例程中的用户缓冲区


## <span id="ddk_accessing_user_buffers_in_a_preoperation_callback_routine_if"></span><span id="DDK_ACCESSING_USER_BUFFERS_IN_A_PREOPERATION_CALLBACK_ROUTINE_IF"></span>


微筛选器驱动程序的[**preoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)应在基于 IRP 的 i/o 操作中处理缓冲区，如下所示：

-   检查缓冲区是否存在 MDL。 可以在操作的[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)的*MdlAddress*或*OutputMdlAddress*参数中找到 MDL 指针。 微筛选器驱动程序可以调用[**FltDecodeParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdecodeparameters)来查询 MDL 指针。

    获取有效 MDL 的一种方法是在回调数据中查找 i/o 参数块的**MinorFunction**成员中的 IRP\_MN\_MDL 标志， [**FLT\_IO\_参数\_block**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)。 下面的示例演示如何检查 IRP\_MN\_MDL 标志。

    ```ManagedCPlusPlus
    NTSTATUS status;
    PMDL *ReadMdl = NULL;
    PVOID ReadAddress = NULL;

    if (FlagOn(CallbackData->Iopb->MinorFunction, IRP_MN_MDL))
    {
        ReadMdl = &CallbackData->Iopb->Parameters.Read.MdlAddress;
    }
    ```

    但是，只能为读写操作设置 IRP\_MN\_MDL 标志。 最好使用[**FltDecodeParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdecodeparameters)检索 MDL，因为例程检查任何操作是否有有效的 mdl。 在以下示例中，如果有效，则仅返回 MDL 参数。

    ```ManagedCPlusPlus
    NTSTATUS status;
    PMDL *ReadMdl = NULL;
    PVOID ReadAddress = NULL;

    status = FltDecodeParameters(CallbackData, &ReadMdl, NULL, NULL, NULL);
    ```

-   如果缓冲区存在 MDL，请调用[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)获取缓冲区的系统地址，然后使用此地址访问缓冲区。

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

-   如果缓冲区没有 MDL，请使用缓冲区地址访问缓冲区。 若要确保用户空间缓冲区的地址有效，微筛选器驱动程序必须使用[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)或[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)等例程，并在**try**/**except**块中包含所有缓冲区引用。

Preoperation 回调例程应按如下所示在快速 i/o 操作中处理缓冲区：

-   使用缓冲区地址访问缓冲区（因为快速 i/o 操作不能具有 MDL）。

-   若要确保用户空间缓冲区的地址有效，微筛选器驱动程序必须使用**ProbeForRead**或**ProbeForWrite**等例程，并在**try**/**except**块中包含所有缓冲区引用。

对于可以是快速 i/o 或基于 IRP 的操作，所有缓冲区引用都应括在**try**/**除了**块。 尽管不需要将这些引用包含在使用缓冲 i/o 的基于 IRP 的操作中，但**try**/**例外**块是一项安全预防措施。

 

 




