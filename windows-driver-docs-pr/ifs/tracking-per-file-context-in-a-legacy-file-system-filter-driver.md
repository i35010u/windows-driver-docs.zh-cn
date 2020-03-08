---
title: 跟踪旧文件系统筛选器驱动程序中的按文件上下文
description: 跟踪旧文件系统筛选器驱动程序中的按文件上下文
ms.assetid: 6be3ff10-47e4-47f5-8f15-88a80a16f451
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e991bb3148fb552f93196f8fface4891c6956d3
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910454"
---
# <a name="tracking-per-file-context-in-a-legacy-file-system-filter-driver"></a>跟踪旧文件系统筛选器驱动程序中的按文件上下文

> [!NOTE]
> 为了获得最佳的可靠性和性能，请使用带有筛选器管理器支持的[文件系统微筛选器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-concepts)，而不是使用旧的文件系统 若要将旧驱动程序移植到微筛选器驱动程序，请参阅[迁移旧筛选器驱动程序的准则](guidelines-for-porting-legacy-filter-drivers.md)。

旧式文件系统筛选器驱动程序可以通过将[**FSRTL_PER_FILE_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsrtl_per_file_context)对象与用户定义的上下文信息结构关联来记录文件的上下文信息。

> [!NOTE]
> 并非所有文件系统都支持每文件上下文对象。 若要确定文件是否与支持它们的文件系统相关联，请使用[**FsRtlSupportsPerFileContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlsupportsperfilecontexts)宏。

使用[**FsRtlInitPerFileContext**](https://docs.microsoft.com/previous-versions/ff546161(v=vs.85))宏初始化 FSRTL_PER_FILE_CONTEXT 的对象。 然后，使用[**FsRtlInsertPerFileContext**](https://msdn.microsoft.com/library/windows/hardware/ff546184)例程将该文件与任意上下文对象相关联。

使用[**FsRtlGetPerFileContextPointer**](https://docs.microsoft.com/previous-versions/ff546051(v=vs.85))宏获取文件系统运行时库（FSRTL）包用来跟踪文件上下文的指针。

筛选器驱动程序可以使用[**FsRtlLookupPerFileContext**](https://msdn.microsoft.com/library/windows/hardware/ff546930)例程查找与文件关联的文件上下文对象。 例程可以指定结构的所有者或结构的实例，以缩小搜索范围。

筛选器驱动程序可以通过使用[**FsRtlRemovePerFileContext**](https://msdn.microsoft.com/library/windows/hardware/ff547226)删除上下文对象。 例程可以指定结构的所有者或结构的实例，以缩小搜索范围。

> [!NOTE]
> 仅当文件仍处于打开状态时，才使用[**FsRtlRemovePerFileContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlremoveperfilecontext)例程删除上下文对象。 不要将其与[**FsRtlTeardownPerFileContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlteardownperfilecontexts)混淆。

文件系统调用[**FsRtlTeardownPerFileContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlteardownperfilecontexts) ，以释放任何仍与每个文件控制块结构（FCB）关联的筛选器上下文，它们会撕裂。 **FsRtlTeardownPerFileContexts**例程调用每个筛选器上下文的 FSRTL_PER_FILE_CONTEXT 对象中指定的[**FreeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ifs/pfree-function)例程。
