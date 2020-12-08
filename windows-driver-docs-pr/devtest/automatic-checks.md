---
title: 自动检查
description: 自动检查
keywords:
- 自动检查 WDK 驱动程序验证程序
- IRQL 监视 WDK 驱动程序验证程序
- 堆栈切换 WDK 驱动程序验证程序
- 免费池计时器，WDK 驱动程序验证程序
- 清理检查 WDK 驱动程序验证程序
- 切换堆栈 WDK 驱动程序验证程序
- 驱动程序卸载 WDK 驱动程序验证程序
- 驱动程序验证程序选项，监视 IRQL 和内存例程
- 驱动程序验证程序选项，监视堆栈切换
- 驱动程序验证程序选项，检查驱动程序卸载
- 驱动程序验证程序选项，监视驱动程序调度例程
- 驱动程序验证程序选项，监视内存调度列表 (MDL) 使用情况
ms.date: 10/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff126a375263e7c6a411b7dbc81cee10c696350a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784085"
---
# <a name="automatic-checks"></a>自动检查


## <span id="ddk_automatic_checks_tools"></span><span id="DDK_AUTOMATIC_CHECKS_TOOLS"></span>


驱动程序验证程序在验证一个或多个驱动程序时执行以下检查。 不能激活或停用这些检查。 从 Windows 10 版本1709开始，这些自动检查已移动到相关的 [标准标志](verifier-command-line.md)。 因此，启用带有标准标志的驱动程序验证程序的用户应该看不到所应用的检查的缩减。

### <a name="span-idddk_monitoring_irql_and_memory_routines_toolsspanspan-idddk_monitoring_irql_and_memory_routines_toolsspanmonitoring-irql-and-memory-routines"></a><span id="ddk_monitoring_irql_and_memory_routines_tools"></span><span id="DDK_MONITORING_IRQL_AND_MEMORY_ROUTINES_TOOLS"></span>监视 IRQL 和内存例程

驱动程序验证器监视所选的驱动程序以了解以下禁止的操作：

-   通过调用 **KeLowerIrql** 引发 IRQL

-   通过调用 **KeRaiseIrql** 降低 IRQL

-   请求大小为零的内存分配

-   分配或释放具有 IRQL &gt; APC 级别的页面缓冲池 \_

-   分配或释放 IRQL &gt; 调度级别的非分页池 \_

-   正在尝试释放以前分配中未返回的地址

-   尝试释放已释放的地址

-   获取或释放具有 IRQL &gt; APC 级别的快速 \_ mutex

-   获取或释放 IRQL 不等于调度级别的自旋锁 \_

-   双释放旋转锁。

-   标记分配请求必须 \_ 成功。 不允许此类请求。

如果驱动程序验证程序不处于活动状态，则在所有情况下，这些冲突可能不会导致立即发生系统崩溃。 驱动程序验证程序监视驱动程序的行为，并在发生任何这些冲突时发出 bug 检查0xC4。 有关错误检查参数的列表，请参阅 [**Bug 检查 0xC4**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (驱动程序 \_ 验证器 \_ 检测到 \_ 冲突) 。

### <a name="span-idddk_monitoring_stack_switching_toolsspanspan-idddk_monitoring_stack_switching_toolsspanmonitoring-stack-switching"></a><span id="ddk_monitoring_stack_switching_tools"></span><span id="DDK_MONITORING_STACK_SWITCHING_TOOLS"></span>监视堆栈切换

驱动程序验证器监视正在验证的驱动程序的堆栈使用情况。 如果驱动程序切换其堆栈，并且新堆栈既不是线程堆栈也不是 DPC 堆栈，则会发出 bug 检查。  (这将是0xC4 的第一个参数等于0x90 的 bug 检查。 ) 由 **知识库** 调试器命令显示的堆栈通常会显示执行此操作的驱动程序。

### <a name="span-idddk_checking_on_driver_unload_toolsspanspan-idddk_checking_on_driver_unload_toolsspanchecking-on-driver-unload"></a><span id="ddk_checking_on_driver_unload_tools"></span><span id="DDK_CHECKING_ON_DRIVER_UNLOAD_TOOLS"></span>正在卸载驱动程序

在要进行验证的驱动程序卸载之后，驱动程序验证器会执行多个检查以确保驱动程序已清理。

具体而言，驱动程序验证程序将查找：

-   删除的计时器

-   ) Dpc (挂起的延迟过程调用

-   未删除的后备链表列表

-   未删除的工作线程

-   删除的队列

-   其他类似资源

此类问题可能会导致系统 bug 检查在驱动程序卸载后发出一段时间，并且可能难以确定这些错误检查的原因。 当驱动程序验证程序处于活动状态时，此类冲突会导致 bug 检查0xC7 在卸载驱动程序后立即发出。 有关错误检查参数的列表，请参阅 [**Bug 检查 0xC7**](../debugger/bug-check-0xc7--timer-or-dpc-invalid.md) (计时器 \_ 或 \_ DPC \_ 无效的) 。


### <a name="span-idmonitoring__memory_descriptor_list__mdl__usagespanspan-idmonitoring__memory_descriptor_list__mdl__usagespanspan-idmonitoring__memory_descriptor_list__mdl__usagespanmonitoring-memory-descriptor-list-mdl-usage"></a><span id="Monitoring__Memory_Descriptor_List__MDL__Usage"></span><span id="monitoring__memory_descriptor_list__mdl__usage"></span><span id="MONITORING__MEMORY_DESCRIPTOR_LIST__MDL__USAGE"></span> (MDL) 使用情况监视内存描述符列表

在 Windows Vista 中，驱动程序验证器还会监视选定的驱动程序是否有以下禁止的操作：

-   在没有相应标志的 MDL 上调用 [**MmProbeAndLockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages) 或 MmProbeAndLockProcessPages。 例如，对使用 [**MmBuildMdlForNonPagedPool**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool)创建的 MDL 调用 **MmProbeAndLockPages** 是不正确的。

-   在没有相应标志的 MDL 上调用 [**MmMapLockedPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages) 。 例如，对于已映射到系统地址或未锁定的 MDL 的 MDL，调用 **MmMapLockedPages** 是不正确的。

-   对使用 [**IoBuildPartialMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl)创建的部分 MDL 调用 [**MmUnlockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)或 [**MmUnmapLockedPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmaplockedpages) 。

-   对未映射到系统地址的 MDL 调用 **MmUnmapLockedPages** 。

如果驱动程序验证程序不处于活动状态，则在所有情况下，这些冲突可能不会导致系统立即停止响应。 驱动程序验证程序监视驱动程序的行为，并在发生任何这些冲突时发出 bug 检查0xC4。 有关错误检查参数的列表，请参阅 [**Bug 检查 0xC4**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (驱动程序 \_ 验证器 \_ 检测到 \_ 冲突) 。

### <a name="span-idsynchronization_object_allocation_from_nonpagedpoolsession_memoryspanspan-idsynchronization_object_allocation_from_nonpagedpoolsession_memoryspanspan-idsynchronization_object_allocation_from_nonpagedpoolsession_memoryspansynchronization-object-allocation-from-nonpagedpoolsession-memory"></a><span id="Synchronization_Object_Allocation_from_NonPagedPoolSession_Memory"></span><span id="synchronization_object_allocation_from_nonpagedpoolsession_memory"></span><span id="SYNCHRONIZATION_OBJECT_ALLOCATION_FROM_NONPAGEDPOOLSESSION_MEMORY"></span>从 NonPagedPoolSession 内存分配同步对象

从 Windows 7 开始，驱动程序验证程序将从会话内存中检查同步对象。

同步对象必须为不可分页。 它们还必须位于全系统范围内的虚拟地址空间。

图形驱动程序可以通过调用 Api （如 [**EngAllocMem**](/windows/win32/api/winddi/nf-winddi-engallocmem)）分配会话内存。 与全局地址空间不同，每个终端服务器会话的会话地址空间都是虚拟的。 这意味着在两个不同会话的上下文中使用的同一虚拟地址引用了两个不同的对象。 Windows 内核必须能够从任何终端服务器会话访问同步对象。 尝试从其他会话引用会话内存地址具有不可预知的结果，如系统崩溃或其他会话数据的无提示损坏。

从 Windows 7 开始，当经验证的驱动程序通过调用 [**KeInitializeEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeevent) 或 [**KeInitializeMutex**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializemutex)等 api 初始化同步对象时，驱动程序验证器将检查该对象的地址是否落在会话虚拟地址空间内。 如果驱动程序验证器检测到这种错误的地址，则会发出 [**错误检查0xC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md)，参数1值为0xDF。

### <a name="span-idobject_reference_counter_changes_from_0_to_1spanspan-idobject_reference_counter_changes_from_0_to_1spanspan-idobject_reference_counter_changes_from_0_to_1spanobject-reference-counter-changes-from-0-to-1"></a><span id="Object_Reference_Counter_Changes_from_0_to_1"></span><span id="object_reference_counter_changes_from_0_to_1"></span><span id="OBJECT_REFERENCE_COUNTER_CHANGES_FROM_0_TO_1"></span>对象引用计数器从0更改为1

从 Windows 7 开始，驱动程序验证程序将检查其他类的不正确的对象引用。

当 Windows 内核对象管理器创建对象（如文件对象或线程对象）时，新对象的引用计数器将设置为1。 引用计数器通过对 Api （如 [**ObReferenceObjectByPointer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer) 或 [**ObReferenceObjectByHandle**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)）的调用来递增。 对于同一对象，引用计数器将减少每个 [**ObDereferenceObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject) 调用。

引用计数器达到0值后，就可以释放对象了。 对象管理器可能会立即释放该对象，否则以后可能会将其释放。 调用 [**ObReferenceObjectByPointer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer) 或 [**ObDereferenceObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject) 并将引用计数器从0更改为1意味着会递增已经释放的对象的引用计数器。 这始终不正确，因为这可能会导致其他人的内存分配损坏。

### <a name="span-idsystem_shutdown_blocks_or_delaysspanspan-idsystem_shutdown_blocks_or_delaysspanspan-idsystem_shutdown_blocks_or_delaysspansystem-shutdown-blocks-or-delays"></a><span id="System_Shutdown_Blocks_or_Delays"></span><span id="system_shutdown_blocks_or_delays"></span><span id="SYSTEM_SHUTDOWN_BLOCKS_OR_DELAYS"></span>系统关闭块或延迟

从 Windows 7 开始，如果系统关闭在启动后的20分钟内未完成，则驱动程序验证器会发出进入内核调试器的中断。 驱动程序验证程序将系统关闭的开始时间指定为 Windows 内核开始关闭其各种子系统（如注册表、即插即用或 i/o 管理器子系统）的时间。

如果内核调试器未连接到系统，则驱动程序验证程序会发出 [**Bug 检查0xC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md)，并将参数1值0x115 （而不是此断点）。

通常在不到20分钟内无法完成的系统关闭表明在该系统上运行的其中一个驱动程序出现故障。 正在运行！从内核调试器 **分析-v** 会显示负责关闭的系统工作线程的堆栈跟踪。 你应检查该堆栈跟踪，并确定该关闭线程是否被正在测试的某个驱动程序阻止。

有时，系统无法关闭，因为它受到繁重的压力测试，即使所有驱动程序都正常运行。 用户可以选择在此驱动程序验证程序断点后继续执行，并检查系统是否最终会关闭。

 

