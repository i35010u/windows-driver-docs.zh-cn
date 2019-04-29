---
title: 文件系统控制处理
description: 文件系统控制处理
ms.assetid: 95a610c8-b48c-4fff-bf1f-f9fb6abb0fd9
keywords:
- 安全 WDK 文件系统，语义模型检查
- 语义模型检查 WDK 的文件系统控制处理
- FILE_SPECIAL_ACCESS
- FSCTL_MOVE_FILE
- 控制处理 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0035ec5d7ec3110d1f261d97f88eea0c1beed0d5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383833"
---
# <a name="file-system-control-processing"></a>文件系统控制处理


## <span id="ddk_file_system_control_processing_if"></span><span id="DDK_FILE_SYSTEM_CONTROL_PROCESSING_IF"></span>


处理[ **IRP\_MJ\_文件\_系统\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff548670)操作是不同于所需的其他操作的数据缓冲区处理在文件系统中。 这是因为每个操作建立其特定的数据传输机制 I/O 管理器作为其控制代码的一部分通过 CTL\_代码宏。 此外，控制代码指定由调用方所需的文件访问权限。 文件系统特别留意此问题时应定义控制代码，因为由 I/O 管理器强制执行此访问权限。 某些 I/O 控制代码 (FSCTL\_移动\_文件，如) 指定文件\_特殊\_访问权限，这是一种机制允许文件系统，以指示将由文件检查操作的安全直接系统。 文件\_特殊\_访问权限是按数字顺序等效于文件\_ANY\_访问，因此在 I/O 管理器不提供任何特定的安全检查，而推迟到文件系统。 文件\_特殊\_访问主要提供额外的检查将由文件系统的文档。

多个文件系统操作指定文件\_特殊\_访问。 FSCTL\_移动\_文件操作用作文件系统碎片整理程序界面的一部分，并指定文件\_特殊\_访问。 由于您希望能够进行碎片整理正在积极的打开的文件读取和写入，句柄用于具有只有文件\_读取\_属性授予访问权限，以避免共享访问冲突。 但是，此操作必须是一项特权的操作，因为正在低级别上修改磁盘。 解决方法是验证该句柄用于发出 FSCTL\_移动\_文件是一个直接访问存储设备 (DASD) 用户卷打开，这是特权句柄。 正在 FASTFAT 文件系统代码，以确保此操作对打开的用户卷处于**FatMoveFile**函数 （请参阅 fsctrl.c 源文件从 WDK 包含 fastfat 示例）：

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

结构，可由 FSCTL\_移动\_文件操作指定要移动的文件：

```cpp
typedef struct {
    HANDLE FileHandle;
    LARGE_INTEGER StartingVcn;
    LARGE_INTEGER StartingLcn;
    ULONG ClusterCount;
} MOVE_FILE_DATA, *PMOVE_FILE_DATA;
```

正如前面提到，用于发出 FSCTL 的句柄\_移动\_文件是整个卷时，"打开"操作，而该操作实际应用到移动中指定的文件句柄\_文件\_数据输入缓冲区。 这使得此操作的安全检查有些复杂。 例如，此接口必须将文件句柄转换为表示要移动的文件的文件对象。 这需要仔细考虑任何驱动程序的部分。 FASTFAT 是使用[ **ObReferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff558678)以在受保护的方式**FatMoveFile** WDK 包含 fastfat 示例中的 fsctrl.c 源代码文件中的函数：

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

请注意，使用 Irp-&gt;RequestorMode 以确保如果调用方是在用户模式应用程序，该句柄不能为内核句柄。 所需的权限为 0，以便可以移动文件，而正在积极地访问它。 和最后请注意，如果在用户模式下发起调用，必须在正确的进程上下文中进行此调用。 这也在强制 FASTFAT 文件系统中的源代码**FatMoveFile** fsctrl.c 中的函数：

```cpp
    //
    //  Force WAIT to true. There is a handle in the input buffer that can only
    //  be referenced within the originating process.
    //

    SetFlag( IrpContext->Flags, IRP_CONTEXT_FLAG_WAIT );
```

所需的任何操作都将传递一个句柄的文件系统的典型 FAT 文件系统执行这些语义安全检查。 此外，FAT 文件系统还必须执行特定于操作的完整性检查。 这些完整性检查是确保完全不同的参数兼容 （正在移动的文件是已打开，例如在卷上） 以防止调用方执行一项特权的操作时不应该被允许。

对于任何文件系统，正确安全性是必不可少的组成部分的文件系统控制操作，其中包括：

-   适当地验证用户句柄。

-   保护用户缓冲区的访问权限。

-   正在验证的特定操作的语义。

在许多情况下，执行适当的验证和安全所必需的代码可能构成大部分中给定的函数的代码。

 

 




