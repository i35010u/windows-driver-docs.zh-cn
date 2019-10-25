---
title: 跟踪旧文件系统筛选器驱动程序中的按文件上下文
description: 跟踪旧文件系统筛选器驱动程序中的按文件上下文
ms.assetid: 6be3ff10-47e4-47f5-8f15-88a80a16f451
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be0a78af1a8bbd352c3f17c43c0a36a694ffd3bd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840948"
---
# <a name="tracking-per-file-context-in-a-legacy-file-system-filter-driver"></a>跟踪旧文件系统筛选器驱动程序中的按文件上下文


<div class="alert">
<strong>注意</strong>  为了获得最佳的可靠性和性能，我们建议使用<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">文件系统微筛选器驱动程序</a>，而不是旧的文件系统筛选器驱动程序。 此外，旧文件系统筛选器驱动程序不能附加到直接访问（DAX）卷。 有关文件系统微筛选器驱动程序的详细信息，请参阅<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">筛选器管理器模型的优点</a>。 若要将旧驱动程序移植到微筛选器驱动程序，请参阅<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">迁移旧筛选器驱动程序的准则</a>。
</div>
 

旧式文件系统筛选器驱动程序可以通过将[**FSRTL\_每\_文件\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff547352)对象与用户定义的上下文信息结构关联来记录文件的上下文信息。

<div class="alert">
<strong>注意</strong>  并非所有文件系统都支持每文件上下文对象。 若要确定文件是否与支持它们的文件系统相关联，请使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlsupportsperfilecontexts" data-raw-source="[**FsRtlSupportsPerFileContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlsupportsperfilecontexts)"><strong>FsRtlSupportsPerFileContexts</strong></a>宏。
</div>
 

使用[**FsRtlInitPerFileContext**](https://docs.microsoft.com/previous-versions/ff546161(v=vs.85))宏\_上下文对象初始化每\_文件的 FSRTL\_。 然后，使用[**FsRtlInsertPerFileContext**](https://msdn.microsoft.com/library/windows/hardware/ff546184)例程将该文件与任意上下文对象相关联。

使用[**FsRtlGetPerFileContextPointer**](https://docs.microsoft.com/previous-versions/ff546051(v=vs.85))宏获取文件系统运行时库（FSRTL）包用来跟踪文件上下文的指针。

筛选器驱动程序可以使用[**FsRtlLookupPerFileContext**](https://msdn.microsoft.com/library/windows/hardware/ff546930)例程查找与文件关联的文件上下文对象。 例程可以指定结构的所有者或结构的实例，以缩小搜索范围。

筛选器驱动程序可以通过使用[**FsRtlRemovePerFileContext**](https://msdn.microsoft.com/library/windows/hardware/ff547226)删除上下文对象。 例程可以指定结构的所有者或结构的实例，以缩小搜索范围。

<div class="alert">
<strong>注意</strong>  仅当文件仍处于打开状态时，才使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff547226" data-raw-source="[**FsRtlRemovePerFileContext**](https://msdn.microsoft.com/library/windows/hardware/ff547226)"><strong>FsRtlRemovePerFileContext</strong></a>例程删除上下文对象。 不要将其与<a href="https://msdn.microsoft.com/library/windows/hardware/ff547290" data-raw-source="[**FsRtlTeardownPerFileContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547290)"><strong>FsRtlTeardownPerFileContexts</strong></a>混淆。
</div>
 

文件系统调用[**FsRtlTeardownPerFileContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547290) ，以释放任何仍与每个文件控制块结构（FCB）关联的筛选器上下文，它们会撕裂。 **FsRtlTeardownPerFileContexts**例程调用每个\_文件的 FSRTL\_中指定的[**FreeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ifs/pfree-function)例程，每个筛选器上下文\_上下文对象。

 

 




