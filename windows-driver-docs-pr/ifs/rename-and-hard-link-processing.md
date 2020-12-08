---
title: 重命名和硬链接处理
description: 重命名和硬链接处理
keywords:
- 安全 WDK 文件系统，语义模型检查
- 语义模型检查 WDK 文件系统，重命名操作
- 重命名操作 WDK 文件系统
- 语义模型检查 WDK 文件系统、硬链接操作
- 硬链接操作 WDK 文件系统
- 命名 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae48eb05f2a89438804296eb6a9c0a64e96b5e68
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840717"
---
# <a name="rename-and-hard-link-processing"></a>重命名和硬链接处理


## <span id="ddk_rename_and_hard_link_processing_if"></span><span id="DDK_RENAME_AND_HARD_LINK_PROCESSING_IF"></span>


文件系统的一个特别关注的方面是正确处理重命名操作。 需要考虑的一个类似领域是支持硬链接的文件系统的硬链接创建。 对于重命名操作，文件系统可能会)  (重命名操作的目标删除文件，这需要文件系统进行其他安全检查。

查看用于重命名操作的控制结构时，其中一个结构字段是 **ReplaceIfExists** 选项：

```cpp
typedef struct _FILE_RENAME_INFORMATION {
    BOOLEAN ReplaceIfExists;
    HANDLE RootDirectory;
    ULONG FileNameLength;
    WCHAR FileName[1];
} FILE_RENAME_INFORMATION, *PFILE_RENAME_INFORMATION;
```

同样，在硬链接操作的控制结构中，其中一个结构字段是 **ReplaceIfExists** 选项：

```cpp
typedef struct _FILE_LINK_INFORMATION {
    BOOLEAN ReplaceIfExists;
    HANDLE RootDirectory;
    ULONG FileNameLength;
    WCHAR FileName[1];
} FILE_LINK_INFORMATION, *PFILE_LINK_INFORMATION;
```

在这两种情况下，选项是替换操作的目标（如果存在）。 尽管 FASTFAT 文件系统不支持硬链接，但它确实支持重命名操作。 可以在 **FatSetRenameInfo** 函数的 FASTFAT 文件系统源代码中看到这些语义和行为 (请参阅 WDK 包含) 的 FASTFAT 示例中的 *Fileinfo* 源文件。

下面的代码示例用于处理重命名操作，模拟文件系统检查是否有删除文件。 对于具有更可靠安全模型 (NTFS 的文件系统，例如) ，此检查还需要进行安全检查，以确保允许调用方删除给定文件， (调用方具有删除) 所需的相应权限。

```cpp
    //
    //  The name already exists. Check if the user wants
    //  to overwrite the name and has access to do the overwrite.
    //  We cannot overwrite a directory.
    //

    if ((!ReplaceIfExists) ||
        (FlagOn(TargetDirent->Attributes, FAT_DIRENT_ATTR_DIRECTORY)) || 
        (FlagOn(TargetDirent->Attributes, FAT_DIRENT_ATTR_READ_ONLY))) {

        try_return( Status = STATUS_OBJECT_NAME_COLLISION );
    }

    //
    //  Check that the file has no open user handles; otherwise, 
    //  access will be denied. To do the check, search
    //  the list of FCBs opened under the parent Dcb, and make
    //  sure that none of the matching FCBs have a nonzero unclean count or
    //  outstanding image sections.
    //

    for (Links = TargetDcb->Specific.Dcb.ParentDcbQueue.Flink;
            Links != &TargetDcb->Specific.Dcb.ParentDcbQueue; ) {

        TempFcb = CONTAINING_RECORD( Links, FCB, ParentDcbLinks );

        //
        //  Advance now. The image section flush may cause the final
        //  close, which will recursively happen underneath of us here.
        //  It would be unfortunate if we looked through free memory.
        //

        Links = Links->Flink;

        if ((TempFcb->DirentOffsetWithinDirectory == TargetDirentOffset) &&
                ((TempFcb->UncleanCount != 0) ||
                !MmFlushImageSection( &TempFcb->NonPaged->SectionObjectPointers,
                MmFlushForDelete))) {

            //
            //  If there are batch oplocks on this file, then break the
            //  oplocks before failing the rename.
            //

            Status = STATUS_ACCESS_DENIED;

            if ((NodeType(TempFcb) == FAT_NTC_FCB) &&
                    FsRtlCurrentBatchOplock( &TempFcb->Specific.Fcb.Oplock )) {

                //
                //  Do all of the cleanup now since the IrpContext
                //  could go away when this request is posted.
                //

                FatUnpinBcb( IrpContext, TargetDirentBcb );

                Status = FsRtlCheckOplock( &TempFcb->Specific.Fcb.Oplock,
                    Irp,
                    IrpContext,
                    FatOplockComplete,
                    NULL );

                if (Status != STATUS_PENDING) {

                    Status = STATUS_ACCESS_DENIED;
                }
            }

            try_return( NOTHING );
        }
    }

    //
    //  OK, this target is finished. Remember the Lfn offset.
    //

    TargetLfnOffset = TargetDirentOffset -
        FAT_LFN_DIRENTS_NEEDED(&TargetLfn) * sizeof(DIRENT);

    DeleteTarget = TRUE;
}
```

 

 




