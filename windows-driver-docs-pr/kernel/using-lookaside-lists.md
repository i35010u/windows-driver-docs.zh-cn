---
title: 使用后备列表
description: 使用后备列表
ms.assetid: 07a75b8b-04b9-48ea-bda4-53889dd661a9
keywords:
- 内存管理 WDK 内核，后备链表列表
- 后备链表列出 WDK 内核
- 固定大小的缓冲区分配 WDK 内核
- ExXxxLookasideList 例程 WDK
- 项 WDK 后备链表
- 非分页后备链表列出 WDK 内核
- 分页后备链表列出 WDK 内核
- 分配例程 WDK 内存
- 免费例程 WDK 内存
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3a8a5c99ec83cec3b0e31864c21672e894c326d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187161"
---
# <a name="using-lookaside-lists"></a>使用后备列表





必须动态分配固定大小的缓冲区以执行按需输入/输出操作的驱动程序才能使用 **Ex*xxx*LookasideListEx** 或 **ex*xxx*LookasideList** 支持例程。 此类驱动程序初始化其后备链表列表后，操作系统会在驱动程序的后备链表列表中保存一些给定大小的动态分配的缓冲区，从而有效地为驱动程序保留一组可重用的固定大小缓冲区。 驱动程序的固定大小缓冲区的格式和内容 (也称为其后备链表列表中) *条目* ，由驱动程序确定。

例如，必须为底层 SCSI 端口/微型端口驱动程序 (SRBs) 设置 SCSI 请求块的存储类驱动程序使用后备链表列表。 此类驱动程序根据需要从其后备链表列表中为 SRBs 分配缓冲区，并将每个 SRB 缓冲区释放到后备链表列表的后备链表列表，每次将 SRB 返回到已完成 IRP 中的类驱动程序时，都要重复使用。 由于存储类驱动程序无法预先确定该驱动程序的 i/o 需求增加并下降，因此它必须随时使用多少 SRBs，后备链表列表是一种便捷而经济的方式，用于管理此类驱动程序中固定大小的 SRBs 的缓冲区分配和解除分配。

操作系统维护当前正在使用的所有分页和非分页后备链表列表的状态，动态跟踪对所有列表中条目的分配和释放的需求，以及新条目的可用系统池。 当对分配的需求较高时，操作系统将增加每个后备链表列表中的条目数。 当需求再次下降时，它会将多余的后备链表项释放回系统池。

后备链表列表是线程安全的。 后备链表列表具有内置同步，使得驱动程序中的多个并发运行的线程可以共享后备链表列表。 这些线程可以安全地从共享后备链表列表分配缓冲区，并将这些缓冲区释放到列表，而无需驱动程序显式同步这些操作。 但是，为了避免可能的泄漏和数据损坏，共享后备链表列表的一组线程必须显式同步该列表的初始化和删除操作。

## <a name="lookaside-list-interfaces"></a>后备链表列表接口


从 Windows Vista 开始， [**后备链表 \_ 列表 \_ EX**](./eprocess.md) 结构描述了可包含分页或非分页缓冲的后备链表列表。 如果驱动程序为此后备链表列表提供自定义的 *分配* 和 *自由* 例程，则这些例程会接收专用上下文作为输入参数。 驱动程序可以使用此上下文来收集后备链表列表的专用数据。 例如，上下文可用于计算按列表动态分配和释放的列表项的数目。 有关演示如何以这种方式使用上下文的代码示例，请参阅 [**ExInitializeLookasideListEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializelookasidelistex)。

以下系统提供的例程支持 **后备链表 \_ 列表 \_ EX** 结构描述的后备链表列表：

[**ExAllocateFromLookasideListEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefromlookasidelistex)

[**ExDeleteLookasideListEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletelookasidelistex)

[**ExFlushLookasideListEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exflushlookasidelistex)

[**ExFreeToLookasideListEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetolookasidelistex)

[**ExInitializeLookasideListEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializelookasidelistex)

从 Windows 2000 开始， [**分页 \_ 后备链表 \_ 列表**](./eprocess.md) 结构描述了包含分页缓冲区的后备链表列表。 如果驱动程序为此后备链表列表提供自定义的 *分配* 和 *自由* 例程，则这些例程不会接收专用上下文作为输入参数。 出于此原因，如果你的驱动程序只能在 Windows Vista 和更高版本的 Windows 上运行，请考虑使用后备链表列表的 **后备链表 \_ 列表 \_ EX** 结构，而不是 **分页 \_ 后备链表 \_ 列表** 结构。 以下系统提供的例程支持通过 **分页 \_ 后备链表 \_ 列表** 结构描述的后备链表列表：

[**ExAllocateFromPagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefrompagedlookasidelist)

[**ExDeletePagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletepagedlookasidelist)

[**ExFreeToPagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetopagedlookasidelist)

[**ExInitializePagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializepagedlookasidelist)

从 Windows 2000 开始， [**NPAGED \_ 后备链表 \_ 列表**](./eprocess.md) 结构描述了包含非分页缓冲区的后备链表列表。 如果驱动程序为此后备链表列表提供自定义的 *分配* 和 *自由* 例程，则这些例程不会接收专用上下文作为输入参数。 同样，如果你的驱动程序只能在 Windows Vista 和更高版本的 Windows 上运行，请考虑使用 **后备链表 \_ 列表 \_ EX** 结构，而不是后备链表列表的 **NPAGED \_ 后备链表 \_ 列表** 结构。 以下系统提供的例程支持 **NPAGED \_ 后备链表 \_ 列表** 结构描述的后备链表列表：

[**ExAllocateFromNPagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefromnpagedlookasidelist)

[**ExDeleteNPagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletenpagedlookasidelist)

[**ExFreeToNPagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetonpagedlookasidelist)

[**ExInitializeNPagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializenpagedlookasidelist)

## <a name="implementation-guidelines"></a>实现准则


若要实现使用 **后备链表 \_ 列表 \_ EX** 结构的后备链表列表，请遵循以下设计准则：

-   调用 **ExInitializeLookasideListEx** 以设置后备链表列表。 在此调用中，指定后备链表列表中的条目是分页还是非分页缓冲。 如果驱动程序本身或它将其后备链表列表项传递到的任何基础驱动程序，则使用非分页缓冲区可能会以 IRQL &gt; = 调度级别访问这些项 \_ 。 仅当对驱动程序的后备链表列表项的访问始终以 IRQL = APC 级别进行访问时，才使用分页缓冲区 &lt; \_ 。

-   后备链表列表的 **后备链表 \_ 列表 \_ EX** 结构必须始终驻留在未分页的系统内存中，无论列表中的条目是分页还是未分页。

-   为了获得更好的性能，请将**NULL**指针传递给**ExInitializeLookasideListEx**的*分配*和*自由*参数，除非分配和释放例程必须对后备链表列表项仅分配和释放内存。 例如，这些例程可能会记录有关驱动程序使用动态分配的缓冲区的信息。

-   驱动程序提供的 *分配* 例程可以传递输入参数 (*PoolType*、 *Tag*和 *Size*) 它直接接收到 [**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) 或 [**ExAllocatePoolWithQuotaTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag) 例程以分配新的缓冲区。

-   对于每次调用 **ExAllocateFromLookasideListEx**，只要不再使用以前分配的条目，就应尽快对 **ExFreeToLookasideListEx** 进行倒数调用。

提供只需调用[**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)和[**ExFreePool**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)，而不会浪费处理器周期的*分配*和*自由*例程。 当驱动程序将**NULL** *分配*和*自由*指针传递到**ExInitializeLookasideListEx**时， **ExAllocateFromLookasideListEx**会自动进行对**ExAllocatePoolWithTag**和**ExFreePool**的必要调用。

任何驱动程序提供的 *分配* 例程都不得为分页池中的条目分配内存，以使其保留在非分页的后备链表列表中，反之亦然。 它还必须分配固定大小的条目，因为对 **ExAllocateFromLookasideListEx** 的任何后续驱动程序调用都将返回当前保存在后备链表列表中的第一个条目，除非该列表为空。 也就是说，仅当给定的后备链表列表当前为空时，对 **ExAllocateFromLookasideListEx** 的调用才会引发对驱动程序提供的 *分配* 例程的调用。 因此，在每次调用 **ExAllocateFromLookasideListEx**时，返回的项将是仅当后备链表列表中的所有项都为固定大小时才需要驱动程序所需的大小。 驱动程序提供的*分配*例程还应不会更改驱动程序最初传递给**ExInitializeLookasideListEx**的*标记*值，因为池标记值中的更改会导致调试和跟踪驱动程序的内存使用量。

调用 **ExFreeToLookasideListEx** 在后备链表列表中存储以前分配的条目，除非该列表已 *满* (即，此列表包含系统确定的最大条目数) 。 为了获得更好的性能，驱动程序应尽快对 **ExFreeToLookasideListEx** 进行的调用，使其对 **ExAllocateFromLookasideListEx**的每次调用都能正常进行。 当驱动程序快速将条目释放回其后备链表列表时，该驱动程序对 **ExAllocateFromLookasideListEx** 的下一次调用将不太可能导致为新条目动态分配内存的性能损失。

类似指导原则适用于使用 **分页 \_ 后备链表 \_ 列表** 或 **NPAGED \_ 后备链表 \_ 列表** 结构的后备链表列表。

 

