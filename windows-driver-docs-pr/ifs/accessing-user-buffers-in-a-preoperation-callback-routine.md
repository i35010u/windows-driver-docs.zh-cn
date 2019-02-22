---
title: 访问 Preoperation 回调例程中的用户缓冲区
description: 访问 Preoperation 回调例程中的用户缓冲区
ms.assetid: 16e6a9e0-3a92-471f-98e6-9a4e8eb7d4a6
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7c35fcc95ff83f74a42d07ff95c6b8860d57d8f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523656"
---
# <a name="accessing-user-buffers-in-a-preoperation-callback-routine"></a>访问 Preoperation 回调例程中的用户缓冲区


## <span id="ddk_accessing_user_buffers_in_a_preoperation_callback_routine_if"></span><span id="DDK_ACCESSING_USER_BUFFERS_IN_A_PREOPERATION_CALLBACK_ROUTINE_IF"></span>


微筛选器驱动程序[ **preoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551109)应将缓冲区的基于 IRP 的 I/O 操作，如下所示：

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

-   如果 MDL 缓冲区存在，则调用[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559)获取缓冲区的系统地址，然后使用此地址来访问缓冲区。

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

-   如果没有 MDL 缓冲区，使用的缓冲区地址来访问缓冲区。 若要确保用户空间缓冲区地址是否有效，微筛选器驱动程序必须使用一个例程如[ **ProbeForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559876)或[ **ProbeForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559879)，封闭中的所有缓冲区引用**尝试**/**除**块。

Preoperation 回调例程应将缓冲区的快速 I/O 操作，如下所示：

-   使用的缓冲区地址来访问缓冲区 （因为快速 I/O 操作不能具有 MDL）。

-   若要确保用户空间缓冲区地址是否有效，微筛选器驱动程序必须使用一个例程如**ProbeForRead**或**ProbeForWrite**，封闭中的所有缓冲区引用**尝试**/**除**块。

有关可快速 I/O 操作或基于 IRP 的所有缓冲区引用应都括在**尝试**/**除**块。 尽管无需将使用缓冲的 I/O 的 IRP 基于操作的引用**尝试**/**除**块是一项安全预防措施。

 

 




