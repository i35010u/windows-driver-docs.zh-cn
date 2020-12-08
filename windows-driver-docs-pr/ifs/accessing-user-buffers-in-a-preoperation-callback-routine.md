---
title: 访问预操作回调例程中的用户缓冲区
description: 访问预操作回调例程中的用户缓冲区
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7f4b4321f35dceb2c5ba5cd9400b6404228f27a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816291"
---
# <a name="accessing-user-buffers-in-a-preoperation-callback-routine"></a>访问预操作回调例程中的用户缓冲区


## <span id="ddk_accessing_user_buffers_in_a_preoperation_callback_routine_if"></span><span id="DDK_ACCESSING_USER_BUFFERS_IN_A_PREOPERATION_CALLBACK_ROUTINE_IF"></span>


微筛选器驱动程序的 [**preoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback) 应在基于 IRP 的 i/o 操作中处理缓冲区，如下所示：

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

-   如果缓冲区存在 MDL，请调用 [**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md) 获取缓冲区的系统地址，然后使用此地址访问缓冲区。

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

-   如果缓冲区没有 MDL，请使用缓冲区地址访问缓冲区。 若要确保用户空间缓冲区的地址有效，微筛选器驱动程序必须使用 [**ProbeForRead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)或 [**ProbeForWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)等例程，并在 **try** / **except** 块中包含所有缓冲区引用。

Preoperation 回调例程应按如下所示在快速 i/o 操作中处理缓冲区：

-   使用缓冲区地址访问缓冲区 (因为快速 i/o 操作不能具有 MDL) 。

-   若要确保用户空间缓冲区的地址有效，微筛选器驱动程序必须使用 **ProbeForRead** 或 **ProbeForWrite** 等例程，并在 **try** / **except** 块中包含所有缓冲区引用。

对于可以是快速 i/o 或基于 IRP 的操作，所有缓冲区引用应包含在 **try** / **except** 块中。 尽管不需要将这些引用包含在使用缓冲 i/o 的基于 IRP 的操作中，但 **try** / **except** 块是一项安全预防措施。

 

