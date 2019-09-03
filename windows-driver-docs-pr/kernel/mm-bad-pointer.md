---
title: Windows 内核宏
description: Windows 内核宏
ms.assetid: 91366400-3307-4F13-A839-50BA85B7F73E
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 46ab783d7acff09e72a76d4a6ca3a8bb726d0f78
ms.sourcegitcommit: 2c3b8e0ea0e75b72067d2e22dc530390bc19b11e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2019
ms.locfileid: "67386005"
---
# <a name="windows-kernel-macros"></a>Windows 内核宏


以下列表包含 Windows 内核宏:


## <a name="address_and_size_to_span_pages"></a>**ADDRESS_AND_SIZE_TO_SPAN_PAGES**

定义在:Wdm。h

**ADDRESS_AND_SIZE_TO_SPAN_PAGES**宏按虚拟地址定义的虚拟范围以及传输请求的大小 (以字节为单位) 返回跨越的页数。

_Va [in]_

**PVOID**

指向作为范围基数的虚拟地址的指针。

_大小 [in]_

**ULONG**

指定传输请求的大小 (以字节为单位)。

**返回值**

**ULONG**

**ADDRESS_AND_SIZE_TO_SPAN_PAGES**返回虚拟范围从_Va_开始跨越的页数。

使 DMA 传输的驱动程序将调用**ADDRESS_AND_SIZE_TO_SPAN_PAGES** , 以确定是否必须将传输请求拆分为设备 DMA 操作序列。

驱动程序可以使用系统定义的常量 PAGE_SIZE 来确定要传输的字节数是否小于当前平台的虚拟内存页面大小。

**ADDRESS_AND_SIZE_TO_SPAN_PAGES**的调用方可以在任何 IRQL 上运行。 调用方必须确保指定的参数不会导致内存溢出。

从 Windows 2000 开始可用。


## <a name="byte_offset"></a>**BYTE_OFFSET**

定义在:Wdm。h

**BYTE_OFFSET**宏获取虚拟地址, 并返回该地址在页面中的字节偏移量。

_Va [in]_

**PVOID**

指向虚拟地址的指针。

**返回值**

**ULONG**

**BYTE_OFFSET**返回虚拟地址的偏移量部分。

从 Windows 2000 开始可用。

IRQL任何级别


## <a name="bytes_to_pages"></a>**BYTES_TO_PAGES**

定义在:Wdm。h

**BYTES_TO_PAGES**宏获取传输请求的大小 (以字节为单位), 并计算包含这些字节所需的页数。

_大小 [in]_

**ULONG**

指定传输请求的大小 (以字节为单位)。

**返回值**

**ULONG**

**BYTES_TO_PAGES**返回包含指定字节数所需的页数。

系统定义的常量 PAGE_SIZE 可用于确定传输的给定长度是否小于当前平台的虚拟内存页面大小。

从 Windows 2000 开始可用。

IRQL任何级别


## <a name="containing_record"></a>**CONTAINING_RECORD**

定义在:Ntdef

**CONTAINING_RECORD**宏在给定结构的类型和包含结构中的字段地址的情况, 返回结构实例的基址。

_Address [in]_

**PCHAR**

一个指针, 指向类型类型的结构实例中的字段。

_类型 [in]_

**类别**

要返回其基址的结构类型的名称。

_Field [in]_

**PCHAR**

按_地址_指向并包含在类型类型的结构中的字段的名称。

**返回值**

**PCHAR**

返回包含_字段_的结构的基址。

调用以确定在调用方具有指向此类结构内的字段的指针时, 其类型为已知的结构的基址。 此宏适用于符号访问已知类型结构中的其他字段。

从 Windows 2000 开始可用。

IRQL任何级别


## <a name="ioskipcurrentirpstacklocation"></a>**IoSkipCurrentIrpStackLocation**

定义在:Wdm。h

\N **IoSkipCurrentIrpStackLocation**宏会修改系统的[**IO_STACK_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)数组指针, 以便当当前驱动程序调用下一个较低的驱动程序时, 该驱动程序将收到与已收到当前驱动程序。

_Irp [in, out]_

**PIRP**

指向 IRP 的指针。

**返回值**

**导致**

当驱动程序将 IRP 发送到下一个较低版本的驱动程序时, 如果不打算提供[_IoCompletion_](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程 (存储在驱动程序的[**IO_STACK_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)中的地址, 则驱动程序可以调用**IoSkipCurrentIrpStackLocation** )。结构)。 如果在调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)之前调用**IoSkipCurrentIrpStackLocation** , 则下一个较低的驱动程序将收到你的驱动程序收到的相同**IO_STACK_LOCATION** 。

如果要为 IRP 提供_IoCompletion_例程, 则驱动程序应调用[**IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)而不是**IoSkipCurrentIrpStackLocation**。 如果编写错误的驱动程序会导致错误调用**IoSkipCurrentIrpStackLocation** , 然后设置完成例程, 则此驱动程序可能会覆盖由其下的驱动程序设置的完成例程。

如果驱动程序挂起了 IRP, 则在将 IRP 传递到下一个较低版本的驱动程序之前, 驱动程序不应调用**IoSkipCurrentIrpStackLocation** 。 如果驱动程序在将已挂起的 IRP 传递到下一个较低版本的驱动程序之前对其调用**IoSkipCurrentIrpStackLocation** , 则在下一个驱动程序的 i/o 堆栈位置的**控件**成员中仍会设置 SL_PENDING_RETURNED 标志。 由于下一个驱动程序拥有该堆栈位置, 并且可以对其进行修改, 因此可能会清除挂起的标志。 这种情况可能会导致操作系统发出 bug 检查或从不完成对 IRP 的处理。

相反, 已挂起 IRP 的驱动程序应调用**IoCopyCurrentIrpStackLocationToNext** , 以便在调用**IoCallDriver**之前为下一个较低版本的驱动程序设置新的堆栈位置。

如果你的驱动程序调用**IoSkipCurrentIrpStackLocation**, 请小心不要修改**IO_STACK_LOCATION**结构, 因为这可能会无意中影响较低的驱动程序或系统与该驱动程序相关的行为。 例如, 修改**IO_STACK_LOCATION**结构的**参数**union 或调用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)。

从 Windows 2000 开始可用。

IRQL任何级别


## <a name="keinitializecallbackrecord"></a>**KeInitializeCallbackRecord**

定义在:Wdm。h

**KeInitializeCallbackRecord**宏初始化[**KBUGCHECK_CALLBACK_RECORD**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)或[**KBUGCHECK_REASON_CALLBACK_RECORD**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构。

_CallbackRecord [in]_

**PKBUGCHECK_CALLBACK_RECORD**

指向**KBUGCHECK_CALLBACK_RECORD**或**KBUGCHECK_REASON_CALLBACK_RECORD**结构的指针。 该结构必须位于驻留内存中, 如非分页池。

**返回值**

**导致**

在 windows 2000 和更高版本的 Windows 中可用。

IRQL任何级别


## <a name="mm_bad_pointer"></a>**MM_BAD_POINTER**

定义在:Wdm。h

驱动程序可以将**MM_BAD_POINTER**宏用作错误的指针值, 以分配给未初始化或不再有效的指针变量。 尝试访问此无效指针变量指向的内存位置将导致 bug 检查。

在许多硬件平台上, 地址 0 (通常表示为命名常量**NULL**) 是无效地址, 但驱动程序开发人员不应假定地址0在所有平台中都是通用的。 如果将未初始化或无效的指针变量设置为地址 0, 则可能不会始终保证会检测到通过这些指针进行不适当的访问。

与此相反, 值**MM_BAD_POINTER**保证在运行驱动程序的每个平台上都是无效地址。

在地址0为无效地址的平台上, 以 IRQL < DISPATCH_LEVEL 访问地址0的驱动程序会导致`try/except`语句无意中捕获到异常 (访问冲突)。 因此, 驱动程序的异常处理代码可能会掩盖无效访问权限, 并防止在调试过程中检测到该访问代码。 但是, 对**MM_BAD_POINTER**地址的访问保证会导致错误检查, 异常处理程序无法屏蔽该检查。

下面的代码示例演示如何将值**MM_BAD_POINTER**分配给名`ptr`为的指针变量。 Ntdef 头文件将 PUCHAR 类型定义为指向的指针`unsigned char`。

`PUCHAR ptr = (PUCHAR)MM_BAD_POINTER; // Now _ptr is guaranteed to fault._`

设置`ptr`为**MM_BAD_POINTER**后, 尝试访问指向的`ptr`内存位置将导致 bug 检查。

事实上, **MM_BAD_POINTER**是无效地址的整个页面的基址。 因此, **MM_BAD_POINTER**到 (**MM_BAD_POINTER** + **PAGE_SIZE** -1) 范围内的地址的任何访问都将导致 bug 检查。

从 Windows 8.1 开始, **MM_BAD_POINTER**宏是在 Wdm 头文件中定义的。 但是, 使用此宏定义的驱动程序代码可以在 Windows Vista 以前版本的 Windows 中运行。

从 Windows Vista 开始, [**MmBadPointer**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm64bitphysicaladdress)全局变量可用作指针值的指针, 该指针值保证是无效地址。 但是, 从 Windows 8.1 开始, 不推荐使用**MmBadPointer** , 而应将驱动程序更新为改用**MM_BAD_POINTER**宏。

从 Windows 8.1 \ 开始可用。 与 Windows Vista 以前版本的 Windows 兼容。 _


## <a name="mmgetmdlbytecount"></a>**MmGetMdlByteCount**

定义在:Wdm。h

**MmGetMdlByteCount**宏返回指定 MDL 所描述的缓冲区的长度 (以字节为单位)。

_Mdl [in]_

**PMDL**

指向[**MDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_mdl)结构的指针, 该结构描述物理内存中虚拟内存缓冲区的布局。 有关详细信息, 请参阅[Using MDLs](using-mdls.md)。

**返回值**

**ULONG**

## <a name="mmgetmdlbytecount-returns-the-length-in-bytes-of-the-buffer-described-by-_mdl_"></a>**MmGetMdlByteCount**返回_Mdl_所描述的缓冲区的长度 (以字节为单位)。

**MmGetMdlByteCount**的调用方可以在任何 IRQL 上运行。 通常, 调用方在 IRQL < = DISPATCH_LEVEL 的情况下运行。

从 Windows 2000 开始可用。

IRQL任何级别


## <a name="mmgetmdlbyteoffset"></a>**MmGetMdlByteOffset**

定义在:Wdm。h

**MmGetMdlByteOffset**宏返回给定 MDL 所描述的缓冲区初始页面内的字节偏移量。

_Mdl [in]_

**PMDL**

指向 MDL 的指针。

**返回值**

**ULONG**

## <a name="mmgetmdlbyteoffset-returns-the-offset-in-bytes"></a>**MmGetMdlByteOffset**返回偏移量 (以字节为单位)。

**MmGetMdlByteOffset**的调用方可以在任何 IRQL 上运行。 通常, 调用方在 IRQL < = DISPATCH_LEVEL 的情况下运行。

在 windows 2000 和更高版本的 Windows 中可用。

IRQL任何级别


## <a name="mmgetmdlpfnarray"></a>**MmGetMdlPfnArray**

定义在:Wdm。h

**MmGetMdlPfnArray**宏返回一个指针, 该指针指向与内存描述符列表 (MDL) 关联的物理页码数组的开头。

_Mdl [in]_

**PMDL**

指向 MDL 的指针。

**返回值**

**PPFN_NUMBER**

指向与 MDL 关联的物理页码数组的开头的指针。 数组中的条目数为**ADDRESS_AND_SIZE_TO_SPAN_PAGES**(**MmGetMdlVirtualAddress**(_mdl_), **MmGetMdlByteCount**(_mdl_))。 每个 array 元素都是 PFN_NUMBER 类型的整数值, 在中定义:Wdm, 如下所示:

`cpp typedef ULONG PFN_NUMBER, *PPFN_NUMBER;`

**注意**更改数组的内容可能导致难以诊断的微妙系统问题。 建议您不要读取或更改此数组的内容。

对于可分页内存, 数组的内容仅对使用[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)锁定的缓冲区有效。 对于非分页池, 数组的内容仅对用[**MmBuildMdlForNonPagedPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmbuildmdlfornonpagedpool)、 [**MmAllocatePagesForMdlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatepagesformdlex)或[**MmAllocatePagesForMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatepagesformdl)更新的 MDL 有效。

有关 MDLs 的详细信息, 请参阅[使用 MDLs](using-mdls.md)。

从 Windows 2000 开始可用。

IRQL任何级别


## <a name="mmgetmdlvirtualaddress"></a>**MmGetMdlVirtualAddress**

定义在:Wdm。h

**MmGetMdlVirtualAddress**宏返回 MDL 描述的缓冲区的基本虚拟地址。

_Mdl [in]_

**PMDL**

指向 MDL 的指针, 该 MDL 描述要为其返回初始虚拟地址的缓冲区。

**返回值**

**PVOID**

## <a name="mmgetmdlvirtualaddress-returns-the-starting-virtual-address-of-the-mdl"></a>**MmGetMdlVirtualAddress**返回 MDL 的起始虚拟地址。

**MmGetMdlVirtualAddress**返回的虚拟地址在当前线程上下文中不一定有效。 较低级别的驱动程序不应尝试使用返回的虚拟地址来访问内存, 尤其是用户内存空间。

返回的地址用作 MDL 中物理地址条目的索引, 可以输入到[**MapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pmap_transfer)。

**MmGetMdlVirtualAddress**的调用方可以在任何 IRQL 上运行。 通常, 调用方在 IRQL = DISPATCH_LEVEL 上运行, 因为通常会调用此例程来获取**MapTransfer**的_CurrentVa_参数。

在 windows 2000 和更高版本的 Windows 中可用。

IRQL任何级别


## <a name="mmgetsystemaddressformdlsafe"></a>**MmGetSystemAddressForMdlSafe**

定义在:Wdm。h

**MmGetSystemAddressForMdlSafe**宏为指定的 MDL 描述的缓冲区返回一个未分页的系统空间虚拟地址。

_Mdl [in]_

**PMDL**

指向要映射其对应基虚拟地址的缓冲区的指针。

_优先级 [in]_

## <a name="mm_page_priority"></a>**Mm_PAGE_PRIORITY**

指定一个**MM_PAGE_PRIORITY**值, 该值指示在低可用 PTE 条件下成功的重要性。 指定**LowPagePriority**、 **NormalPagePriority**或**HighPagePriority**的优先级值。 从 Windows 8 开始, 指定的优先级值可以是运算和**MdlMappingNoWrite**或**MdlMappingNoExecute**标志。

*   **LowPagePriority**表示如果系统资源相对较低, 映射请求可能会失败。 这种情况的一个示例是不关键的网络连接, 驱动程序可以在其中处理映射失败。

*   **NormalPagePriority**表示如果系统资源不足, 则映射请求可能会失败。 这种情况的一个示例是不重要的本地文件系统请求。

*   **HighPagePriority**指示除非系统完全用尽资源, 否则映射请求必须失败。 此情况的一个示例是驱动程序中的分页文件路径。

*   **MdlMappingNoWrite**指示映射的物理页面将被配置为非写入 (只读) 内存。 从 Windows 8 开始, 此标志位可为按位与**MM_PAGE_PRIORITY**值的运算, 以指定禁用写入的内存。

*   **MdlMappingNoExecute**指示映射的物理页面将被配置为 "无执行内存"。 从 Windows 8 开始, 此标志位可为按位与**MM_PAGE_PRIORITY**值的运算, 以指定禁用指令执行的内存。 作为最佳做法, 为 Windows 8 及更高版本的 Windows 编写的驱动程序应始终指定无需执行内存, 除非显式需要可执行内存。

*   **返回值**

    **PVOID**

    **MmGetSystemAddressForMdlSafe**返回用于映射指定 MDL 描述的物理页面的基本系统空间虚拟地址。 如果页面尚未映射到系统地址空间, 并且尝试将它们映射到, 则返回**NULL** 。

此例程将指定 MDL 描述的物理页面映射到系统地址空间 (如果它们尚未映射到系统地址空间)。

程控 I/O (PIO) 设备的驱动程序调用此例程, 以将用户模式缓冲区 ( **Irp > MdlAddress**上的 MDL 和已映射到用户模式的虚拟地址范围) 映射到系统地址空间中的范围。

进入此例程后, 指定的 MDL 必须描述锁定的物理页面。 锁定的 MDL 可以通过使用[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)、 [**MmBuildMdlForNonPagedPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmbuildmdlfornonpagedpool)、 [**IoBuildPartialMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildpartialmdl)或[**MmAllocatePagesForMdlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatepagesformdlex)例程来生成。

如果不再需要**MmGetSystemAddressForMdlSafe**返回的系统地址空间映射, 则必须将其释放。 发布映射所需的步骤取决于 MDL 的生成方式。 以下是四种可能的情况:

*   如果 MDL 是通过调用**MmProbeAndLockPages**例程生成的, 则无需显式释放系统地址空间映射。 相反, 如果分配了映射, 则调用[**MmUnlockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunlockpages)例程会释放映射。

*   如果 MDL 是通过调用**MmBuildMdlForNonPagedPool**例程生成的, 则**MmGetSystemAddressForMdlSafe**重复使用现有的系统地址空间映射, 而不是创建一个新的。 在这种情况下, 不需要清除 (也就是说, 无需进行解除锁定和取消映射)。

*   如果 MDL 是通过调用**IoBuildPartialMdl**例程生成的, 则驱动程序必须调用[**MmPrepareMdlForReuse**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)例程或[**IoFreeMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreemdl)例程才能释放系统地址空间映射。

*   如果 MDL 是通过调用**MmAllocatePagesForMdlEx**例程生成的, 则驱动程序必须调用**MmUnmapLockedPages**例程来释放系统地址空间映射。 如果对 MDL 多次调用**MmGetSystemAddressForMdlSafe** , 则后续**MmGetSystemAddressForMdlSafe**调用只会返回第一次调用所创建的映射。 对**MmUnmapLockedPages**的调用足以释放此映射。

从 Windows 7 和 Windows Server 2008 R2 开始, 无需为**MmAllocatePagesForMdlEx**创建的 MDL 显式调用**MmUnmapLockedPages** 。 相反, 调用[**MmFreePagesFromMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmfreepagesfrommdl)例程会释放系统地址空间映射 (如果已分配一个)。

若要创建新的系统地址空间映射, **MmGetSystemAddressForMdlSafe**调用**MmMapLockedPagesSpecifyCache** , 并将_CacheType_参数设置为**MmCached**。 需要**MmCached**以外的缓存类型的驱动程序应直接调用**MmMapLockedPagesSpecifyCache** , 而不是调用**MmGetSystemAddressForMdlSafe**。 有关_CacheType_参数的详细信息, 请参阅[**MmMapLockedPagesSpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpagesspecifycache)。

在对**MmMapLockedPagesSpecifyCache**的调用中, 仅当 MDL 描述的页面还没有与其关联的缓存类型时, 才使用指定的缓存类型。 不过, 几乎在所有情况下, 页面都已有关联的缓存类型, 并且此缓存类型由新的映射使用。 此规则的例外情况是, **MmAllocatePagesForMdl**分配的页面将缓存类型设置为**MmCached** , 而与页面的原始缓存类型无关。

一次只能有一个线程可以安全地调用特定 MDL 的**MmGetSystemAddressForMdlSafe** , 因为此例程假定调用线程拥有 MDL。 但是, 可以通过从同一个线程进行所有调用, 或从多个线程 (如果调用是通过显式同步调用), 为同一 MDL 调用**MmGetSystemAddressForMdlSafe**一次。

如果驱动程序必须将请求拆分为较小的请求, 则驱动程序可以分配其他 MDLs, 或驱动程序可以使用**IoBuildPartialMdl**例程。

返回的基址与 MDL 中的虚拟地址具有相同的偏移量。

Windows 98 不支持**MmGetSystemAddressForMdlSafe**。 改用[**MmGetSystemAddressForMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmgetsystemaddressformdl) 。

由于此宏会调用[**MmMapLockedPagesSpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpagesspecifycache), 因此使用它可能需要链接到 ntoskrnl.exe。

从 Windows 2000 开始可用。

IRQL < = DISPATCH_LEVEL


## <a name="mminitializemdl"></a>**MmInitializeMdl**

定义在:Wdm。h

**MmInitializeMdl**宏初始化 MDL 的标头。

_MemoryDescriptorList [in]_

**PMDL**

指向缓冲区的指针, 该缓冲区将初始化为 MDL。 有关详细信息, 请参阅下一节。

_BaseVa [in]_

**PVOID**

指向缓冲区的基虚拟地址的指针。

_长度 [in]_

**SIZE_T**

指定 MDL 要描述的缓冲区的长度 (以字节为单位)。 此例程支持最大缓冲区长度 MAXULONG 字节。

**返回值**

**导致**

_MemoryDescriptorList_指向的缓冲区必须在非分页内存中分配。 此缓冲区的大小必须至少为**sizeof**(MDL) + **sizeof**(PFN_NUMBER)**ADDRESS_AND_SIZE_TO_SPAN_PAGES**(_BaseVa_, _Length_)。

在 windows 2000 和更高版本的 Windows 中可用。

IRQL < = DISPATCH_LEVEL


## <a name="mmpreparemdlforreuse"></a>**MmPrepareMdlForReuse**

定义在:Wdm。h

**MmPrepareMdlForReuse**宏释放与部分 MDL 关联的资源, 以便可以重复使用 mdl。

_Mdl [in]_

**PMDL**

指向部分 MDL 的指针, 它将准备用于重用。

**返回值**

**导致**

此宏由驱动程序使用, 该驱动程序对[**IoBuildPartialMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildpartialmdl)例程的调用中的_TargetMdl_参数重复使用相同的分配 MDL。 如果在对**MmPrepareMdlForReuse**的调用中, 指定的部分 MDL 具有与系统地址空间关联的映射, 则**MmPrepareMdlForReuse**将释放该映射, 以使 MDL 可以重复使用。

**MmPrepareMdlForReuse**仅接受**IoBuildPartialMdl**生成的部分 MDLs。 如果**MmPrepareMdlForReuse**接收到的 MDL 映射到系统地址空间, 但不是由**IoBuildPartialMdl**生成的, 则**MmPrepareMdlForReuse**不会释放该映射, 而在已检查生成中, 将导致断言失败。

有关部分 MDLs 的详细信息, 请参阅[使用 MDLs](using-mdls.md)。

在 windows 2000 和更高版本的 Windows 中可用。

IRQL < = DISPATCH_LEVEL


## <a name="page_align"></a>**PAGE_ALIGN**

定义在:Wdm。h

**PAGE_ALIGN**宏为给定的虚拟地址返回一个页面对齐的虚拟地址。

_Va [in]_

**PVOID**

指向虚拟地址的指针。

**返回值**

**PVOID**

## <a name="page_align-returns-a-pointer-to-the-page-aligned-virtual-address"></a>**PAGE_ALIGN**返回指向与页面对齐的虚拟地址的指针。

从 Windows 2000 开始可用。

IRQL任何级别


## <a name="paged_code"></a>**PAGED_CODE**

定义在:Wdm。h

**PAGED_CODE**宏可确保正在运行的调用线程的 IRQL 足以允许分页。

**返回值**

**导致**

如果 IRQL > APC_LEVEL, 则**PAGED_CODE**宏会导致系统断言。

应在每个驱动程序例程 (其中包含可分页的代码或访问可分页的代码) 的开头发出对此宏的调用。

**PAGED_CODE**宏仅在驱动程序代码执行宏的位置检查 IRQL。 如果该代码随后引发了 IRQL, 则宏将不会检测到此更改。 驱动程序开发人员应使用[静态驱动程序验证](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)程序和[驱动程序验证](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)器来检测在执行驱动程序例程期间错误地引发了 IRQL 的时间。

**PAGED_CODE**宏仅适用于已检查的生成。

从 Windows 2000 开始可用。


## <a name="paged_code_locked"></a>**PAGED_CODE_LOCKED**

定义在:Wdm。h

**PAGED_CODE_LOCKED**宏断言当前正在运行的代码节是可分页的, 并且在运行之前必须已锁定到内存中。

**返回值**

**导致**

可分页代码必须遵循某些限制 (如 IRQL < = APC_LEVEL), 除非已将其锁定到位。 必须先将对**PAGED_CODE_LOCKED**的调用开始, 必须锁定为正确工作的可分页例程。

有关将代码段锁定到适当位置的详细信息, 请参阅[锁定可分页的代码或数据](locking-pageable-code-or-data.md)。


## <a name="posetdevicebusy"></a>**PoSetDeviceBusy**

定义在:Wdm。h

**PoSetDeviceBusy**宏通知[电源管理器](power-manager.md)与_IdlePointer_关联的设备忙。

_IdlePointer [in, out]_

**PULONG**

指定以前由[**PoRegisterDeviceForIdleDetection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-poregisterdeviceforidledetection)返回的非**NULL**空闲指针。 请注意, **PoRegisterDeviceForIdleDetection**可能返回**NULL**指针。 **PoSetDeviceBusy**的调用方必须先验证指针是否为非**NULL** , 然后再将其传递给**PoSetDeviceBusy**。

**返回值**

**导致**

**注意**[**PoSetDeviceBusyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-posetdevicebusyex)例程是**PoSetDeviceBusy**宏的直接替换。 如果要为带有 Service Pack 1 (SP1) 的 Windows Vista 和更高版本的 Windows 编写新的驱动程序代码, 请调用**PoSetDeviceBusyEx**而不是**PoSetDeviceBusy**。

驱动程序将**PoSetDeviceBusy**与**PoRegisterDeviceForIdleDetection**一起使用, 以便为其设备启用系统空闲检测。 如果注册为空闲检测的设备处于空闲状态, 则电源管理器将发送[**IRP_MN_SET_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)请求以使设备进入请求的睡眠状态。

**PoSetDeviceBusy**报告设备处于繁忙状态, 以便电源管理器可以重新启动其空闲倒计时。 如果未启动设备, **PoSetDeviceBusy**不会更改其状态。 也就是说, 它不会导致系统发送开机请求。

驱动程序应在每个 i/o 请求上调用**PoSetDeviceBusy** 。

从 Windows 2000 开始可用。

IRQL任何级别


## <a name="psgetcurrentprocess"></a>**PsGetCurrentProcess**

定义在:Ntddk

返回一个指针, 该指针指向当前线程的进程。

**返回值**

指向不透明进程对象的指针。



从 Windows 2000 开始可用。

IRQL任何级别


## <a name="read_register_buffer_ulong64"></a>**READ_REGISTER_BUFFER_ULONG64**

定义在:Wdm。h

**READ_REGISTER_BUFFER_ULONG64**宏从指定的寄存器地址将一些 ULONG64 值读取到缓冲区中。

_注册 [in]_

**PULONG64**

指向寄存器的指针, 它必须是内存空间中的映射范围。

_Buffer [out]_

**PULONG64**

指向缓冲区的指针, ULONG64 值的数组将读入该缓冲区。

_计数 [in]_

**ULONG**

指定要读入到缓冲区中的 ULONG64 值的数量。

**返回值**

**导致**

_缓冲区_缓冲区的大小必须足以至少包含指定数量的 ULONG64 值。

**READ_REGISTER_BUFFER_ULONG64**宏的调用方可以在任何 IRQL 的情况下运行, 前提是_缓冲区_缓冲区处于驻留状态且_寄存器_注册为驻留的、映射的设备内存。

仅适用于64位版本的 Windows。

IRQL任何级别


## <a name="read_register_ulong64"></a>**READ_REGISTER_ULONG64**

定义在:Wdm。h

**READ_REGISTER_ULONG64**宏从指定的寄存器地址读取 ULONG64 值。

_volatile * 寄存器 [in]_

**ULONG64**

指向寄存器地址的指针, 该地址必须是内存空间中的映射范围。

**返回值**

**ULONG64**

**READ_REGISTER_ULONG64**返回从指定的寄存器地址读取的 ULONG64 值。

假设_注册_地址是驻留的、映射的设备内存, **READ_REGISTER_ULONG64**宏的调用方可以在任何 IRQL 上运行。

仅适用于64位版本的 Windows。

IRQL任何级别


## <a name="round_to_pages"></a>**ROUND_TO_PAGES**

定义在:Wdm。h

**ROUND_TO_PAGES**宏的大小以字节为单位, 并将其向上舍入到下一个整页。

_大小 [in]_

**ULONG_PTR**

指定向上舍入到多页的大小 (以字节为单位)。

**返回值**

**ULONG_PTR**

**ROUND_TO_PAGES**返回向上舍入到当前平台的虚拟内存页面大小的倍数的输入大小。

**ROUND_TO_PAGES**的调用方可以在任何 IRQL 上运行。 调用方必须确保所提供的参数不会导致内存溢出。

IRQL任何级别


## <a name="rtlequalluid"></a>**RtlEqualLuid**

定义在:Wdm。h

**返回值**

从 Windows 2000 开始可用。

IRQL任何级别


## <a name="rtlinitemptyansistring"></a>**RtlInitEmptyAnsiString**

定义在:Wdm。h

**RtlInitEmptyAnsiString**宏初始化一个空的计数 ANSI 字符串。

_DestinationString [out]_

**PANSI_STRING**

指向要初始化的[**ANSI_STRING**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_string)结构的指针。

_缓冲区 [in]_

**PCHAR**

指向要用于包含 WCHAR 字符串的调用方分配的缓冲区的指针。

_BufferSize [in]_

**USHORT**

_缓冲区_所指向的缓冲区的长度 (以字节为单位)。

**返回值**

**导致**

_DestinationString_参数指向的结构的成员按如下方式初始化。

*   **Length**。 无.

*   **MaximumLength**。 _BufferSize_。

*   **缓冲区**。 _SourceString_。

若要初始化非空计数的 Unicode 字符串, 请调用[**RtlInitAnsiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlinitansistring)。

在 Microsoft Windows XP 和更高版本的 Windows 中可用。

IRQL任何级别


## <a name="rtlinitemptyunicodestring"></a>**RtlInitEmptyUnicodeString**

定义在:Wdm。h

**RtlInitEmptyUnicodeString**宏初始化一个空的计数 Unicode 字符串。

_DestinationString [out]_

**PUNICODE_STRING**

指向要初始化的[**UNICODE_STRING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/ns-wudfwdm-_unicode_string)结构的指针。

_缓冲区 [in]_

**PWCHAR**

指向要用于包含 WCHAR 字符串的调用方分配的缓冲区的指针。

_BufferSize [in]_

**USHORT**

_缓冲区_所指向的缓冲区的长度 (以字节为单位)。

**返回值**

**导致**

_DestinationString_参数指向的结构的成员按如下方式进行初始化。

*   **Length**。 无.

*   **MaximumLength**。 _BufferSize_。

*   **缓冲区**。 _SourceString_。

若要初始化非空计数的 Unicode 字符串, 请调用[**RtlInitUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlinitunicodestring)。

可从 Windows XP 开始使用。

IRQL任何级别


## <a name="rtliszeroluid"></a>**RtlIsZeroLuid**

定义在:Ntddk

**RtlIsZeroLuid**宏确定指定的 luid 是否为 0 luid。

_L1 [in]_

**PLUID**

指定要检查的[**LUID**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_luid) 。

**返回值**

**变量**

如果_L1_为零, 则**RtlIsZeroLuid**返回**TRUE** , 否则返回**FALSE** 。

IRQL任何级别


## <a name="rtlretrieveulong"></a>**RtlRetrieveUlong**

定义在:Wdm。h

**RtlRetrieveUlong**宏从源地址中检索 ULONG 值, 从而避免对齐错误。 目标地址假定为对齐。

_DestinationAddress [out]_

**PULONG**

一个指针, 指向要在其中存储 ULONG 值的 ULONG 对齐位置。

_SourceAddress [in]_

**PULONG**

一个指针, 指向要从中检索 ULONG 值的位置。

**返回值**

**导致**

如果给定的地址位于非分页池, 则**RtlRetrieveUlong**的调用方可以在任何 IRQL 上运行。 否则, 调用方必须以 IRQL < = APC_LEVEL 运行。

在 windows 2000 和更高版本的 Windows 中可用。


## <a name="rtlretrieveushort"></a>**RtlRetrieveUshort**

定义在:Wdm。h

**RtlRetrieveUshort**宏从源地址中检索 USHORT 值, 避免对齐错误。

_DestinationAddress [out]_

**PUSHORT**

一个指针, 指向要存储值的 USHORT 对齐位置。

_SourceAddress [in]_

**PUSHORT**

一个指针, 指向要从中检索值的位置。

**返回值**

**导致**

如果给定的地址位于非分页池, 则**RtlRetrieveUshort**的调用方可以在任何 IRQL 上运行。 否则, 调用方必须以 IRQL < = APC_LEVEL 运行。

在 windows 2000 和更高版本的 Windows 中可用。

IRQL任何级别


## <a name="rtlstoreulong"></a>**RtlStoreUlong**

定义在:Wdm。h

**RtlStoreUlong**宏在特定地址存储 ULONG 值, 从而避免对齐错误。

_Address [out]_

**PULONG**

指向存储指定 ULONG 值的位置的指针。

_值 [in]_

**ULONG**

指定要存储的 ULONG 值。

**返回值**

**导致**

如果_地址_指向非分页池, 则调用方可以在任何 IRQL 上运行。 否则, 调用方必须以 IRQL < = APC_LEVEL 运行。

在 windows 2000 和更高版本的 Windows 中可用。

IRQL任何级别


## <a name="rtlstoreulonglong"></a>**RtlStoreUlonglong**

定义在:Wdm。h

**RtlStoreUlonglong**宏在指定的内存地址存储指定的 ULONGLONG 值, 避免内存对齐错误。

_Address [out]_

**PULONGLONG**

一个指针, 指向要存储指定 ULONGLONG 值的位置。

_值 [in]_

**ULONGLONG**

要存储的 ULONGLONG 值。

**返回值**

**导致**

**RtlStoreUlonglong**避免了内存对齐错误。 如果通过_地址_指定的地址与 ULONGLONG 的存储要求不符, 则**RtlStoreUlonglong**将从内存位置 (PUCHAR)_地址_开始存储_值_的字节。

如果_地址_指向非分页池, **RtlStoreUlonglong**将以任何 IRQL 运行;否则, 它必须以 IRQL < = APC_LEVEL 运行。

从 Windows 2000 开始可用。

IRQL任何级别


## <a name="rtlstoreulongptr"></a>**RtlStoreUlongPtr**

定义在:Wdm。h

**RtlStoreUlongPtr**宏在指定的内存位置存储指定的 ULONG_PTR 值, 从而避免内存对齐错误。

_Address [out]_

**PULONG_PTR**

一个指针, 指向要在其中存储 ULONG_PTR 值的位置。

_值 [in]_

**ULONG_PTR**

指定要存储的 ULONG_PTR 值。

**返回值**

**导致**

**RtlStoreUlongPtr**避免了内存对齐错误。 如果_Address_的值与 ULONG_PTR 的存储要求不匹配, 则**RtlStoreUlongPtr**将从内存位置 (PUCHAR)_地址_开始存储_值_的字节。

如果_地址_指向非分页池, **RtlStoreUlongPtr**将以任何 IRQL 运行;否则, 它必须以 IRQL < = APC_LEVEL 运行。

在 windows 2000 和更高版本的 Windows 中可用。

IRQL任何级别


## <a name="rtlstoreushort"></a>**RtlStoreUshort**

定义在:Wdm。h

**RtlStoreUshort**宏在特定地址存储 USHORT 值, 避免对齐错误。

_Address [out]_

**PUSHORT**

指向存储指定 USHORT 值的位置的指针。

_值 [in]_

**USHORT**

指定要存储的 USHORT 值。

**返回值**

**导致**

如果_地址_指向非分页池, 则调用方可以在任何 IRQL 上运行。 否则, 调用方必须以 IRQL < = APC_LEVEL 运行。

在 windows 2000 和更高版本的 Windows 中可用。

IRQL任何级别


## <a name="write_register_buffer_ulong64"></a>**WRITE_REGISTER_BUFFER_ULONG64**

定义在:Wdm。h

**WRITE_REGISTER_BUFFER_ULONG64**宏将多个 ULONG64 值从缓冲区写入指定的寄存器。

_注册 [in]_

**PULONG64**

指向寄存器的指针, 它必须是内存空间中的映射范围。

_缓冲区 [in]_

**PULONG64**

指向缓冲区的指针, ULONG64 值数组将写入该缓冲区。

_计数 [in]_

**ULONG**

指定要写入寄存器的 ULONG64 值的数量。

**返回值**

**导致**

_缓冲区_缓冲区的大小必须足以至少包含指定数量的 ULONG64 值。

**WRITE_REGISTER_BUFFER_ULONG64**宏的调用方可以在任何 IRQL 的情况下运行, 前提是_缓冲区_缓冲区处于驻留状态且_寄存器_注册为驻留的、映射的设备内存。

仅适用于64位版本的 Windows。

IRQL任何级别


## <a name="write_register_ulong64"></a>**WRITE_REGISTER_ULONG64**

定义在:Wdm。h

**WRITE_REGISTER_ULONG64**宏将 ULONG64 值写入指定的地址。

_volatile * 寄存器 [in]_

**ULONG64**

指向寄存器的指针, 它必须是内存空间中的映射范围。

_值 [in]_

**ULONG64**

指定要写入寄存器的 ULONG64 值。

**返回值**

**导致**

假设_注册_注册为驻留的、映射的设备内存, **WRITE_REGISTER_ULONG64**宏的调用方可以在任何 IRQL 上运行。

仅适用于64位版本的 Windows。

IRQL任何级别


## <a name="zwcurrentprocess"></a>**ZwCurrentProcess**

定义在:Wdm。h

**ZwCurrentProcess**宏返回当前进程的句柄。

**返回值**

**柄**

**ZwCurrentProcess**返回一个表示当前进程的特殊句柄值。

返回的值不是真正的句柄, 但它是始终表示当前进程的特殊值。

**NtCurrentProcess**和**ZwCurrentProcess**是同一 Windows Native 系统服务例程的两个版本。 内核模式驱动程序无法直接访问 Windows 内核中的**NtCurrentProcess**例程。 但内核模式驱动程序可以通过调用**ZwCurrentProcess**间接访问此例程。

对于来自内核模式驱动程序的调用, Windows 本机系统服务例程的**Nt_Xxx_** 和**Zw_Xxx_** 版本的行为方式与它们处理和解释输入参数的方式不同。 有关例程的**Nt_Xxx_** 和**Zw_Xxx_** 版本之间的关系的详细信息, 请参阅[使用本机系统服务例程的 Nt 和 Zw 版本](using-nt-and-zw-versions-of-the-native-system-services-routines.md)。

所有受支持的操作系统。

IRQL任何级别


## <a name="zwcurrentthread"></a>**ZwCurrentThread**

定义在:Wdm。h

**ZwCurrentThread**宏将返回当前线程的句柄。

**返回值**

**柄**

**ZwCurrentThread**返回一个表示当前线程的特殊句柄值。

返回的值不是真正的句柄, 但它是始终表示当前线程的特殊值。

**NtCurrentThread**和**ZwCurrentThread**是同一 Windows Native 系统服务例程的两个版本。 内核模式驱动程序无法直接访问 Windows 内核中的**NtCurrentThread**例程。 但内核模式驱动程序可以通过调用**ZwCurrentThread**例程来间接访问此例程。

对于来自内核模式驱动程序的调用, Windows 本机系统服务例程的**Nt_Xxx_** 和**Zw_Xxx_** 版本的行为方式与它们处理和解释输入参数的方式不同。 有关例程的**Nt_Xxx_** 和**Zw_Xxx_** 版本之间的关系的详细信息, 请参阅[使用本机系统服务例程的 Nt 和 Zw 版本](using-nt-and-zw-versions-of-the-native-system-services-routines.md)。

所有受支持的操作系统。

IRQL任何级别










