---
title: 可执行映像
description: 可执行映像
keywords:
- 安全 WDK 文件系统，语义模型检查
- 语义模型检查 WDK 文件系统和可执行映像
- 可执行映像 WDK 文件系统
- 内存映射文件 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 001d556a029d0a74e7c9ae2781794afe4ed197ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826535"
---
# <a name="executable-images"></a>可执行映像


## <span id="ddk_executable_images_if"></span><span id="DDK_EXECUTABLE_IMAGES_IF"></span>


可执行文件将加载到使用内存映射映像文件的进程的地址空间中。 不需要打开文件本身，也不需要创建句柄，因为映射是通过节来完成的。 如果文件系统支持内存映射文件，则必须检查这些特殊语义。 例如，可以从 WDK 包含的 FASTFAT 示例中的 FatOpenExistingFCB 函数的 **FatOpenExistingFCB** 函数中找到用于检查此情况的 FASTFAT 文件系统代码：

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

因此，即使文件未打开，文件系统也可以确保无法删除内存映射文件（包括可执行映像）。

 

 




