---
title: 文件系统控制处理
description: 文件系统控制处理
ms.assetid: 95a610c8-b48c-4fff-bf1f-f9fb6abb0fd9
keywords:
- 安全 WDK 文件系统，语义模型检查
- 语义模型检查 WDK 文件系统，控制处理
- FILE_SPECIAL_ACCESS
- FSCTL_MOVE_FILE
- 控制处理 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca6e30151acc89fbb675ac4ad88e447bcd7399b3
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063672"
---
# <a name="file-system-control-processing"></a>文件系统控制处理


## <span id="ddk_file_system_control_processing_if"></span><span id="DDK_FILE_SYSTEM_CONTROL_PROCESSING_IF"></span>


处理 [**IRP \_ MJ \_ 文件 \_ 系统 \_ 控制**](./irp-mj-file-system-control.md) 操作不同于文件系统中其他操作所需的数据缓冲区处理。 这是因为，每个操作都通过 CTL 代码宏为 i/o 管理器建立其控制代码的一部分的特定数据传输机制 \_ 。 此外，控制代码指定调用方所需的文件访问权限。 定义控制代码时，文件系统应特别 cognizant 此问题，因为这种访问是由 i/o 管理器强制实施的。 某些 i/o 控制代码 (FSCTL \_ 移动 \_ 文件，例如) 指定文件 \_ 特殊 \_ 访问，这是一种允许文件系统指示操作的安全性将由文件系统直接检查的机制。 文件 \_ 特殊 \_ 访问的数值相当于文件 \_ 任何 \_ 访问权限，因此，i/o 管理器不会提供任何特定的安全检查，而是推迟到文件系统。 文件 \_ 特殊 \_ 访问主要提供文档，指出文件系统将执行其他检查。

若干文件系统操作指定文件 \_ 特殊 \_ 访问权限。 FSCTL \_ 移动 \_ 文件操作用作文件系统的碎片整理接口的一部分，它指定文件的 \_ 特殊 \_ 访问权限。 由于你希望能够对正在进行读取和写入的打开文件进行碎片整理，因此要使用的句柄只有文件 \_ 读取 \_ 属性授予了访问权限，以避免共享访问冲突。 但是，在较低级别修改磁盘时，此操作需要为特权操作。 解决方法是验证用于发出 FSCTL 移动文件的句柄 \_ \_ 是否为直接访问存储设备 (DASD) 用户卷是否打开，这是一个特权句柄。 FASTFAT 文件系统代码可确保对已打开的用户卷执行此操作， (请参阅 **FatMoveFile** 函数中的 fsctrl 源文件，该文件来自 WDK 包含) 的 FASTFAT 示例：

```cpp
    //
    //  extract and decode the file object and check for type of open
    //

    if (FatDecodeFileObject( IrpSp->FileObject, &Vcb, &FcbOrDcb, &Ccb ) != UserVolumeOpen) {

        FatCompleteRequest( IrpContext, Irp, STATUS_INVALID_PARAMETER );

        DebugTrace(-1, Dbg, "FatMoveFile -> %08lx\n", STATUS_INVALID_PARAMETER);
        return STATUS_INVALID_PARAMETER;
    }
```

FSCTL \_ 移动文件操作使用的结构 \_ 指定要移动的文件：

```cpp
typedef struct {
    HANDLE FileHandle;
    LARGE_INTEGER StartingVcn;
    LARGE_INTEGER StartingLcn;
    ULONG ClusterCount;
} MOVE_FILE_DATA, *PMOVE_FILE_DATA;
```

如前文所述，用于发出 FSCTL 移动文件的句 \_ 柄 \_ 是整个卷的 "打开" 操作，而操作实际上适用于在移动 \_ 文件数据输入缓冲区中指定的文件句柄 \_ 。 这使得此操作的安全检查稍微复杂一些。 例如，此接口必须将文件句柄转换为表示要移动的文件的文件对象。 这需要仔细考虑任何驱动程序的部分。 FASTFAT 使用 [**ObReferenceObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject) 在 WDK 包含的 FASTFAT 示例的 fsctrl 文件中的 **FatMoveFile** 函数中以受保护的方式执行此操作：

```cpp
    //
    //  Try to get a pointer to the file object from the handle passed in.
    //

    Status = ObReferenceObjectByHandle( InputBuffer->FileHandle,
                                        0,
                                        *IoFileObjectType,
                                        Irp->RequestorMode,
                                        &FileObject,
                                        NULL );

    if (!NT_SUCCESS(Status)) {

        FatCompleteRequest( IrpContext, Irp, Status );

        DebugTrace(-1, Dbg, "FatMoveFile -> %08lx\n", Status);
        return Status;
    }
    //  Complete the following steps to ensure that this is not an invalid attempt
    //
    //    - check that the file object is opened on the same volume as the
    //      DASD handle used to call this routine.
    //
    //    - extract and decode the file object and check for type of open.
    //
    //    - if this is a directory, verify that it's not the root and that
    //      you are not trying to move the first cluster.  You cannot move the
    //      first cluster because sub-directories have this cluster number
    //      in them and there is no safe way to simultaneously update them
    //      all.
    //
    //  Allow movefile on the root directory if it's FAT32, since the root dir
    //  is a real chained file.
    //    //
```

请注意使用 Irp- &gt; irp->requestormode 以确保如果调用方是用户模式应用程序，句柄不能是内核句柄。 所需的访问权限为0，以便文件在主动访问时可以移动。 最后要注意的是，如果调用是以用户模式发出的，则必须在正确的进程上下文中执行此调用。 FASTFAT 文件系统中的源代码也会在 fsctrl 中的 **FatMoveFile** 函数中执行此操作。

```cpp
    //
    //  Force WAIT to true. There is a handle in the input buffer that can only
    //  be referenced within the originating process.
    //

    SetFlag( IrpContext->Flags, IRP_CONTEXT_FLAG_WAIT );
```

FAT 文件系统执行的这些语义安全检查通常是那些传递句柄的操作所要求的文件系统的语义安全检查。 此外，FAT 文件系统还必须执行特定于该操作的性能检查。 这些稳定检查旨在确保完全不同的参数 (兼容的文件位于打开的卷上，例如) ，以防止调用方执行不应允许的特权操作。

对于任何文件系统，正确的安全性都是文件系统控制操作必不可少的部分，其中包括：

-   适当地验证用户句柄。

-   保护用户缓冲区访问。

-   正在验证特定操作的语义。

在许多情况下，执行正确验证和安全所需的代码可以构成给定函数内的大量代码。

 

