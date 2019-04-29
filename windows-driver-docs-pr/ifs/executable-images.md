---
title: 可执行映像
description: 可执行映像
ms.assetid: ca279a74-5f30-4413-bf1c-4d5af12d294d
keywords:
- 安全 WDK 文件系统，语义模型检查
- 语义模型检查 WDK 的文件系统，可执行映像
- WDK 的文件系统的可执行映像
- 内存映射文件 WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac55025cb80e76c4f9a0acae0d2e53bd3ac74f93
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383844"
---
# <a name="executable-images"></a>可执行映像


## <span id="ddk_executable_images_if"></span><span id="DDK_EXECUTABLE_IMAGES_IF"></span>


可执行文件加载到使用内存映射的图像文件的进程的地址空间。 文件本身不需要打开，也不会句柄需要创建，因为映射通过部分完成的。 必须检查文件系统来强制执行这些特殊语义，假定它们支持内存映射文件。 例如中, 找到 FASTFAT 文件系统代码以检查这种情况下**FatOpenExistingFCB** Create.c 源文件从 WDK 包含 fastfat 示例中的函数：

```cpp
    //
    //  If the user wants write access to the file, make sure there
    //  is not a process mapping this file as an image. Any attempt to
    //  delete the file will be stopped in fileinfo.c
    //
    //  If the user wants to delete on close, check at this
    //  point though.
    //

    if (FlagOn(*DesiredAccess, FILE_WRITE_DATA) || DeleteOnClose) {

        Fcb->OpenCount += 1;
        DecrementFcbOpenCount = TRUE;

        if (!MmFlushImageSection( &Fcb->NonPaged->SectionObjectPointers,
                                  MmFlushForWrite )) {

            Iosb.Status = DeleteOnClose ? STATUS_CANNOT_DELETE :STATUS_SHARING_VIOLATION;
            try_return( Iosb );
        }
    }
```

因此，文件系统可确保即使该文件未打开，不能删除内存映射的文件，其中包括一个可执行文件的映像。

 

 




