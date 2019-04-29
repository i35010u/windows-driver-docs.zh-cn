---
title: 重命名和硬链接处理
description: 重命名和硬链接处理
ms.assetid: 53eb3c9b-cb48-4d5f-8e26-dc93b7607813
keywords:
- 安全 WDK 文件系统，语义模型检查
- 语义模型检查 WDK 文件系统中，重命名操作
- 重命名操作 WDK 的文件系统
- 语义模型检查 WDK 的文件系统，硬链接操作
- 硬链接操作 WDK 文件系统
- 名称 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 781e954139ec90a2085b75c49b9e27855f6ead1b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365922"
---
# <a name="rename-and-hard-link-processing"></a>重命名和硬链接处理


## <span id="ddk_rename_and_hard_link_processing_if"></span><span id="DDK_RENAME_AND_HARD_LINK_PROCESSING_IF"></span>


对于文件系统的特定需要关注的方面是正确处理重命名操作。 考虑类似区域都是问题的支持硬链接的文件系统的硬链接创建。 对于重命名操作，就可以删除额外的安全检查所需的文件系统的文件 （重命名操作的目标） 的文件系统。

在查看时重命名操作的控制结构，结构字段之一是**ReplaceIfExists**选项：

```cpp
typedef struct _FILE_RENAME_INFORMATION {
    BOOLEAN ReplaceIfExists;
    HANDLE RootDirectory;
    ULONG FileNameLength;
    WCHAR FileName[1];
} FILE_RENAME_INFORMATION, *PFILE_RENAME_INFORMATION;
```

同样，硬链接操作的控制结构中的结构字段之一是**ReplaceIfExists**选项：

```cpp
typedef struct _FILE_LINK_INFORMATION {
    BOOLEAN ReplaceIfExists;
    HANDLE RootDirectory;
    ULONG FileNameLength;
    WCHAR FileName[1];
} FILE_LINK_INFORMATION, *PFILE_LINK_INFORMATION;
```

在这两种情况下，选项将替换为目标的操作，如果它存在。 虽然 FASTFAT 文件系统不支持的硬链接，但它支持重命名操作。 中的 FASTFAT 文件系统源代码中可以看到这些语义和行为**FatSetRenameInfo**函数 (请参阅*Fileinfo.c*从 WDK 包含 fastfat 示例的源文件)。

下面的代码示例，以处理重命名操作模仿用于删除该文件的文件系统检查。 与更强大的安全的文件系统的模型 (例如 NTFS)，此检查还需要安全检查以确保允许调用方删除给定的文件 （调用方必须为要删除所需的相应权限）。

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

 

 




