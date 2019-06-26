---
title: 跟踪旧文件系统筛选器驱动程序中的按文件上下文
description: 跟踪旧文件系统筛选器驱动程序中的按文件上下文
ms.assetid: 6be3ff10-47e4-47f5-8f15-88a80a16f451
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 573738ed2128abd0ce9024eec78febb66b8d421e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380321"
---
# <a name="tracking-per-file-context-in-a-legacy-file-system-filter-driver"></a>跟踪旧文件系统筛选器驱动程序中的按文件上下文


<div class="alert">
<strong>请注意</strong>最佳的可靠性和性能，我们建议使用<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">文件系统微筛选器驱动程序</a>而不是旧的文件系统筛选器驱动程序。 此外，旧的文件系统筛选器驱动程序不能将附加到直接访问 (DAX) 卷。 有关文件系统微筛选器驱动程序的详细信息，请参阅<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">筛选器管理器模型的优势</a>。 若要移植到微筛选器驱动程序的传统的驱动程序，请参阅<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">移植旧筛选器驱动程序的指导原则</a>。
</div>
 

旧的文件系统筛选器驱动程序可以通过将关联记录的文件的上下文信息[ **FSRTL\_每\_文件\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff547352)具有用户定义对象上下文信息结构。

<div class="alert">
<strong>请注意</strong>不是所有的文件系统支持每个文件上下文对象。 若要了解文件是否支持它们的文件系统与相关联，请使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlsupportsperfilecontexts" data-raw-source="[**FsRtlSupportsPerFileContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlsupportsperfilecontexts)"> <strong>FsRtlSupportsPerFileContexts</strong> </a>宏。
</div>
 

使用[ **FsRtlInitPerFileContext** ](https://docs.microsoft.com/previous-versions/ff546161(v=vs.85))宏来初始化 FSRTL\_每\_文件\_上下文对象。 然后，使用[ **FsRtlInsertPerFileContext** ](https://msdn.microsoft.com/library/windows/hardware/ff546184)例程，以将该文件与任意上下文对象相关联。

使用[ **FsRtlGetPerFileContextPointer** ](https://docs.microsoft.com/previous-versions/ff546051(v=vs.85))宏来获取文件系统运行时库 (FSRTL) 包用来跟踪文件上下文的指针。

可以使用筛选器驱动程序[ **FsRtlLookupPerFileContext** ](https://msdn.microsoft.com/library/windows/hardware/ff546930)例程，以查找与文件相关联的文件上下文对象。 例程可以指定要缩小搜索范围结构或结构的实例的所有者。

筛选器驱动程序可通过删除上下文对象[ **FsRtlRemovePerFileContext**](https://msdn.microsoft.com/library/windows/hardware/ff547226)。 例程可以指定要缩小搜索范围结构或结构的实例的所有者。

<div class="alert">
<strong>请注意</strong>只用<a href="https://msdn.microsoft.com/library/windows/hardware/ff547226" data-raw-source="[**FsRtlRemovePerFileContext**](https://msdn.microsoft.com/library/windows/hardware/ff547226)"> <strong>FsRtlRemovePerFileContext</strong> </a>例程，以删除上下文对象，而该文件仍处于打开状态。 请将其与混淆<a href="https://msdn.microsoft.com/library/windows/hardware/ff547290" data-raw-source="[**FsRtlTeardownPerFileContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547290)"> <strong>FsRtlTeardownPerFileContexts</strong></a>。
</div>
 

文件系统调用[ **FsRtlTeardownPerFileContexts** ](https://msdn.microsoft.com/library/windows/hardware/ff547290)以释放任何与他们关闭每个文件控制块结构 (FCB) 仍关联的筛选器上下文。 **FsRtlTeardownPerFileContexts**例程调用[ **FreeCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/pfree-function) FSRTL 中指定的例程\_每\_文件\_每个筛选器上下文的上下文对象。

 

 




