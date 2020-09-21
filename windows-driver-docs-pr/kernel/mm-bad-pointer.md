---
title: Windows 内核宏
description: Windows 内核宏
ms.assetid: 91366400-3307-4F13-A839-50BA85B7F73E
ms.localizationpriority: High
ms.date: 10/17/2018
ms.openlocfilehash: 1d8f2f6ce9bd4d0cbaa045fb47170998ead9503a
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717478"
---
# <a name="windows-kernel-macros"></a>Windows 内核宏


下面的列表包含 Windows 内核宏：


## <a name="address_and_size_to_span_pages"></a>**ADDRESS_AND_SIZE_TO_SPAN_PAGES**

定义位置：Wdm.h

**ADDRESS_AND_SIZE_TO_SPAN_PAGES** 宏返回按虚拟地址以及传输请求的大小（以字节为单位）定义的虚拟范围所跨越的页面数。

_Va [in]_

**PVOID**

指向作为范围基础的虚拟地址的指针。

_Size [in]_

**ULONG**

指定传输请求的大小（以字节为单位）。

**返回值**

**ULONG**

**ADDRESS_AND_SIZE_TO_SPAN_PAGES** 返回虚拟范围所跨越的页面数，从 _Va_ 开始。

使 DMA 传输调用 **ADDRESS_AND_SIZE_TO_SPAN_PAGES** 以确定是否必须将传输请求拆分为设备 DMA 操作序列的驱动程序。

驱动程序可以使用系统定义的常量 PAGE_SIZE 来确定要传输的字节数是否小于当前平台的虚拟内存页面大小。

**ADDRESS_AND_SIZE_TO_SPAN_PAGES** 的调用方可在任何 IRQL 上运行。 调用方必须确保指定的参数不会导致内存溢出。

从 Windows 2000 开始可用。


## <a name="byte_offset"></a>**BYTE_OFFSET**

定义位置：Wdm.h

**BYTE_OFFSET** 宏获取虚拟地址，并返回该地址在页面中的字节偏移量。

_Va [in]_

**PVOID**

指向虚拟地址的指针。

**返回值**

**ULONG**

**BYTE_OFFSET** 返回虚拟地址的偏移部分。

从 Windows 2000 开始可用。

IRQL：任何级别


## <a name="bytes_to_pages"></a>**BYTES_TO_PAGES**

定义位置：Wdm.h

**BYTES_TO_PAGES** 宏获取传输请求的大小（以字节为单位），并计算包含这些字节所需的页面数。

_Size [in]_

**ULONG**

指定传输请求的大小（以字节为单位）。

**返回值**

**ULONG**

**BYTES_TO_PAGES** 返回包含指定字节数所需的页面数。

可以使用系统定义的常量 PAGE_SIZE 来确定传输的给定长度（以字节为单位）是否小于当前平台的虚拟内存页面大小。

从 Windows 2000 开始可用。

IRQL：任何级别


## <a name="containing_record"></a>**CONTAINING_RECORD**

定义位置：Ntdef.h

**CONTAINING_RECORD** 宏返回某个结构的某个实例的基址，并提供该结构的类型，以及某个字段在包含结构中的地址。

_Address [in]_

**PCHAR**

一个指针，指向 _Type_ 类型的结构的实例中的字段。

_Type [in]_

**TYPE**

要返回其基址的结构的类型名称。

_Field [in]_

**PCHAR**

_Address_ 指向的、包含在 _Type_ 类型的结构中的字段的名称。

**返回值**

**PCHAR**

返回包含 _Field_ 的结构的基址。

调用该宏可以确定当调用方具有指向此类结构中的字段的指针时，其类型已知的结构的基址。 此宏可用于以符号方式访问已知类型的结构中的其他字段。

从 Windows 2000 开始可用。

IRQL：任何级别


## <a name="ioskipcurrentirpstacklocation"></a>**IoSkipCurrentIrpStackLocation**

定义位置：Wdm.h

\n**IoSkipCurrentIrpStackLocation** 宏修改系统的 [**IO_STACK_LOCATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location) 数组指针，以便在当前驱动程序调用下一个较低级别的驱动程序时，被调用的驱动程序会收到当前驱动程序所收到的相同 **IO_STACK_LOCATION** 结构。

_Irp [in, out]_

**PIRP**

指向 IRP 的指针。

**返回值**

**VOID**

当你的驱动程序向下一个较低级别的驱动程序发送 IRP 时，如果你不打算提供 [_IoCompletion_](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程（存储在驱动程序的 [**IO_STACK_LOCATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location) 结构中的地址），则你的驱动程序可以调用 **IoSkipCurrentIrpStackLocation**。 如果在调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 之前先调用 **IoSkipCurrentIrpStackLocation**，则下一个较低级别的驱动程序会收到你的驱动程序所收到的相同 **IO_STACK_LOCATION**。

如果你打算为 IRP 提供 _IoCompletion_ 例程，则你的驱动程序应调用 [**IoCopyCurrentIrpStackLocationToNext**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) 而不是 **IoSkipCurrentIrpStackLocation**。 如果错误编写的驱动程序在调用 **IoSkipCurrentIrpStackLocation** 时出错，然后设置完成例程，则此驱动程序可能会覆盖其下级驱动程序设置的完成例程。

如果该驱动程序挂起了某个 IRP，则该驱动程序在将该 IRP 传递给下一个较低级别的驱动程序之前，不应调用 **IoSkipCurrentIrpStackLocation**。 如果该驱动程序在将挂起的 IRP 传递给下一个较低级别的驱动程序之前对该 IRP 调用 **IoSkipCurrentIrpStackLocation**，仍会在下一个驱动程序的 I/O 堆栈位置的 **Control** 成员中设置 SL_PENDING_RETURNED 标志。 由于下一个驱动程序拥有该堆栈位置并可对其进行修改，因此它可能会清除挂起标志。 这种情况可能导致操作系统发出 bug 检查，或者 IRP 处理永远无法完成。

挂起 IRP 的驱动程序应在调用 **IoCallDriver** 之前先调用 **IoCopyCurrentIrpStackLocationToNext**，以便为下一个较低级别的驱动程序设置新的堆栈位置。

如果驱动程序调用 **IoSkipCurrentIrpStackLocation**，请注意修改 **IO_STACK_LOCATION** 结构的方式不能无意中影响较低级别的驱动程序，或运行该驱动器时的系统行为。 示例包括修改 **IO_STACK_LOCATION** 结构的 **Parameters** 并集或调用 [**IoMarkIrpPending**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)。

从 Windows 2000 开始可用。

IRQL：任何级别


## <a name="keinitializecallbackrecord"></a>**KeInitializeCallbackRecord**

定义位置：Wdm.h

**KeInitializeCallbackRecord** 宏初始化 [**KBUGCHECK_CALLBACK_RECORD**](./eprocess.md) 或 [**KBUGCHECK_REASON_CALLBACK_RECORD**](./eprocess.md) 结构。

_CallbackRecord [in]_

**PKBUGCHECK_CALLBACK_RECORD**

指向 **KBUGCHECK_CALLBACK_RECORD** 或 **KBUGCHECK_REASON_CALLBACK_RECORD** 结构的指针。 该结构必须位于常驻内存（例如非分页池）中。

**返回值**

**VOID**

在 Windows 2000 和更高版本的 Windows 中可用。

IRQL：任何级别


## <a name="mm_bad_pointer"></a>**MM_BAD_POINTER**

定义位置：Wdm.h

驱动程序可以使用 **MM_BAD_POINTER** 宏作为要分配给未初始化或不再有效的指针变量的错误指针值。 尝试访问此无效指针变量指向的内存位置将导致 bug 检查。

在许多硬件平台上，地址 0（往往表示为命名常量 **NULL**）是无效地址，但驱动程序开发人员不应假设地址 0 在所有平台中均无效。 将未初始化或无效的指针变量设置为地址 0 不一定总能保证可以检测到通过这些指针进行的不当访问。

相反，可以保证 **MM_BAD_POINTER** 值是运行驱动程序的每个平台上的无效地址。

在地址 0 是无效地址的平台上，在 < DISPATCH_LEVEL 的 IRQL 上访问地址 0 的驱动程序会导致异常（访问冲突），而 `try/except` 语句可能会无意中捕获到该异常。 因此，驱动程序的异常处理代码可能会屏蔽无效访问，并在调试过程中阻止检测这种访问。 但是，可以保证对 **MM_BAD_POINTER** 地址的访问会导致 bug 检查，异常处理程序无法对此进行屏蔽。

下面的代码示例演示如何将 **MM_BAD_POINTER** 值分配给名为 `ptr` 的指针变量。 Ntdef.h 标头文件将 PUCHAR 类型定义为指向 `unsigned char` 的指针。

`PUCHAR ptr = (PUCHAR)MM_BAD_POINTER; // Now _ptr is guaranteed to fault._`

将 `ptr` 设置为 **MM_BAD_POINTER** 后，尝试访问 `ptr` 指向的内存位置会导致 bug 检查。

事实上，**MM_BAD_POINTER** 是无效地址的整个页面的基址。 因此，对 **MM_BAD_POINTER** 至 (**MM_BAD_POINTER** + **PAGE_SIZE** - 1) 范围内的地址进行任何访问都会导致 bug 检查。

从 Windows 8.1 开始，**MM_BAD_POINTER** 宏在 Wdm.h 标头文件中定义。 但是，使用此宏定义的驱动程序代码可以在 Windows Vista 及更低版本的 Windows 中运行。

从 Windows Vista 开始，[**MmBadPointer**](./mm64bitphysicaladdress.md) 全局变量可用作指向某个指针值（保证为无效地址）的指针。 但是，从 Windows 8.1 开始，**MmBadPointer** 已弃用；应将驱动程序更新为改用 **MM_BAD_POINTER** 宏。

从 Windows 8.1 开始可用。 与 Windows Vista 及更低版本的 Windows 兼容。


## <a name="mmgetmdlbytecount"></a>**MmGetMdlByteCount**

定义位置：Wdm.h

**MmGetMdlByteCount** 宏返回指定 MDL 描述的缓冲区的长度（以字节为单位）。

_Mdl [in]_

**PMDL**

指向 [**MDL**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl) 结构的指针，该结构描述物理内存中虚拟内存缓冲区的布局。 有关详细信息，请参阅[使用 MDL](using-mdls.md)。

**返回值**

**ULONG**

**MmGetMdlByteCount** 返回 _Mdl_ 描述的缓冲区的长度（以字节为单位）。

**MmGetMdlByteCount** 的调用方可在任何 IRQL 上运行。 通常，调用方在 <= DISPATCH_LEVEL 的 IRQL 上运行。

从 Windows 2000 开始可用。

IRQL：任何级别


## <a name="mmgetmdlbyteoffset"></a>**MmGetMdlByteOffset**

定义位置：Wdm.h

**MmGetMdlByteOffset** 宏返回给定 MDL 描述的缓冲区的初始页面中的字节偏移量。

_Mdl [in]_

**PMDL**

指向 MDL 的指针。

**返回值**

**ULONG**

**MmGetMdlByteOffset** 返回偏移量（以字节为单位）。

**MmGetMdlByteOffset** 的调用方可在任何 IRQL 上运行。 通常，调用方在 <= DISPATCH_LEVEL 的 IRQL 上运行。

在 Windows 2000 和更高版本的 Windows 中可用。

IRQL：任何级别


## <a name="mmgetmdlpfnarray"></a>**MmGetMdlPfnArray**

定义位置：Wdm.h

**MmGetMdlPfnArray** 宏返回指向与内存描述符列表 (MDL) 关联的物理页面编号数组开头位置的指针。

_Mdl [in]_

**PMDL**

指向 MDL 的指针。

**返回值**

**PPFN_NUMBER**

指向与 MDL 关联的物理页面编号数组开头位置的指针。 数组中的项数为 **ADDRESS_AND_SIZE_TO_SPAN_PAGES**(**MmGetMdlVirtualAddress**(_Mdl_), **MmGetMdlByteCount**(_Mdl_))。 每个数组元素是 PFN_NUMBER 类型的整数值，其定义位置为：Wdm.h，如下所示：

`cpp typedef ULONG PFN_NUMBER, *PPFN_NUMBER;`

**注意**：更改该数组的内容可能会导致难以诊断的微妙系统问题。 建议不要读取或更改此数组的内容。

对于可分页内存，该数组的内容仅对使用 [**MmProbeAndLockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages) 锁定的缓冲区有效。 对于非分页池，该数组的内容仅对使用 [**MmBuildMdlForNonPagedPool**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool)、[**MmAllocatePagesForMdlEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdlex) 或 [**MmAllocatePagesForMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdl) 更新的 MDL 有效。

有关 MDL 的详细信息，请参阅[使用 MDL](using-mdls.md)。

从 Windows 2000 开始可用。

IRQL：任何级别


## <a name="mmgetmdlvirtualaddress"></a>**MmGetMdlVirtualAddress**

定义位置：Wdm.h

**MmGetMdlVirtualAddress** 宏返回 MDL 描述的缓冲区的基本虚拟地址。

_Mdl [in]_

**PMDL**

指向 MDL 的指针，该 MDL 描述要返回其初始虚拟地址的缓冲区。

**返回值**

**PVOID**

**MmGetMdlVirtualAddress** 返回 MDL 的起始虚拟地址。

**MmGetMdlVirtualAddress** 返回在当前线程上下文中不一定有效的虚拟地址。 较低级别的驱动程序不应尝试使用返回的虚拟地址来访问内存，尤其是在用户内存空间中。

可将用作 MDL 中物理地址项的索引的返回地址输入到 [**MapTransfer**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer) 中。

**MmGetMdlVirtualAddress** 的调用方可在任何 IRQL 上运行。 通常，调用方在 = DISPATCH_LEVEL 的 IRQL 上运行，因为通常会调用此例程来获取 **MapTransfer**的 _CurrentVa_ 参数。

在 Windows 2000 和更高版本的 Windows 中可用。

IRQL：任何级别


## <a name="mmgetsystemaddressformdlsafe"></a>**MmGetSystemAddressForMdlSafe**

定义位置：Wdm.h

**MmGetSystemAddressForMdlSafe** 宏返回指定 MDL 描述的缓冲区的非分页系统空间虚拟地址。

_Mdl [in]_

**PMDL**

指向要映射其对应基本虚拟地址的缓冲区的指针。

_Priority [in]_

**MM_PAGE_PRIORITY**

指定一个 **MM_PAGE_PRIORITY** 值，用于指示在可用 PTE 不足的情况下成功的重要性。 指定优先级值 **LowPagePriority**、**NormalPagePriority** 或 **HighPagePriority**。 从 Windows 8 开始，指定的优先级值可以结合 **MdlMappingNoWrite** 或 **MdlMappingNoExecute** 标志进行按位 OR 运算。

*   **LowPagePriority** 表示当系统的资源相当少时，映射请求可以失败。 这种情况的一个例子是网络连接并不关键，驱动程序可以处理映射失败问题。

*   **NormalPagePriority** 表示当系统的资源非常少时，映射请求可以失败。 这种情况的一个例子是本地文件系统请求并不关键。

*   **HighPagePriority** 表示除非系统完全耗尽资源，否则映射请求不得失败。 这种情况的一个例子是驱动程序中的分页文件路径。

*   **MdlMappingNoWrite** 表示要将映射的物理页面配置为不可写（只读）内存。 从 Windows 8 开始，此标志位可以结合 **MM_PAGE_PRIORITY** 值进行按位 OR 运算，以指定要在其中禁用写入的内存。

*   **MdlMappingNoExecute** 表示要将映射的物理页面配置为不可执行内存。 从 Windows 8 开始，此标志位可以结合 **MM_PAGE_PRIORITY** 值进行按位 OR 运算，以指定要在其中禁用指令执行的内存。 最佳做法是，除非明确需要可执行内存，否则，为 Windows 8 和更高版本的 Windows 编写的驱动程序应始终指定不可执行内存。

*   **返回值**

    **PVOID**

    **MmGetSystemAddressForMdlSafe** 返回用于映射指定 MDL 描述的物理页面的基本系统空间虚拟地址。 如果页面尚未映射到系统地址空间，并且尝试映射这些页面失败，则会返回 **NULL**。

如果指定 MDL 描述的物理页面尚未映射到系统地址空间，此例程会将这些页面映射到系统地址空间。

编程 I/O (PIO) 设备的驱动程序调用此例程将位于 **Irp->MdlAddress** 的 MDL 描述的、已映射到用户模式虚拟地址范围的用户模式缓冲区映射到系统地址空间中的某个范围。

进入此例程后，指定的 MDL 必须描述已锁定的物理页面。 可以使用 [**MmProbeAndLockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)、[**MmBuildMdlForNonPagedPool**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool)、[**IoBuildPartialMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl) 或 [**MmAllocatePagesForMdlEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdlex) 例程生成锁定的 MDL。

不再需要 **MmGetSystemAddressForMdlSafe** 返回的系统地址空间映射时，必须将其释放。 释放映射所要执行的步骤取决于 MDL 的生成方式。 下面是四种可能的情况：

*   如果 MDL 是通过调用 **MmProbeAndLockPages** 例程生成的，则无需显式释放系统地址空间映射。 可以调用 [**MmUnlockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages) 例程来释放映射（如果已分配）。

*   如果 MDL 是通过调用 **MmBuildMdlForNonPagedPool** 例程生成的，则 **MmGetSystemAddressForMdlSafe** 会重复使用现有的系统地址空间映射，而不是创建新的映射。 在这种情况下，无需进行清理（即，无需解除锁定和取消映射）。

*   如果 MDL 是通过调用 **IoBuildPartialMdl** 例程生成的，则驱动程序必须调用 [**MmPrepareMdlForReuse**]() 例程或 [**IoFreeMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreemdl) 例程来释放系统地址空间映射。

*   如果 MDL 是通过调用 **MmAllocatePagesForMdlEx** 例程生成的，则驱动程序必须调用 **MmUnmapLockedPages** 例程来释放系统地址空间映射。 如果对 MDL 多次调用 **MmGetSystemAddressForMdlSafe**，后续的 **MmGetSystemAddressForMdlSafe** 调用只会返回第一次调用所创建的映射。 调用 **MmUnmapLockedPages** 一次就足以释放此映射。

从 Windows 7 和 Windows Server 2008 R2 开始，不必要对 **MmAllocatePagesForMdlEx** 创建的 MDL 显式调用 **MmUnmapLockedPages**。 调用 [**MmFreePagesFromMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreepagesfrommdl) 例程可以释放系统地址空间映射（如果已分配）。

若要创建新的系统地址空间映射，**MmGetSystemAddressForMdlSafe** 将结合设置为 **MmCached** 的 _CacheType_ 参数调用 **MmMapLockedPagesSpecifyCache**。 需要除 **MmCached** 以外的缓存类型的驱动程序应直接调用 **MmMapLockedPagesSpecifyCache**，而不是调用 **MmGetSystemAddressForMdlSafe**。 有关 _CacheType_ 参数的详细信息，请参阅 [**MmMapLockedPagesSpecifyCache**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache)。

在 **MmMapLockedPagesSpecifyCache** 的调用中，仅当 MDL 描述的页面尚无关联的缓存类型时，才使用指定的缓存类型。 不过，几乎在所有情况下，页面都已有关联的缓存类型，并且此缓存类型已由新的映射使用。 **MmAllocatePagesForMdl** 分配的页面不适用此规则：无论页面的原始缓存类型是什么，该例程都会将缓存类型设置为 **MmCached**。

每次只有一个线程可以安全地对特定的 MDL 调用 **MmGetSystemAddressForMdlSafe**，因为此例程假设调用方线程拥有该 MDL。 但是，可对同一 MDL 多次调用 **MmGetSystemAddressForMdlSafe**，调用方法是：从同一线程发出所有调用；如果从多个线程发出调用，可以显式同步调用。

如果驱动程序必须将请求拆分成较小的请求，该驱动程序可以分配更多的 MDL，或者使用 **IoBuildPartialMdl** 例程。

返回的基址的偏移量与 MDL 中的虚拟地址相同。

Windows 98 不支持 **MmGetSystemAddressForMdlSafe**。 请改用 [**MmGetSystemAddressForMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmgetsystemaddressformdl)。

由于此宏调用 [**MmMapLockedPagesSpecifyCache**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache)，因此使用它可能需要链接到 NtosKrnl.lib。

从 Windows 2000 开始可用。

IRQL <= DISPATCH_LEVEL


## <a name="mminitializemdl"></a>**MmInitializeMdl**

定义位置：Wdm.h

**MmInitializeMdl** 宏初始化 MDL 的标头。

_MemoryDescriptorList [in]_

**PMDL**

指向初始化为 MDL 的缓冲区的指针。 有关详细信息，请参阅以下部分。

_BaseVa [in]_

**PVOID**

指向缓冲区的基本虚拟地址的指针。

_Length [in]_

**SIZE_T**

指定 MDL 描述的缓冲区的长度（以字节为单位）。 此例程支持 MAXULONG 字节的最大缓冲区长度。

**返回值**

**VOID**

必须在非分页内存中分配 _MemoryDescriptorList_ 指向的缓冲区。 此缓冲区的大小（以字节为单位）必须至少为 **sizeof**(MDL) + **sizeof**(PFN_NUMBER) * **ADDRESS_AND_SIZE_TO_SPAN_PAGES**(_BaseVa_, _Length_)。

在 Windows 2000 和更高版本的 Windows 中可用。

IRQL <= DISPATCH_LEVEL


## <a name="mmpreparemdlforreuse"></a>**MmPrepareMdlForReuse**

定义位置：Wdm.h

**MmPrepareMdlForReuse** 宏释放与部分 MDL 关联的资源，以便可以重复使用该 MDL。

_Mdl [in]_

**PMDL**

指向准备供重复使用的部分 MDL 的指针。

**返回值**

**VOID**

对 [**IoBuildPartialMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl) 例程调用中的 _TargetMdl_ 参数重复使用同一分配 MDL 的驱动程序使用此宏。 如果在 **MmPrepareMdlForReuse** 调用中，指定的部分 MDL 具有与系统地址空间之间的关联映射，则 **MmPrepareMdlForReuse** 将释放该映射，以便可以重复使用该 MDL。

**MmPrepareMdlForReuse** 仅接受 **IoBuildPartialMdl** 生成的部分 MDL。 如果 **MmPrepareMdlForReuse** 收到一个已映射到系统地址空间但并非由 **IoBuildPartialMdl** 生成的 MDL，则 **MmPrepareMdlForReuse** 不会释放该映射。

有关部分 MDL 的详细信息，请参阅[使用 MDL](using-mdls.md)。

在 Windows 2000 和更高版本的 Windows 中可用。

IRQL <= DISPATCH_LEVEL


## <a name="page_align"></a>**PAGE_ALIGN**

定义位置：Wdm.h

**PAGE_ALIGN** 宏返回给定虚拟地址的页面对齐虚拟地址。

_Va [in]_

**PVOID**

指向虚拟地址的指针。

**返回值**

**PVOID**

**PAGE_ALIGN** 返回指向页面对齐虚拟地址的指针。

从 Windows 2000 开始可用。

IRQL：任何级别


## <a name="paged_code"></a>**PAGED_CODE**

定义位置：Wdm.h

**PAGED_CODE** 宏确保调用方线程在足够低的允许分页的 IRQL 上运行。

**返回值**

**VOID**

如果 IRQL > APC_LEVEL，则 **PAGED_CODE** 宏会导致系统 ASSERT。

应在包含可分页代码或访问可分页代码的每个驱动程序例程的开头位置调用此宏。

**PAGED_CODE** 宏仅检查位于驱动程序代码执行宏的位置的 IRQL。 如果该代码随后引发 IRQL，该宏将不会检测此更改。 驱动程序开发人员应使用[静态驱动程序验证程序](../devtest/static-driver-verifier.md)和[驱动程序验证程序](../devtest/driver-verifier.md)来检测执行驱动程序例程期间错误引发 IRQL 的时间。

**PAGED_CODE** 宏仅在已检查的生成中工作。

从 Windows 2000 开始可用。


## <a name="paged_code_locked"></a>**PAGED_CODE_LOCKED**

定义位置：Wdm.h

**PAGED_CODE_LOCKED** 宏断言当前正在运行的代码节可分页，在运行之前必须已锁定到内存中。

**返回值**

**VOID**

可分页代码必须遵守某些限制（例如 IRQL <= APC_LEVEL），除非锁定就位。 必须锁定就位才能正常工作的可分页例程首先应该调用 **PAGED_CODE_LOCKED**。

有关将代码节锁定就位的详细信息，请参阅[锁定可分页代码或数据](locking-pageable-code-or-data.md)。


## <a name="posetdevicebusy"></a>**PoSetDeviceBusy**

定义位置：Wdm.h

**PoSetDeviceBusy** 宏向[电源管理器](power-manager.md)告知与 _IdlePointer_ 关联的设备繁忙。

_IdlePointer [in, out]_

**PULONG**

指定 [**PoRegisterDeviceForIdleDetection**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregisterdeviceforidledetection) 先前返回的非 **NULL** 空闲指针。 请注意，**PoRegisterDeviceForIdleDetection** 可能返回 **NULL** 指针。 **PoSetDeviceBusy** 的调用方必须在将指针传递给 **PoSetDeviceBusy** 之前验证该指针是否非 **NULL**。

**返回值**

**VOID**

**注意**：[**PoSetDeviceBusyEx**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetdevicebusyex) 例程可直接取代 **PoSetDeviceBusy** 宏。 如果你正在为 Windows Vista Service Pack 1 (SP1) 和更高版本的 Windows 编写新驱动程序代码，请调用 **PoSetDeviceBusyEx**，而不要调用 **PoSetDeviceBusy**。

驱动程序结合使用 **PoSetDeviceBusy** 和 **PoRegisterDeviceForIdleDetection** 为其设备启用系统空闲检测。 如果注册了空闲检测的设备处于空闲状态，电源管理器将发送 [**IRP_MN_SET_POWER**](./irp-mn-set-power.md) 请求，使设备进入请求的睡眠状态。

**PoSetDeviceBusy** 报告设备处于繁忙状态，使电源管理器能够重启其空闲倒计时。 如果设备未开机，**PoSetDeviceBusy** 不会更改其状态。 也就是说，它不会导致系统发送开机请求。

驱动程序应该对每个 I/O 请求调用 **PoSetDeviceBusy**。

从 Windows 2000 开始可用。

IRQL：任何级别


## <a name="psgetcurrentprocess"></a>**PsGetCurrentProcess**

定义位置：Ntddk.h

返回指向当前线程的进程的指针。

**返回值**

**PEPROCESS**

指向不透明进程对象的指针。



从 Windows 2000 开始可用。

IRQL：任何级别


## <a name="read_register_buffer_ulong64"></a>**READ_REGISTER_BUFFER_ULONG64**

定义位置：Wdm.h

**READ_REGISTER_BUFFER_ULONG64** 宏将指定寄存器地址中的多个 ULONG64 值读入缓冲区。

_Register [in]_

**PULONG64**

指向寄存器的指针，该寄存器必须是内存空间中的已映射范围。

_Buffer [out]_

**PULONG64**

指向 ULONG64 值数组已读入到的缓冲区的指针。

_Count [in]_

**ULONG**

指定要读入到缓冲区中的 ULONG64 值的数量。

**返回值**

**VOID**

_Buffer_ 缓冲区的大小必须足够大，至少可包含指定数量的 ULONG64 值。

**READ_REGISTER_BUFFER_ULONG64** 宏的调用方可在任何 IRQL 上运行，前提是 _Buffer_ 缓冲区是常驻的，并且 _Register_ 寄存器是常驻的已映射设备内存。

仅在 64 位版本的 Windows 中可用。

IRQL：任何级别


## <a name="read_register_ulong64"></a>**READ_REGISTER_ULONG64**

定义位置：Wdm.h

**READ_REGISTER_ULONG64** 宏从指定的寄存器地址读取 ULONG64 值。

_volatile *Register [in]_

**ULONG64**

指向寄存器地址的指针，该地址必须是内存空间中的已映射范围。

**返回值**

**ULONG64**

**READ_REGISTER_ULONG64** 返回从指定寄存器地址读取的 ULONG64 值。

**READ_REGISTER_ULONG64** 宏的调用方可在任何 IRQL 上运行，前提是 _Register_ 地址是常驻的已映射设备内存。

仅在 64 位版本的 Windows 中可用。

IRQL：任何级别


## <a name="round_to_pages"></a>**ROUND_TO_PAGES**

定义位置：Wdm.h

**ROUND_TO_PAGES** 宏获取以字节为单位的大小，并将其向上舍入为下一个完整页面。

_Size [in]_

**ULONG_PTR**

指定要向上舍入为页面倍数的大小（以字节为单位）。

**返回值**

**ULONG_PTR**

**ROUND_TO_PAGES** 返回已向上舍入为当前平台的虚拟内存页面大小倍数的输入大小。

**ROUND_TO_PAGES** 的调用方可在任何 IRQL 上运行。 调用方必须确保提供的参数不会导致内存溢出。

IRQL：任何级别


## <a name="rtlequalluid"></a>**RtlEqualLuid**

定义位置：Wdm.h

**返回值**

从 Windows 2000 开始可用。

IRQL：任何级别


## <a name="rtlinitemptyansistring"></a>**RtlInitEmptyAnsiString**

定义位置：Wdm.h

**RtlInitEmptyAnsiString** 宏初始化一个空的计数 ANSI 字符串。

_DestinationString [out]_

**PANSI_STRING**

指向要初始化的 [**ANSI_STRING**](/windows/win32/api/ntdef/ns-ntdef-_string) 结构的指针。

_Buffer [in]_

**PCHAR**

指向调用方分配的、用于包含 WCHAR 字符串的缓冲区的指针。

_BufferSize [in]_

**USHORT**

_Buffer_ 指向的缓冲区的长度（以字节为单位）。

**返回值**

**VOID**

_DestinationString_ 参数指向的结构的成员按如下所示进行初始化。

*   **Length**. Zero。

*   **MaximumLength**. _BufferSize_。

*   **Buffer**. _SourceString_。

若要初始化非空计数 Unicode 字符串，请调用 [**RtlInitAnsiString**](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlinitansistring)。

在 Microsoft Windows XP 和更高版本的 Windows 中可用。

IRQL：任何级别


## <a name="rtlinitemptyunicodestring"></a>**RtlInitEmptyUnicodeString**

定义位置：Wdm.h

**RtlInitEmptyUnicodeString** 宏初始化一个空的计数 Unicode 字符串。

_DestinationString [out]_

**PUNICODE_STRING**

指向要初始化的 [**UNICODE_STRING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string) 结构的指针。

_Buffer [in]_

**PWCHAR**

指向调用方分配的、用于包含 WCHAR 字符串的缓冲区的指针。

_BufferSize [in]_

**USHORT**

_Buffer_ 指向的缓冲区的长度（以字节为单位）。

**返回值**

**VOID**

_DestinationString_ 参数指向的结构的成员按如下所示进行初始化。

*   **Length**. Zero。

*   **MaximumLength**. _BufferSize_。

*   **Buffer**. _SourceString_。

若要初始化非空计数 Unicode 字符串，请调用 [**RtlInitUnicodeString**](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlinitunicodestring)。

从 Windows XP 开始可用。

IRQL：任何级别


## <a name="rtliszeroluid"></a>**RtlIsZeroLuid**

定义位置：Ntddk.h

**RtlIsZeroLuid** 宏确定指定的 LUID 是否为零 LUID。

_L1 [in]_

**PLUID**

指定要检查的 [**LUID**](/windows/win32/api/ntdef/ns-ntdef-_luid)。

**返回值**

**BOOLEAN**

如果 _L1_ 为零，则 **RtlIsZeroLuid** 返回 **TRUE**，否则返回 **FALSE**。

IRQL：任何级别


## <a name="rtlretrieveulong"></a>**RtlRetrieveUlong**

定义位置：Wdm.h

**RtlRetrieveUlong** 宏从源地址检索 ULONG 值，可避免对齐错误。 假设目标地址已对齐。

_DestinationAddress [out]_

**PULONG**

指向要在其中存储 ULONG 值的 ULONG 对齐位置的指针。

_SourceAddress [in]_

**PULONG**

指向要从中检索 ULONG 值的位置的指针。

**返回值**

**VOID**

如果给定的地址位于非分页池中，则 **RtlRetrieveUlong** 的调用方可在任何 IRQL 上运行。 否则，调用方必须在 <= APC_LEVEL 的 IRQL 上运行。

在 Windows 2000 和更高版本的 Windows 中可用。


## <a name="rtlretrieveushort"></a>**RtlRetrieveUshort**

定义位置：Wdm.h

**RtlRetrieveUshort** 宏从源地址检索 USHORT 值，可避免对齐错误。

_DestinationAddress [out]_

**PUSHORT**

指向要在其中存储值的 USHORT 对齐位置的指针。

_SourceAddress [in]_

**PUSHORT**

指向要从中检索值的位置的指针。

**返回值**

**VOID**

如果给定的地址位于非分页池中，则 **RtlRetrieveUshort** 的调用方可在任何 IRQL 上运行。 否则，调用方必须在 <= APC_LEVEL 的 IRQL 上运行。

在 Windows 2000 和更高版本的 Windows 中可用。

IRQL：任何级别


## <a name="rtlstoreulong"></a>**RtlStoreUlong**

定义位置：Wdm.h

**RtlStoreUlong** 宏在特定的地址中存储 ULONG 值，可避免对齐错误。

_Address [out]_

**PULONG**

指向要在其中存储指定 ULONG 值的位置的指针。

_Value [in]_

**ULONG**

指定要存储的 ULONG 值。

**返回值**

**VOID**

如果 _Address_ 指向非分页池，则调用方可在任何 IRQL 上运行。 否则，调用方必须在 <= APC_LEVEL 的 IRQL 上运行。

在 Windows 2000 和更高版本的 Windows 中可用。

IRQL：任何级别


## <a name="rtlstoreulonglong"></a>**RtlStoreUlonglong**

定义位置：Wdm.h

**RtlStoreUlonglong** 宏在指定的内存地址中存储指定的 ULONGLONG 值，可避免内存对齐错误。

_Address [out]_

**PULONGLONG**

指向要在其中存储指定 ULONGLONG 值的位置的指针。

_Value [in]_

**ULONGLONG**

要存储的 ULONGLONG 值。

**返回值**

**VOID**

**RtlStoreUlonglong** 可避免内存对齐错误。 如果 _Address_ 指定的地址不符合 ULONGLONG 的存储要求，**RtlStoreUlonglong** 将在内存位置 (PUCHAR)_Address_ 的开头位置存储 _Value_ 的字节。

如果 _Address_ 指向非分页池，则 **RtlStoreUlonglong** 可在任何 IRQL 上运行；否则，它必须在 <= APC_LEVEL 的 IRQL 上运行。

从 Windows 2000 开始可用。

IRQL：任何级别


## <a name="rtlstoreulongptr"></a>**RtlStoreUlongPtr**

定义位置：Wdm.h

**RtlStoreUlongPtr** 宏在指定的内存位置存储指定的 ULONG_PTR 值，可避免内存对齐错误。

_Address [out]_

**PULONG_PTR**

指向要在其中存储 ULONG_PTR 值的位置的指针。

_Value [in]_

**ULONG_PTR**

指定要存储的 ULONG_PTR 值。

**返回值**

**VOID**

**RtlStoreUlongPtr** 可避免内存对齐错误。 如果 _Address_ 的值不符合 ULONG_PTR 的存储要求，**RtlStoreUlongPtr** 将在内存位置 (PUCHAR)_Address_ 的开头位置存储 _Value_ 的字节。

如果 _Address_ 指向非分页池，则 **RtlStoreUlongPtr** 可在任何 IRQL 上运行；否则，它必须在 <= APC_LEVEL 的 IRQL 上运行。

在 Windows 2000 和更高版本的 Windows 中可用。

IRQL：任何级别


## <a name="rtlstoreushort"></a>**RtlStoreUshort**

定义位置：Wdm.h

**RtlStoreUshort** 宏在特定的地址中存储 USHORT 值，可避免对齐错误。

_Address [out]_

**PUSHORT**

指向要在其中存储指定 USHORT 值的位置的指针。

_Value [in]_

**USHORT**

指定要存储的 USHORT 值。

**返回值**

**VOID**

如果 _Address_ 指向非分页池，则调用方可在任何 IRQL 上运行。 否则，调用方必须在 <= APC_LEVEL 的 IRQL 上运行。

在 Windows 2000 和更高版本的 Windows 中可用。

IRQL：任何级别


## <a name="write_register_buffer_ulong64"></a>**WRITE_REGISTER_BUFFER_ULONG64**

定义位置：Wdm.h

**WRITE_REGISTER_BUFFER_ULONG64** 宏将缓冲区中的多个 ULONG64 值写入指定的寄存器。

_Register [in]_

**PULONG64**

指向寄存器的指针，该寄存器必须是内存空间中的已映射范围。

_Buffer [in]_

**PULONG64**

指向 ULONG64 值数组要写入到的缓冲区的指针。

_Count [in]_

**ULONG**

指定要写入到寄存器中的 ULONG64 值的数量。

**返回值**

**VOID**

_Buffer_ 缓冲区的大小必须足够大，至少可包含指定数量的 ULONG64 值。

**WRITE_REGISTER_BUFFER_ULONG64** 宏的调用方可在任何 IRQL 上运行，前提是 _Buffer_ 缓冲区是常驻的，并且 _Register_ 寄存器是常驻的已映射设备内存。

仅在 64 位版本的 Windows 中可用。

IRQL：任何级别


## <a name="write_register_ulong64"></a>**WRITE_REGISTER_ULONG64**

定义位置：Wdm.h

**WRITE_REGISTER_ULONG64** 宏将 ULONG64 值写入指定的地址。

_volatile *Register [in]_

**ULONG64**

指向寄存器的指针，该寄存器必须是内存空间中的已映射范围。

_Value [in]_

**ULONG64**

指定要写入到寄存器中的 ULONG64 值。

**返回值**

**VOID**

**WRITE_REGISTER_ULONG64** 宏的调用方可在任何 IRQL 上运行，前提是 _Register_ 寄存器是常驻的已映射设备内存。

仅在 64 位版本的 Windows 中可用。

IRQL：任何级别


## <a name="zwcurrentprocess"></a>**ZwCurrentProcess**

定义位置：Wdm.h

**ZwCurrentProcess** 宏返回当前进程的句柄。

**返回值**

**HANDLE**

**ZwCurrentProcess** 返回表示当前进程的特殊句柄值。

返回的值不是真正的句柄，而是始终表示当前进程的特殊值。

**NtCurrentProcess** 和 **ZwCurrentProcess** 是同一 Windows 本机系统服务例程的两个版本。 内核模式驱动程序无法直接访问 Windows 内核中的 **NtCurrentProcess** 例程。 但是，内核模式驱动程序可以通过调用 **ZwCurrentProcess** 来间接访问此例程。

对于来自内核模式驱动程序的调用，Windows 本机系统服务例程的 **Nt_Xxx_** 和 **Zw_Xxx_** 版本的行为方式可能不同于它们处理和解释输入参数的方式。 有关例程 **Nt_Xxx_** 与 **Zw_Xxx_** 版本之间的关系的详细信息，请参阅[使用本机系统服务例程的 Nt 和 Zw 版本](using-nt-and-zw-versions-of-the-native-system-services-routines.md)。

所有支持的操作系统。

IRQL：任何级别


## <a name="zwcurrentthread"></a>**ZwCurrentThread**

定义位置：Wdm.h

**ZwCurrentThread** 宏返回当前线程的句柄。

**返回值**

**HANDLE**

**ZwCurrentThread** 返回表示当前线程的特殊句柄值。

返回的值不是真正的句柄，而是始终表示当前线程的特殊值。

**NtCurrentThread** 和 **ZwCurrentThread** 是同一 Windows 本机系统服务例程的两个版本。 内核模式驱动程序无法直接访问 Windows 内核中的 **NtCurrentThread** 例程。 但是，内核模式驱动程序可以通过调用 **ZwCurrentThread** 来间接访问此例程。

对于来自内核模式驱动程序的调用，Windows 本机系统服务例程的 **Nt_Xxx_** 和 **Zw_Xxx_** 版本的行为方式可能不同于它们处理和解释输入参数的方式。 有关例程 **Nt_Xxx_** 与 **Zw_Xxx_** 版本之间的关系的详细信息，请参阅[使用本机系统服务例程的 Nt 和 Zw 版本](using-nt-and-zw-versions-of-the-native-system-services-routines.md)。

所有支持的操作系统。

IRQL：任何级别