---
title: 使用后备链列表
description: 使用后备链列表
ms.assetid: 07a75b8b-04b9-48ea-bda4-53889dd661a9
keywords:
- 内存管理 WDK 内核旁路列表
- 后备链列表 WDK 内核
- 固定大小的缓冲区分配 WDK 内核
- ExXxxLookasideList 例程 WDK
- 条目 WDK 后备链
- 非分页后备链列表 WDK 内核
- 分页后备链列表 WDK 内核
- 分配例程 WDK 内存
- 免费例程 WDK 内存
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0582df0a1cf5966ffdf2a620d0a613a527c68c56
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545856"
---
# <a name="using-lookaside-lists"></a>使用后备链列表





必须分配固定大小缓冲区动态以执行按需 I/O 操作的驱动程序可以使用**Ex*Xxx*LookasideListEx**或**Ex*Xxx*LookasideList**支持例程。 这样的驱动程序初始化其后备链列表后，操作系统将在驱动程序的后备链列表中，有效保留一组的驱动程序的可重用、 固定大小缓冲区中保留一定数量的给定大小的动态分配的缓冲区。 格式和驱动程序的固定大小缓冲区的内容 (也称为*条目*) 在其后备链列表中将驱动程序确定。

例如，必须设置为基础的 SCSI 端口/微型端口驱动程序的 SCSI 请求块 (Srb) 的存储类驱动程序使用后备链列表。 这样的类驱动程序分配缓冲区的 Srb 上按需从其后备链列表，并释放每个 SRB 缓冲区返回到后备链列表时 SRB 返回到的类驱动程序中已完成的 IRP 随时重用的后备链列表。 因为存储类驱动程序无法预先确定多少 Srb 它必须使用在任何时间，因为该驱动程序的 I/O 需求增加且落，后备链列表是一种方便且经济的方法来管理分配和解除分配的缓冲区的大小固定 Srb在此类驱动程序。

操作系统维护有关当前正在使用，动态跟踪分配和释放的所有列表中的条目的需求和可用的系统池的新条目的所有分页和非分页后备链列表的状态。 如果对分配的需求较高，操作系统会增加它保留每个后备链列表中的条目数。 如果需求降低再次，它会释放回系统池多余后备链条目。

后备链列表是线程安全。 后备链列表具有内置的同步，若要启用多个并发运行的线程中驱动程序即可共享后备链列表。 这些线程可以安全地分配从共享的后备缓冲区，以及释放列表为这些缓冲区而无需显式同步这些操作的驱动程序。 但是，若要避免可能泄漏和数据损坏，一组共享后备链列表的线程必须显式同步的初始化和删除的列表。

## <a name="lookaside-list-interfaces"></a>后备链列表接口


从 Windows Vista 开始[**后备链\_列表\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff554329)结构描述后备链列表可以包含分页或非分页缓冲区。 如果驱动程序提供自定义*分配*并*免费*例程后备链列表中，对于这些例程收到作为输入参数的专用上下文。 驱动程序可以使用此上下文的后备链列表的私有数据收集。 例如，可能会使用上下文进行计数的动态分配和释放列表的列表项。 有关演示如何在这种方式中使用上下文的代码示例，请参阅[ **ExInitializeLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff545298)。

系统提供的以下例程支持后备链列表由描述**后备链\_列表\_EX**结构：

[**ExAllocateFromLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544381)

[**ExDeleteLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544563)

[**ExFlushLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544587)

[**ExFreeToLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544597)

[**ExInitializeLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff545298)

从 Windows 2000 [ **PAGED\_后备链\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff558775)结构描述包含分页的缓冲区的后备链列表。 如果驱动程序提供自定义*分配*并*免费*例程有关此后备链列表，这些例程不会收到作为输入参数的专用上下文。 出于此原因，如果您的驱动程序旨在仅在 Windows Vista 和更高版本的 Windows 上运行，请考虑使用**后备链\_列表\_EX**结构，而不是**PAGED\_后备链\_列表**后备链列表的结构。 系统提供的以下例程支持后备链列表由描述**PAGED\_后备链\_列表**结构：

[**ExAllocateFromPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544393)

[**ExDeletePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544570)

[**ExFreeToPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544605)

[**ExInitializePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545309)

从 Windows 2000 [ **NPAGED\_后备链\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff556431)结构描述的旁路列表包含非分页的缓冲区。 如果驱动程序提供自定义*分配*并*免费*例程有关此后备链列表，这些例程不会收到作为输入参数的专用上下文。 同样，如果您的驱动程序旨在仅在 Windows Vista 和更高版本的 Windows 上运行，请考虑使用**后备链\_列表\_EX**结构，而不是**NPAGED\_后备链\_列表**后备链列表的结构。 系统提供的以下例程支持后备链列表由描述**NPAGED\_后备链\_列表**结构：

[**ExAllocateFromNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544388)

[**ExDeleteNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544566)

[**ExFreeToNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544601)

[**ExInitializeNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545301)

## <a name="implementation-guidelines"></a>实现准则


若要实现使用的后备链列表**后备链\_列表\_EX**结构，请遵循这些设计原则：

-   调用**ExInitializeLookasideListEx**设置后备链列表。 在此调用中，指定是否后备链列表中的条目都分页或非分页的缓冲区。 使用非分页的缓冲区，如果驱动程序本身或向其传递其后备链列表项的任何基础驱动程序可能会访问这些项在 IRQL &gt;= 调度\_级别。 使用分页的缓冲区，仅当对驱动程序的后备链列表项的访问始终出现在 IRQL &lt;= APC\_级别。

-   **后备链\_列表\_EX**结构后备链列表必须始终位于非分页的系统内存，而不考虑是否在列表中的条目都分页或非分页。

-   为了提高性能，传递**NULL**指针*分配*并*免费*参数**ExInitializeLookasideListEx**除非分配和解除分配例程必须执行多个只是分配并释放后备链列表项的内存。 例如，这些例程可记录驱动程序的使用情况信息的动态分配的缓冲区。

-   驱动程序提供*分配*例程可以传递输入的参数 (*PoolType*，*标记*，以及*大小*) 直接向接收[ **ExAllocatePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544520)或[ **ExAllocatePoolWithQuotaTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544513)例程来分配新缓冲区。

-   每次调用**ExAllocateFromLookasideListEx**，相互调用**ExFreeToLookasideListEx**越早越好每当先前分配的条目不再使用。

提供*分配*并*免费*不执行任何操作多个调用的例程[ **ExAllocatePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544520)和[ **ExFreePool**](https://msdn.microsoft.com/library/windows/hardware/ff544590)分别，浪费处理器时钟周期数。 **ExAllocateFromLookasideListEx**可以根据需要调用**ExAllocatePoolWithTag**并**ExFreePool**自动时驱动程序传递**NULL***分配*并*免费*指向**ExInitializeLookasideListEx**。

任何驱动程序提供*分配*例程必须分配内存的条目从页面缓冲池以将其保留在非分页后备链列表中，反之亦然。 它必须分配固定大小的条目，原因是，任何后续的驱动程序调用到**ExAllocateFromLookasideListEx**返回当前持有后备链列表中，除非该列表为空的第一个条目。 也就是说，调用**ExAllocateFromLookasideListEx**引起的驱动程序提供调用*分配*例程仅当给定的后备链列表是当前为空。 因此，在每次调用**ExAllocateFromLookasideListEx**，返回的条目将是正是该驱动程序必须仅当后备链列表中的所有条目的固定大小的大小。 驱动程序提供*分配*例程还应未更改*标记*值，该驱动程序最初传递给**ExInitializeLookasideListEx**，这是因为中的更改池标记值会使调试和跟踪驱动程序的内存使用情况更加困难。

调用**ExFreeToLookasideListEx**除非列表已存储的以前分配后备链列表中的条目*完整*（也就是说，列表包含的系统确定最大数目条目）。 为了提高性能，驱动程序应调用相互**ExFreeToLookasideListEx**快速它可以为它对每个调用**ExAllocateFromLookasideListEx**。 驱动程序释放回其后备链的条目时快速，列出该驱动程序的下一次**ExAllocateFromLookasideListEx**太有可能受到的动态分配一个新条目的内存的性能损失。

类似的准则适用于使用的后备链列表**PAGED\_后备链\_列表**或**NPAGED\_后备链\_列表**结构。

 

 




