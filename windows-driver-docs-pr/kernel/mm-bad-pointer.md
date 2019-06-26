---
title: Windows 内核宏
description: Windows 内核宏
ms.assetid: 91366400-3307-4F13-A839-50BA85B7F73E
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 46ab783d7acff09e72a76d4a6ca3a8bb726d0f78
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386005"
---
# <a name="windows-kernel-macros"></a>Windows 内核宏


以下列表包含 Windows 内核宏：


## <a name="addressandsizetospanpages"></a>**ADDRESS_AND_SIZE_TO_SPAN_PAGES**

在中定义：Wdm.h

**ADDRESS_AND_SIZE_TO_SPAN_PAGES**宏返回跨虚拟范围定义的虚拟地址和大小 （字节） 的转移请求的页面数。

_Va [in]_

**PVOID**

为范围的基础的虚拟地址的指针。

_[In] 的大小_

**ULONG**

以字节为单位的转移请求指定的大小。

**返回值**

**ULONG**

**ADDRESS_AND_SIZE_TO_SPAN_PAGES**返回的页面所跨的开始虚拟范围数_Va_。

驱动程序进行调用的 DMA 传输**ADDRESS_AND_SIZE_TO_SPAN_PAGES**以确定是否必须将传输请求拆分为一系列设备 DMA 操作。

驱动程序可以使用系统定义的常量 PAGE_SIZE 以确定是否要传输的字节数小于当前平台的虚拟内存页面大小。

调用方**ADDRESS_AND_SIZE_TO_SPAN_PAGES**可以在任何 IRQL 运行。 调用方必须确保指定的参数不会导致内存溢出。

从 Windows 2000 开始可用。


## <a name="byteoffset"></a>**BYTE_OFFSET**

在中定义：Wdm.h

**BYTE_OFFSET**宏采用虚拟地址，并返回该地址在页面内的字节偏移量。

_Va [in]_

**PVOID**

虚拟地址的指针。

**返回值**

**ULONG**

**BYTE_OFFSET**返回虚拟地址的偏移量的部分。

从 Windows 2000 开始可用。

IRQL:任何级别


## <a name="bytestopages"></a>**BYTES_TO_PAGES**

在中定义：Wdm.h

**BYTES_TO_PAGES**宏采用的大小以字节为单位的转移请求，并计算包含字节所需的页数。

_[In] 的大小_

**ULONG**

以字节为单位的转移请求指定的大小。

**返回值**

**ULONG**

**BYTES_TO_PAGES**返回包含指定的字节数所需的页数。

系统定义的常量 PAGE_SIZE 可以用于确定是否以字节为单位传输的具有给定的长度小于当前平台的虚拟内存页面大小。

从 Windows 2000 开始可用。

IRQL:任何级别


## <a name="containingrecord"></a>**CONTAINING_RECORD**

在中定义：Ntdef.h

**CONTAINING_RECORD**宏将返回给定类型的结构和包含结构中的字段的地址结构的实例的基址。

_[In] 解决_

**PCHAR**

指向类型的结构的实例中的字段的指针_类型_。

_[In] 类型_

**类型**

要返回其基址的结构类型的名称。

_[In] 字段_

**PCHAR**

指向字段的名称_地址_，其中包含在类型的结构_类型_。

**返回值**

**PCHAR**

返回的地址的结构包含基_字段_。

调用以确定其类型已知时调用方具有一个指向此类结构中的字段的结构的基址。 此宏可用于种访问已知类型的结构中的其他字段。

从 Windows 2000 开始可用。

IRQL:任何级别


## <a name="ioskipcurrentirpstacklocation"></a>**IoSkipCurrentIrpStackLocation**

在中定义：Wdm.h

\nThe **IoSkipCurrentIrpStackLocation**宏修改系统的[ **IO_STACK_LOCATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)数组指针，以便当当前驱动程序调用的下一步低驱动程序该驱动程序收到相同**IO_STACK_LOCATION**当前驱动程序收到的结构。

_Irp [中，out]_

**PIRP**

指向 IRP 的指针。

**返回值**

**VOID**

当您的驱动程序将 IRP 发送到下一步低驱动程序时，可以调用您的驱动程序**IoSkipCurrentIrpStackLocation**如果你不想要提供[ _IoCompletion_ ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程(其中的地址存储在驱动程序的[ **IO_STACK_LOCATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)结构)。 如果您调用**IoSkipCurrentIrpStackLocation**之前，调用[ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)下, 一步低驱动程序收到相同**IO_STACK_LOCATION**您的驱动程序接收。

如果你想要提供_IoCompletion_ IRP 的例程，应调用您的驱动程序[ **IoCopyCurrentIrpStackLocationToNext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)而不是**IoSkipCurrentIrpStackLocation**。 如果编写不正确的驱动程序，可以调用错误**IoSkipCurrentIrpStackLocation** ，并设置完成例程，该驱动程序可能会覆盖由其下方的驱动程序设置完成例程。

如果驱动程序具有挂起 IRP，不应调用该驱动程序**IoSkipCurrentIrpStackLocation**将 IRP 传递给下一个较低的驱动程序之前。 如果该驱动程序调用**IoSkipCurrentIrpStackLocation**上然后再将它传递到下一个较低的驱动程序挂起 IRP，SL_PENDING_RETURNED 仍中设置了标志**控制**I/O 堆栈位置的成员下一步的驱动程序。 下一步的驱动程序拥有的堆栈位置，并可能会对其进行修改，因为它可能无法清除挂起的标志。 这种情况下可能会导致操作系统发出的 bug 检查或处理 IRP 永远不会完成。

已挂起 IRP 的驱动程序应改为调用**IoCopyCurrentIrpStackLocationToNext**若要设置新的堆栈位置之前的下一个较低驱动程序调用**IoCallDriver**。

如果您的驱动程序调用**IoSkipCurrentIrpStackLocation**，请注意不要修改**IO_STACK_LOCATION**结构较低的驱动程序或系统的行为可能会无意中影响的方式对于该驱动程序。 示例包括修改**IO_STACK_LOCATION**结构的**参数**union 或调用[ **IoMarkIrpPending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)。

从 Windows 2000 开始可用。

IRQL:任何级别


## <a name="keinitializecallbackrecord"></a>**KeInitializeCallbackRecord**

在中定义：Wdm.h

**KeInitializeCallbackRecord**宏初始化[ **KBUGCHECK_CALLBACK_RECORD** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)或者[ **KBUGCHECK_REASON_CALLBACK_记录**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构。

_CallbackRecord [in]_

**PKBUGCHECK_CALLBACK_RECORD**

为指针**KBUGCHECK_CALLBACK_RECORD**或**KBUGCHECK_REASON_CALLBACK_RECORD**结构。 结构必须在常驻内存中，如非分页缓冲池。

**返回值**

**VOID**

在 Windows 2000 和更高版本的 Windows 中可用。

IRQL:任何级别


## <a name="mmbadpointer"></a>**MM_BAD_POINTER**

在中定义：Wdm.h

可以使用您的驱动程序**MM_BAD_POINTER**无效的指针值，这将分配到未初始化或不再有效的指针变量的宏。 尝试访问此无效的指针变量指向的内存位置将导致的 bug 检查。

在许多硬件平台上，解决 0 (通常表示为命名常量**NULL**) 是无效的地址，但驱动程序开发人员不应假定地址 0 是跨所有平台通用无效。 设置未初始化或无效地址 0 的变量可能始终保证，将检测到不适当的访问，通过这些指针的指针。

与之相反，值**MM_BAD_POINTER**保证是一个驱动程序在运行每个平台上无效的地址。

在平台上的地址上 0 是无效的地址，驱动程序访问的地址在 IRQL 0 < DISPATCH_LEVEL 会导致可由无意中捕获的异常 （访问冲突）`try/except`语句。 因此，驱动程序的异常处理代码可能会屏蔽无效的访问，并阻止它在调试期间检测到。 但是的访问**MM_BAD_POINTER**保证地址会导致错误检查，不能被屏蔽的异常处理程序。

下面的代码示例演示如何将值分配**MM_BAD_POINTER**到名为的指针变量`ptr`。 Ntdef.h 标头文件定义要指向的指针的 PUCHAR 类型`unsigned char`。

`PUCHAR ptr = (PUCHAR)MM_BAD_POINTER; // Now _ptr is guaranteed to fault._`

之后`ptr`设置为**MM_BAD_POINTER**，指向尝试访问的内存位置`ptr`将导致的 bug 检查。

事实上， **MM_BAD_POINTER**是无效的地址的整个页面的基址。 因此，任何访问权限的范围中的地址**MM_BAD_POINTER**到 (**MM_BAD_POINTER** + **PAGE_SIZE** -1) 将导致的 bug 检查。

从 Windows 8.1 **MM_BAD_POINTER** wdm.h 中的标头文件中定义宏。 但是，使用此宏定义的驱动程序代码可以运行在以前版本的 Windows 与 Windows Vista 一起启动。

从 Windows Vista 开始[ **MmBadPointer** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm64bitphysicaladdress)全局变量是可用作指向保证是无效的地址的指针值的指针。 但是，从 Windows 8.1，将开始**MmBadPointer**已被弃用，并应更新驱动程序以使用**MM_BAD_POINTER**宏相反。

从 Windows 8.1\ 开始可用。 与以前版本的 Windows 启动 Windows Vista 兼容。 _


## <a name="mmgetmdlbytecount"></a>**MmGetMdlByteCount**

在中定义：Wdm.h

**MmGetMdlByteCount**宏返回的长度，以字节为单位指定 MDL 所描述的缓冲区。

_[In] Mdl_

**PMDL**

一个指向[ **MDL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_mdl)描述的物理内存中的虚拟内存缓冲区布局的结构。 有关详细信息，请参阅[使用 MDLs](using-mdls.md)。

**返回值**

**ULONG**

## <a name="mmgetmdlbytecount-returns-the-length-in-bytes-of-the-buffer-described-by-mdl"></a>**MmGetMdlByteCount**返回的长度，以字节为单位的所述的缓冲区_Mdl_。

调用方**MmGetMdlByteCount**可以在任何 IRQL 运行。 通常情况下，调用方则正在运行的 IRQL < = DISPATCH_LEVEL。

从 Windows 2000 开始可用。

IRQL:任何级别


## <a name="mmgetmdlbyteoffset"></a>**MmGetMdlByteOffset**

在中定义：Wdm.h

**MmGetMdlByteOffset**宏将返回由给定 MDL 所述的缓冲区的初始页中的字节偏移量。

_[In] Mdl_

**PMDL**

指向 MDL 指针。

**返回值**

**ULONG**

## <a name="mmgetmdlbyteoffset-returns-the-offset-in-bytes"></a>**MmGetMdlByteOffset**返回以字节为单位的偏移量。

调用方**MmGetMdlByteOffset**可以在任何 IRQL 运行。 通常情况下，调用方则正在运行的 IRQL < = DISPATCH_LEVEL。

在 Windows 2000 和更高版本的 Windows 中可用。

IRQL:任何级别


## <a name="mmgetmdlpfnarray"></a>**MmGetMdlPfnArray**

在中定义：Wdm.h

**MmGetMdlPfnArray**宏返回一个指针与内存描述符列表 (MDL) 相关联的物理页数字数组的开头。

_[In] Mdl_

**PMDL**

指向 MDL 的指针。

**返回值**

**PPFN_NUMBER**

指向与 MDL 相关联的物理页数字数组的开头的指针。 数组中的项的数量**ADDRESS_AND_SIZE_TO_SPAN_PAGES**(**MmGetMdlVirtualAddress**(_Mdl_)， **MmGetMdlByteCount**(_Mdl_))。 每个数组元素是类型 PFN_NUMBER 中, 定义的一个整数值：Wdm.h 中，如下所示：

`cpp typedef ULONG PFN_NUMBER, *PPFN_NUMBER;`

**请注意**更改数组的内容可能会导致难以进行诊断的细微系统问题。 我们建议您不要读取或更改此数组的内容。

对于可分页内存，数组的内容是仅对使用锁定的缓冲区的有效[ **MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)。 对于非分页池，该数组的内容是仅对使用更新 MDL 有效[ **MmBuildMdlForNonPagedPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmbuildmdlfornonpagedpool)， [ **MmAllocatePagesForMdlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatepagesformdlex)，或[ **MmAllocatePagesForMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatepagesformdl)。

有关 MDLs 详细信息，请参阅[使用 MDLs](using-mdls.md)。

从 Windows 2000 开始可用。

IRQL:任何级别


## <a name="mmgetmdlvirtualaddress"></a>**MmGetMdlVirtualAddress**

在中定义：Wdm.h

**MmGetMdlVirtualAddress**宏返回 MDL 所描述的缓冲区的基虚拟地址。

_[In] Mdl_

**PMDL**

指向 MDL 描述要为其返回初始虚拟地址的缓冲区的指针。

**返回值**

**PVOID**

## <a name="mmgetmdlvirtualaddress-returns-the-starting-virtual-address-of-the-mdl"></a>**MmGetMdlVirtualAddress**返回 MDL 的起始虚拟地址。

**MmGetMdlVirtualAddress**返回并不一定是当前线程上下文中有效的虚拟地址。 较低级别的驱动程序不应尝试使用返回的虚拟地址来访问内存，尤其是用户内存空间。

返回到物理地址条目 MDL 中的索引使用的地址，可以输入到[ **MapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pmap_transfer)。

调用方**MmGetMdlVirtualAddress**可以在任何 IRQL 运行。 通常情况下，调用方运行在 IRQL = DISPATCH_LEVEL，因为此例程通常调用以获得_CurrentVa_参数**MapTransfer**。

在 Windows 2000 和更高版本的 Windows 中可用。

IRQL:任何级别


## <a name="mmgetsystemaddressformdlsafe"></a>**MmGetSystemAddressForMdlSafe**

在中定义：Wdm.h

**MmGetSystemAddressForMdlSafe**宏将返回指定的 MDL 描述的缓冲区的非分页的系统空间虚拟地址。

_[In] Mdl_

**PMDL**

为其对应的基虚拟地址是要映射的缓冲区的指针。

_[In] 优先级_

## <a name="mmpagepriority"></a>**Mm_PAGE_PRIORITY**

指定**MM_PAGE_PRIORITY**值，该值指示在低可用 PTE 情况下成功的重要性。 指定的优先级值为**LowPagePriority**， **NormalPagePriority**，或**HighPagePriority**。 从 Windows 8 开始，指定的优先级值可以是与按位且**MdlMappingNoWrite**或**MdlMappingNoExecute**标志。

*   **LowPagePriority**指示，是否系统资源上相当低，则映射请求可能会失败。 这种情况的示例是非关键的网络连接，该驱动程序可以处理映射失败。

*   **NormalPagePriority**指示，是否系统资源过低，则映射请求可能会失败。 这种情况下的一个示例是一个非关键的本地文件系统请求。

*   **HighPagePriority**指示映射请求必须不失败，除非系统完全的资源不足。 这种情况的示例是一个驱动程序中的分页文件路径。

*   **MdlMappingNoWrite**指示映射的物理页将配置为禁止写入 （只读） 内存。 从 Windows 8 开始，此标志位可以是与按位且**MM_PAGE_PRIORITY**值，以指定在其中禁用写入内存。

*   **MdlMappingNoExecute**指示要将配置为无执行内存映射的物理页。 从 Windows 8 开始，此标志位可以是与按位且**MM_PAGE_PRIORITY**值，以指定在哪些指令中禁用执行的内存。 作为最佳做法是，编写针对 Windows 8 和更高版本的 Windows 驱动程序应始终指定无执行内存除非显式需要可执行文件的内存。

*   **返回值**

    **PVOID**

    **MmGetSystemAddressForMdlSafe**返回映射指定的 MDL 描述的物理页的基本系统空间虚拟地址。 如果页面未已映射到系统地址空间并尝试将其映射失败， **NULL**返回。

如果它们不已映射到系统地址空间，此例程会映射到系统地址空间由指定 MDL 描述的物理页。

编程输入/输出 (PIO) 设备的驱动程序调用该例程来映射用户模式缓冲区，用于描述在 MDL **Irp-> MdlAddress**和该列已映射到用户模式虚拟地址范围，系统地址中的范围空间。

在进入到此例程时，指定的 MDL 必须描述已锁定的物理页。 可以使用生成锁定的 MDL [ **MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)， [ **MmBuildMdlForNonPagedPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmbuildmdlfornonpagedpool)， [ **IoBuildPartialMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildpartialmdl)，或[ **MmAllocatePagesForMdlEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatepagesformdlex)例程。

返回系统的地址空间映射，当**MmGetSystemAddressForMdlSafe**是不再需要它必须释放。 发布映射所需的步骤取决于 MDL 的构建方式。 以下是四种可能情况：

*   如果通过调用生成 MDL **MmProbeAndLockPages**例程，它不需要显式释放的系统地址空间映射。 相反，调用[ **MmUnlockPages** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunlockpages)例程释放映射，如果其中一个已分配。

*   如果通过调用生成 MDL **MmBuildMdlForNonPagedPool**例程， **MmGetSystemAddressForMdlSafe**重复使用而不是创建一个新的现有系统地址空间映射。 在这种情况下，清除操作 （即，解除锁定和取消映射不是有必要）。

*   如果通过调用生成 MDL **IoBuildPartialMdl**例程，该驱动程序必须调用[ **MmPrepareMdlForReuse** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)例程或[ **IoFreeMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreemdl)例程来释放系统地址空间映射。

*   如果通过调用生成 MDL **MmAllocatePagesForMdlEx**例程，该驱动程序必须调用**MmUnmapLockedPages**例程来释放系统地址空间映射。 如果**MmGetSystemAddressForMdlSafe**后续 MDL 称为不止一次**MmGetSystemAddressForMdlSafe**调用只返回第一次调用创建的映射。 调用一次**MmUnmapLockedPages**足以发布此映射。

从 Windows 7 和 Windows Server 2008 R2 开始，它不需要显式调用**MmUnmapLockedPages**为已通过 MDL **MmAllocatePagesForMdlEx**。 相反，调用[ **MmFreePagesFromMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmfreepagesfrommdl)例程释放系统地址空间映射，如果其中一个已分配。

若要创建新的系统地址空间映射**MmGetSystemAddressForMdlSafe**调用**MmMapLockedPagesSpecifyCache**与_CacheType_参数设置为**MmCached**。 而不需要缓存类型的驱动程序**MmCached**应调用**MmMapLockedPagesSpecifyCache**而不是调用直接**MmGetSystemAddressForMdlSafe**。 有关详细信息_CacheType_参数，请参阅[ **MmMapLockedPagesSpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpagesspecifycache)。

在调用**MmMapLockedPagesSpecifyCache**，仅当通过 MDL 所述的页面还没有与之关联的缓存类型使用指定的缓存类型。 但是，在几乎所有情况下，页面已具有关联的缓存类型，并且此缓存类型由新的映射。 此规则的例外是由分配的页**MmAllocatePagesForMdl**，该缓存类型设置为**MmCached**原始页面的缓存类型无关。

一次只有一个线程可以安全地调用**MmGetSystemAddressForMdlSafe**为特定 MDL 由于此例程假定调用线程拥有 MDL。 但是， **MmGetSystemAddressForMdlSafe**可以调用一次相同 MDL 或者通过使来自同一个线程的所有调用，则调用为从多个线程，通过显式同步调用。

如果驱动程序必须将请求拆分为较小的请求，该驱动程序可以分配其他 MDLs 或驱动程序可以使用**IoBuildPartialMdl**例程。

返回的基址 MDL 中具有相同的偏移量作为虚拟地址。

Windows 98 不支持**MmGetSystemAddressForMdlSafe**。 使用[ **MmGetSystemAddressForMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmgetsystemaddressformdl)相反。

因为此宏将调用[ **MmMapLockedPagesSpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpagesspecifycache)，使用它可能需要将链接到 NtosKrnl.lib。

从 Windows 2000 开始可用。

IRQL <= DISPATCH_LEVEL


## <a name="mminitializemdl"></a>**MmInitializeMdl**

在中定义：Wdm.h

**MmInitializeMdl**宏初始化 MDL 的标头。

_MemoryDescriptorList [in]_

**PMDL**

指向要初始化为 MDL 的缓冲区的指针。 有关详细信息，请参阅以下部分。

_BaseVa [in]_

**PVOID**

指向缓冲区的基虚拟地址的指针。

_[In] 的长度_

**SIZE_T**

以字节为单位，用于描述由 MDL 缓冲区的指定的长度。 此例程支持的最大缓冲区长度 MAXULONG 个字节。

**返回值**

**VOID**

缓冲区的_MemoryDescriptorList_点必须在非分页内存中分配。 以字节为单位，此缓冲区的大小必须至少**sizeof**(MDL) + **sizeof**(PFN_NUMBER)**ADDRESS_AND_SIZE_TO_SPAN_PAGES**(_BaseVa_，_长度_)。

在 Windows 2000 和更高版本的 Windows 中可用。

IRQL <= DISPATCH_LEVEL


## <a name="mmpreparemdlforreuse"></a>**MmPrepareMdlForReuse**

在中定义：Wdm.h

**MmPrepareMdlForReuse**宏释放，以便可以重用 MDL 部分 MDL 与相关联的资源。

_[In] Mdl_

**PMDL**

指向要准备以供重复使用部分 MDL 的指针。

**返回值**

**VOID**

通过重复使用的相同的已分配的 MDL 驱动程序使用此宏_TargetMdl_对的调用中的参数[ **IoBuildPartialMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildpartialmdl)例程。 如果在调用**MmPrepareMdlForReuse**，指定部分 MDL 具有关联的映射到系统地址空间**MmPrepareMdlForReuse**释放映射，以便可以重用 MDL。

**MmPrepareMdlForReuse**接受仅由生成的分部 MDLs **IoBuildPartialMdl**。 如果**MmPrepareMdlForReuse**接收映射到的系统地址空间，但不由生成 MDL **IoBuildPartialMdl**， **MmPrepareMdlForReuse**不会释放映射，并在选中版本中，则引发断言失败。

有关部分 MDLs 详细信息，请参阅[使用 MDLs](using-mdls.md)。

在 Windows 2000 和更高版本的 Windows 中可用。

IRQL <= DISPATCH_LEVEL


## <a name="pagealign"></a>**PAGE_ALIGN**

在中定义：Wdm.h

**PAGE_ALIGN**宏将返回给定的虚拟地址的对齐页上的虚拟地址。

_Va [in]_

**PVOID**

虚拟地址的指针。

**返回值**

**PVOID**

## <a name="pagealign-returns-a-pointer-to-the-page-aligned-virtual-address"></a>**PAGE_ALIGN**返回指向页面对齐虚拟地址的指针。

从 Windows 2000 开始可用。

IRQL:任何级别


## <a name="pagedcode"></a>**PAGED_CODE**

在中定义：Wdm.h

**PAGED_CODE**宏可确保调用线程在够低，以允许分页的 IRQL 运行。

**返回值**

**VOID**

如果 IRQL > APC_LEVEL， **PAGED_CODE** assert 宏会导致的系统。

此宏调用应在每个驱动程序例程的包含可分页的代码或访问的可分页的代码开始处。

**PAGED_CODE**宏检查 IRQL 只能在驱动程序代码的执行宏的点。 如果该代码随后会 IRQL，宏将不会检测此更改。 驱动程序开发人员应使用[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)并[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)用于检测何时 IRQL 驱动程序例程的执行过程中引发不正确。

**PAGED_CODE**宏仅在选中的版本中的工作方式。

从 Windows 2000 开始可用。


## <a name="pagedcodelocked"></a>**PAGED_CODE_LOCKED**

在中定义：Wdm.h

**PAGED_CODE_LOCKED**宏断言，当前正在运行的代码部分是可分页，必须已被锁定到内存之前运行。

**返回值**

**VOID**

可分页的代码必须遵循特定的限制 (例如 IRQL < = APC_LEVEL)，除非它已锁定到位。 必须锁定到位，才能正常工作的可分页例程应开始通过调用**PAGED_CODE_LOCKED**。

锁定到位的代码部分的详细信息，请参阅[锁定可分页代码或数据](locking-pageable-code-or-data.md)。


## <a name="posetdevicebusy"></a>**PoSetDeviceBusy**

在中定义：Wdm.h

**PoSetDeviceBusy**宏通知[电源管理器](power-manager.md)与设备关联_IdlePointer_正忙。

_IdlePointer [中，out]_

**PULONG**

指定一个非**NULL**空闲之前通过返回的指针[ **PoRegisterDeviceForIdleDetection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-poregisterdeviceforidledetection)。 请注意， **PoRegisterDeviceForIdleDetection**可能会返回**NULL**指针。 调用方**PoSetDeviceBusy**必须验证指针是否非**NULL**之前将其传递给**PoSetDeviceBusy**。

**返回值**

**VOID**

**请注意** [ **PoSetDeviceBusyEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-posetdevicebusyex)例程是直接替代**PoSetDeviceBusy**宏。 如果要为 Windows Vista Service Pack 1 (SP1) 和更高版本的 Windows 编写新的驱动程序代码，调用**PoSetDeviceBusyEx**而不是**PoSetDeviceBusy**。

驱动程序将使用**PoSetDeviceBusy**连同**PoRegisterDeviceForIdleDetection**启用系统空闲检测其设备。 如果空闲检测是否已注册的设备进入空闲状态，电源管理器将发送[ **IRP_MN_SET_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)请求将在请求进入睡眠状态中的设备。

**PoSetDeviceBusy**报告设备繁忙状态，以便电源管理器可以重新启动其空闲的倒计时。 如果设备未接通电源， **PoSetDeviceBusy**不会更改其状态。 也就是说，它不会导致系统发送电源的请求。

驱动程序应调用**PoSetDeviceBusy**对每个 I/O 请求。

从 Windows 2000 开始可用。

IRQL:任何级别


## <a name="psgetcurrentprocess"></a>**PsGetCurrentProcess**

在中定义：Ntddk.h

返回一个指向当前线程的过程。

**返回值**

指向一个不透明的进程对象的指针。



从 Windows 2000 开始可用。

IRQL:任何级别


## <a name="readregisterbufferulong64"></a>**READ_REGISTER_BUFFER_ULONG64**

在中定义：Wdm.h

**READ_REGISTER_BUFFER_ULONG64**宏到缓冲区读取大量 ULONG64 值从指定的寄存器的地址。

_[In] 注册_

**PULONG64**

注册，它必须是内存空间中的映射的范围的指针。

_[Out 一个] 缓冲区_

**PULONG64**

指向 ULONG64 值的数组读入的缓冲区。

_Count [in]_

**ULONG**

指定要读取到缓冲区的 ULONG64 值数。

**返回值**

**VOID**

大小_缓冲区_缓冲区必须足够大以至少包含指定的数量的 ULONG64 值。

调用方**READ_REGISTER_BUFFER_ULONG64**宏可以在运行任何 irql，因此假定_缓冲区_缓冲区是常驻并_注册_寄存器是常驻，映射设备内存。

仅在 64 位版本的 Windows 中可用。

IRQL:任何级别


## <a name="readregisterulong64"></a>**READ_REGISTER_ULONG64**

在中定义：Wdm.h

**READ_REGISTER_ULONG64**宏读取 ULONG64 值从指定的寄存器的地址。

_易失性 * 注册 [in]_

**ULONG64**

指向注册地址，它必须是内存空间中映射的范围。

**返回值**

**ULONG64**

**READ_REGISTER_ULONG64**返回从指定的寄存器地址读取 ULONG64 值。

调用方**READ_REGISTER_ULONG64**宏可以在任何 IRQL 运行假设_注册_地址是常驻、 映射设备内存。

仅在 64 位版本的 Windows 中可用。

IRQL:任何级别


## <a name="roundtopages"></a>**ROUND_TO_PAGES**

在中定义：Wdm.h

**ROUND_TO_PAGES**宏将以字节为单位的大小，并将其舍入到下一个整页。

_[In] 的大小_

**ULONG_PTR**

指定的大小以字节为单位来向上舍入到的页面多个。

**返回值**

**ULONG_PTR**

**ROUND_TO_PAGES**返回输入的大小向上舍入到当前平台的虚拟内存页面大小的倍数。

调用方**ROUND_TO_PAGES**可以在任何 IRQL 运行。 调用方必须确保所提供的参数不会导致内存溢出。

IRQL:任何级别


## <a name="rtlequalluid"></a>**RtlEqualLuid**

在中定义：Wdm.h

**返回值**

从 Windows 2000 开始可用。

IRQL:任何级别


## <a name="rtlinitemptyansistring"></a>**RtlInitEmptyAnsiString**

在中定义：Wdm.h

**RtlInitEmptyAnsiString**宏初始化空计数的 ANSI 字符串。

_DestinationString [out]_

**PANSI_STRING**

指向[ **ANSI_STRING** ](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_string)结构进行初始化。

_[In] 缓冲_

**PCHAR**

指向调用方分配的缓冲区，用于将包含一个 WCHAR 字符串。

_[In] BufferSize_

**USHORT**

缓冲区的长度，以字节为单位，该_缓冲区_指向。

**返回值**

**VOID**

结构的成员的_DestinationString_参数指向进行初始化，如下所示。

*   **长度**。 为零。

*   **MaximumLength**。 _BufferSize_。

*   **缓冲区**。 _SourceString_。

若要初始化非空计数 Unicode 字符串，调用[ **RtlInitAnsiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlinitansistring)。

在 Microsoft Windows XP 和更高版本的 Windows 中可用。

IRQL:任何级别


## <a name="rtlinitemptyunicodestring"></a>**RtlInitEmptyUnicodeString**

在中定义：Wdm.h

**RtlInitEmptyUnicodeString**宏会初始化一个空计数 Unicode 字符串。

_DestinationString [out]_

**PUNICODE_STRING**

指向[ **UNICODE_STRING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/ns-wudfwdm-_unicode_string)结构进行初始化。

_[In] 缓冲_

**PWCHAR**

指向调用方分配的缓冲区，用于将包含一个 WCHAR 字符串。

_[In] BufferSize_

**USHORT**

缓冲区的长度，以字节为单位，该_缓冲区_指向。

**返回值**

**VOID**

结构的成员的_DestinationString_参数指向也经过初始化，如下所示。

*   **长度**。 为零。

*   **MaximumLength**。 _BufferSize_。

*   **缓冲区**。 _SourceString_。

若要初始化非空计数 Unicode 字符串，调用[ **RtlInitUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlinitunicodestring)。

从开始，提供与 Windows XP。

IRQL:任何级别


## <a name="rtliszeroluid"></a>**RtlIsZeroLuid**

在中定义：Ntddk.h

**RtlIsZeroLuid**宏确定是否指定的 LUID 为零的 LUID。

_L1 [in]_

**PLUID**

指定[ **LUID** ](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_luid)检查。

**返回值**

**BOOLEAN**

**RtlIsZeroLuid**将返回**TRUE**如果_L1_为零，并返回**FALSE**否则为。

IRQL:任何级别


## <a name="rtlretrieveulong"></a>**RtlRetrieveUlong**

在中定义：Wdm.h

**RtlRetrieveUlong**宏检索来自源地址，避免对齐错误 ULONG 值。 目标地址被假定对齐。

_DestinationAddress [out]_

**PULONG**

指向要在其中存储 ULONG 值的 ULONG 对齐位置。

_SourceAddress [in]_

**PULONG**

要从其中检索 ULONG 值的位置的指针。

**返回值**

**VOID**

调用方**RtlRetrieveUlong**如果给定的地址位于非分页缓冲池可以在任何 IRQL 运行。 否则，调用方必须运行在 IRQL < = APC_LEVEL。

在 Windows 2000 和更高版本的 Windows 中可用。


## <a name="rtlretrieveushort"></a>**RtlRetrieveUshort**

在中定义：Wdm.h

**RtlRetrieveUshort**宏检索来自源地址，避免对齐错误 USHORT 值。

_DestinationAddress [out]_

**PUSHORT**

指向要在其中存储值的 USHORT 对齐位置。

_SourceAddress [in]_

**PUSHORT**

要从中检索值的位置的指针。

**返回值**

**VOID**

调用方**RtlRetrieveUshort**如果给定的地址位于非分页缓冲池可以在任何 IRQL 运行。 否则，调用方必须运行在 IRQL < = APC_LEVEL。

在 Windows 2000 和更高版本的 Windows 中可用。

IRQL:任何级别


## <a name="rtlstoreulong"></a>**RtlStoreUlong**

在中定义：Wdm.h

**RtlStoreUlong**宏存储在特定地址，避免对齐错误 ULONG 值。

_Address [out]_

**PULONG**

指向要在其中存储指定的 ULONG 值的位置的指针。

_[In] 值_

**ULONG**

指定要存储的 ULONG 值。

**返回值**

**VOID**

如果调用方可以运行的任何 irql_地址_指向非分页缓冲池。 否则，调用方必须运行在 IRQL < = APC_LEVEL。

在 Windows 2000 和更高版本的 Windows 中可用。

IRQL:任何级别


## <a name="rtlstoreulonglong"></a>**RtlStoreUlonglong**

在中定义：Wdm.h

**RtlStoreUlonglong**宏存储在指定的内存地址，避免内存对齐错误指定的 ULONGLONG 值。

_Address [out]_

**PULONGLONG**

指向要在其中存储指定的 ULONGLONG 值的位置的指针。

_[In] 值_

**ULONGLONG**

要存储的 ULONGLONG 值。

**返回值**

**VOID**

**RtlStoreUlonglong**可避免内存对齐错误。 如果指定的地址_地址_ULONGLONG 的存储要求未对齐**RtlStoreUlonglong**存储的字节_值_开始的内存位置位置 (PUCHAR)_地址_。

**RtlStoreUlonglong**如果运行的任何 irql_地址_指向非分页池; 否则，它必须运行在 IRQL < = APC_LEVEL。

从 Windows 2000 开始可用。

IRQL:任何级别


## <a name="rtlstoreulongptr"></a>**RtlStoreUlongPtr**

在中定义：Wdm.h

**RtlStoreUlongPtr**宏存储在指定的内存位置，避免内存对齐错误指定的 ULONG_PTR 值。

_Address [out]_

**PULONG_PTR**

指向要在其中存储 ULONG_PTR 值的位置的指针。

_[In] 值_

**ULONG_PTR**

指定要存储的 ULONG_PTR 值。

**返回值**

**VOID**

**RtlStoreUlongPtr**可避免内存对齐错误。 如果的值_地址_ULONG_PTR 的存储要求未对齐**RtlStoreUlongPtr**存储的字节_值_开始的内存位置 （PUCHAR)_地址_。

**RtlStoreUlongPtr**如果运行的任何 irql_地址_指向非分页池; 否则它必须运行在 IRQL < = APC_LEVEL。

在 Windows 2000 和更高版本的 Windows 中可用。

IRQL:任何级别


## <a name="rtlstoreushort"></a>**RtlStoreUshort**

在中定义：Wdm.h

**RtlStoreUshort**宏存储在特定地址，避免对齐错误 USHORT 值。

_Address [out]_

**PUSHORT**

指向要在其中存储指定的 USHORT 值的位置的指针。

_[In] 值_

**USHORT**

指定要存储的 USHORT 值。

**返回值**

**VOID**

如果调用方可以运行的任何 irql_地址_指向非分页缓冲池。 否则，调用方必须运行在 IRQL < = APC_LEVEL。

在 Windows 2000 和更高版本的 Windows 中可用。

IRQL:任何级别


## <a name="writeregisterbufferulong64"></a>**WRITE_REGISTER_BUFFER_ULONG64**

在中定义：Wdm.h

**WRITE_REGISTER_BUFFER_ULONG64**宏指定注册从缓冲区写入大量 ULONG64 值。

_[In] 注册_

**PULONG64**

注册，它必须是内存空间中的映射的范围的指针。

_[In] 缓冲_

**PULONG64**

指向要写入到 ULONG64 值的数组的缓冲区的指针。

_Count [in]_

**ULONG**

指定 ULONG64 值写入到寄存器的数目。

**返回值**

**VOID**

大小_缓冲区_缓冲区必须足够大以至少包含指定的数量的 ULONG64 值。

调用方**WRITE_REGISTER_BUFFER_ULONG64**宏可以在运行任何 irql，因此假定_缓冲区_缓冲区是常驻并_注册_寄存器是常驻，映射设备内存。

仅在 64 位版本的 Windows 中可用。

IRQL:任何级别


## <a name="writeregisterulong64"></a>**WRITE_REGISTER_ULONG64**

在中定义：Wdm.h

**WRITE_REGISTER_ULONG64**宏将 ULONG64 值写入到指定的地址。

_易失性 * 注册 [in]_

**ULONG64**

注册，它必须是内存空间中的映射的范围的指针。

_[In] 值_

**ULONG64**

指定要写入到寄存器 ULONG64 值。

**返回值**

**VOID**

调用方**WRITE_REGISTER_ULONG64**宏可以在任何 IRQL 运行假设_注册_寄存器是常驻、 映射设备内存。

仅在 64 位版本的 Windows 中可用。

IRQL:任何级别


## <a name="zwcurrentprocess"></a>**ZwCurrentProcess**

在中定义：Wdm.h

**ZwCurrentProcess**宏返回的句柄当前进程。

**返回值**

**HANDLE**

**ZwCurrentProcess**返回一个特殊的句柄值，表示当前进程。

返回的值不是 true 的句柄，但它是始终表示当前进程的特殊值。

**NtCurrentProcess**并**ZwCurrentProcess**相同的 Windows 本机系统服务例程的两个版本。 **NtCurrentProcess** Windows 内核中的例程不是直接访问的内核模式驱动程序。 但是，内核模式驱动程序可以访问此例程间接通过调用**ZwCurrentProcess**。

从内核模式驱动程序调用**Nt_Xxx_** 并**Zw_Xxx_** 版本的 Windows 本机系统服务例程在它们处理和解释输入的参数的方式行为可能有所不同。 有关详细信息之间的关系**Nt_Xxx_** 和**Zw_Xxx_** 版本的例程，请参阅[使用 Nt 和 Zw 版本的本机系统服务例程](using-nt-and-zw-versions-of-the-native-system-services-routines.md).

所有受支持操作系统。

IRQL:任何级别


## <a name="zwcurrentthread"></a>**ZwCurrentThread**

在中定义：Wdm.h

**ZwCurrentThread**宏返回的句柄当前线程。

**返回值**

**HANDLE**

**ZwCurrentThread**返回一个特殊的句柄值，表示当前线程。

返回的值不是 true 的句柄，但它是始终表示当前线程的特殊值。

**NtCurrentThread**并**ZwCurrentThread**相同的 Windows 本机系统服务例程的两个版本。 **NtCurrentThread** Windows 内核中的例程不是直接访问的内核模式驱动程序。 但是，内核模式驱动程序可以访问此例程间接通过调用**ZwCurrentThread**例程。

从内核模式驱动程序调用**Nt_Xxx_** 并**Zw_Xxx_** 版本的 Windows 本机系统服务例程在它们处理和解释输入的参数的方式行为可能有所不同。 有关详细信息之间的关系**Nt_Xxx_** 和**Zw_Xxx_** 版本的例程，请参阅[使用 Nt 和 Zw 版本的本机系统服务例程](using-nt-and-zw-versions-of-the-native-system-services-routines.md).

所有受支持操作系统。

IRQL:任何级别










