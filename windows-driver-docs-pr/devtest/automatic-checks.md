---
title: 自动检查
description: 自动检查
ms.assetid: ec3cb6a4-d990-4830-914c-064f6c79371a
keywords:
- 自动检查 WDK Driver Verifier
- 监视 WDK Driver Verifier 的 IRQL
- 堆栈切换 WDK Driver Verifier
- 可用池计时器 WDK Driver Verifier
- 清理检查 WDK Driver Verifier
- 切换堆栈 WDK Driver Verifier
- 驱动程序卸载 WDK Driver Verifier
- Driver Verifier 选项，监视 IRQL 和内存例程
- Driver Verifier 选项，监视堆栈切换
- Driver Verifier 选项检查驱动程序卸载
- Driver Verifier 选项，监视驱动程序调度例程
- Driver Verifier 选项，监视内存调度列表 (MDL) 使用情况
ms.date: 10/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1345b51c6ba30a65991ed51cd7ec85ffd31016bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353006"
---
# <a name="automatic-checks"></a>自动检查


## <span id="ddk_automatic_checks_tools"></span><span id="DDK_AUTOMATIC_CHECKS_TOOLS"></span>


每当它验证一个或多个驱动程序时，驱动程序验证程序将执行以下检查。 无法激活或停用这些检查。 从 Windows 10 版本 1709，开始这些自动检查已移动到相关[标准标志](verifier-command-line.md)。 因此，使用标准标志启用驱动程序验证程序的用户应看到检查应用中的没有减少。

### <a name="span-idddkmonitoringirqlandmemoryroutinestoolsspanspan-idddkmonitoringirqlandmemoryroutinestoolsspanmonitoring-irql-and-memory-routines"></a><span id="ddk_monitoring_irql_and_memory_routines_tools"></span><span id="DDK_MONITORING_IRQL_AND_MEMORY_ROUTINES_TOOLS"></span>监视 IRQL 和内存例程

驱动程序验证工具监视以下已被禁止的操作的所选驱动程序：

-   通过调用引发 IRQL **KeLowerIrql**

-   通过调用降低 IRQL **KeRaiseIrql**

-   请求大小为零内存分配

-   分配或释放页面缓冲的池使用的 IRQL &gt; APC\_级别

-   分配或释放非分页缓冲的池使用的 IRQL&gt;调度\_级别

-   尝试释放未返回从以前分配的地址

-   尝试释放已释放的地址

-   获取或释放快速互斥体，IRQL &gt; APC\_级别

-   获取或释放 IRQL 不等于调度的自旋锁\_级别

-   双释放自旋锁。

-   将标记分配请求必须\_SUCCEED。 没有此类请求是曾经允许。

如果驱动程序验证程序未处于活动状态，这些冲突可能导致在所有情况下立即在系统发生崩溃。 驱动程序验证工具监视驱动程序的行为，并发出错误检查 0xC4，如果出现任何这些冲突。 请参阅[ **Bug 检查 0xC4** ](https://msdn.microsoft.com/library/windows/hardware/ff560187) (驱动程序\_VERIFIER\_检测到\_冲突) 的 bug 列表检查参数。

### <a name="span-idddkmonitoringstackswitchingtoolsspanspan-idddkmonitoringstackswitchingtoolsspanmonitoring-stack-switching"></a><span id="ddk_monitoring_stack_switching_tools"></span><span id="DDK_MONITORING_STACK_SWITCHING_TOOLS"></span>监视堆栈切换

驱动程序验证程序通过正在验证的驱动程序来监视堆栈使用。 如果驱动程序将切换其堆栈，并且新的堆栈的线程堆栈和 DPC 堆栈都不，被颁发的 bug 检查。 （这将是与第一个参数等于 0x90 bug 检查 0xC4）。显示堆栈**KB**调试器命令通常会揭示的驱动程序执行此操作。

### <a name="span-idddkcheckingondriverunloadtoolsspanspan-idddkcheckingondriverunloadtoolsspanchecking-on-driver-unload"></a><span id="ddk_checking_on_driver_unload_tools"></span><span id="DDK_CHECKING_ON_DRIVER_UNLOAD_TOOLS"></span>检查驱动程序卸载

驱动程序正在验证卸载后，驱动程序验证程序执行多个检查以确保该驱动程序已清理。

具体而言，驱动程序验证程序中查找：

-   撤消删除的计时器

-   挂起的延迟过程调用 (Dpc)

-   撤消删除后备链列表

-   撤消删除的工作线程数

-   撤消删除的队列

-   其他类似的资源

如这些可能会导致系统的问题的 bug 检查，以驱动程序卸载，并检查可能很难确定这些 bug 的原因后发出一段时间。 当驱动程序验证程序处于活动状态时，此类违规情况将导致 bug 检查 0xc7:sp 驱动程序已卸载后立即发出。 请参阅[ **Bug 检查 0xc7:sp** ](https://msdn.microsoft.com/library/windows/hardware/ff560198) (计时器\_或者\_DPC\_无效) 有关的 bug 列表检查参数。


### <a name="span-idmonitoringmemorydescriptorlistmdlusagespanspan-idmonitoringmemorydescriptorlistmdlusagespanspan-idmonitoringmemorydescriptorlistmdlusagespanmonitoring-memory-descriptor-list-mdl-usage"></a><span id="Monitoring__Memory_Descriptor_List__MDL__Usage"></span><span id="monitoring__memory_descriptor_list__mdl__usage"></span><span id="MONITORING__MEMORY_DESCRIPTOR_LIST__MDL__USAGE"></span>监视内存描述符列表 (MDL) 使用情况

在 Windows Vista 中，驱动程序验证程序还会监视以下已被禁止的操作的所选驱动程序：

-   调用[ **MmProbeAndLockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff554664)或 MmProbeAndLockProcessPages MDL 不具有适当的标记上。 例如，不应调用**MmProbeAndLockPages**为已通过创建 MDL [ **MmBuildMdlForNonPagedPool**](https://msdn.microsoft.com/library/windows/hardware/ff554498)。

-   调用[ **MmMapLockedPages** ](https://msdn.microsoft.com/library/windows/hardware/ff554622) MDL 不具有适当的标记上。 例如，不应调用**MmMapLockedPages**为已映射到系统地址 MDL 或和 MDL 未锁定。

-   调用[ **MmUnlockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff556381)或[ **MmUnmapLockedPages** ](https://msdn.microsoft.com/library/windows/hardware/ff556391)部分 MDL，也就是说，和使用创建的 MDL [ **IoBuildPartialMdl**](https://msdn.microsoft.com/library/windows/hardware/ff548324)。

-   调用**MmUnmapLockedPages**上未映射到系统地址 MDL。

如果驱动程序验证程序未处于活动状态，这些冲突可能不会导致系统停止在所有情况下立即响应。 驱动程序验证工具监视驱动程序的行为，并发出错误检查 0xC4，如果出现任何这些冲突。 请参阅[ **Bug 检查 0xC4** ](https://msdn.microsoft.com/library/windows/hardware/ff560187) (驱动程序\_VERIFIER\_检测到\_冲突) 的 bug 列表检查参数。

### <a name="span-idsynchronizationobjectallocationfromnonpagedpoolsessionmemoryspanspan-idsynchronizationobjectallocationfromnonpagedpoolsessionmemoryspanspan-idsynchronizationobjectallocationfromnonpagedpoolsessionmemoryspansynchronization-object-allocation-from-nonpagedpoolsession-memory"></a><span id="Synchronization_Object_Allocation_from_NonPagedPoolSession_Memory"></span><span id="synchronization_object_allocation_from_nonpagedpoolsession_memory"></span><span id="SYNCHRONIZATION_OBJECT_ALLOCATION_FROM_NONPAGEDPOOLSESSION_MEMORY"></span>同步从 NonPagedPoolSession 内存对象分配

驱动程序验证程序从 Windows 7 中，检查同步对象从会话内存。

同步对象必须是不可分页。 它们还必须存在于此的全局、 系统范围内的虚拟地址空间。

图形驱动程序可以如分配通过调用 Api 的会话内存[ **EngAllocMem**](https://msdn.microsoft.com/library/windows/hardware/ff564176)。 与全局地址空间中，不同的会话地址空间是为每个终端服务器会话虚拟化的。 这意味着两个不同的对象引用的两个不同的会话的上下文中使用的相同虚拟地址。 Windows 内核必须能够访问任何终端服务器会话中的同步对象。 尝试从不同的会话引用的会话内存地址具有不可预知的结果，如系统崩溃或无提示的另一个会话的数据损坏。

从 Windows 7 开始，当已验证的驱动程序初始化同步对象通过调用 Api 如[ **KeInitializeEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff552137)或[ **KeInitializeMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff552147)，驱动程序验证工具将检查是否将对象的地址范围内的会话虚拟地址空间。 如果驱动程序验证程序检测到这种不正确的地址，则会颁发[ **Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187)，0xDF 的参数 1 值。

### <a name="span-idobjectreferencecounterchangesfrom0to1spanspan-idobjectreferencecounterchangesfrom0to1spanspan-idobjectreferencecounterchangesfrom0to1spanobject-reference-counter-changes-from-0-to-1"></a><span id="Object_Reference_Counter_Changes_from_0_to_1"></span><span id="object_reference_counter_changes_from_0_to_1"></span><span id="OBJECT_REFERENCE_COUNTER_CHANGES_FROM_0_TO_1"></span>对象引用计数器从 0 更改为 1

从 Windows 7 开始，驱动程序验证工具将检查不正确的对象引用的其他类。

当 Windows 内核对象管理器创建一个对象，如文件对象或线程对象，该新对象的引用计数器设置为 1。 如对 Api 的调用通过递增引用计数器[ **ObReferenceObjectByPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff558686)或[ **ObReferenceObjectByHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff558679). 引用计数会通过减少每个[ **ObDereferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff557724)同一对象调用。

引用计数器值达到 0 的值后，该对象将成为以便释放。 对象管理器可能会立即释放它或更高版本可能会释放。 调用[ **ObReferenceObjectByPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff558686)或[ **ObDereferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff557724)并将引用计数器从 0 更改为 1 表示递增已释放对象的引用计数器。 这是始终不正确，因为这样可能会损坏，其他人的内存分配。

### <a name="span-idsystemshutdownblocksordelaysspanspan-idsystemshutdownblocksordelaysspanspan-idsystemshutdownblocksordelaysspansystem-shutdown-blocks-or-delays"></a><span id="System_Shutdown_Blocks_or_Delays"></span><span id="system_shutdown_blocks_or_delays"></span><span id="SYSTEM_SHUTDOWN_BLOCKS_OR_DELAYS"></span>系统关闭受到阻止或延迟

从 Windows 7 开始，驱动程序验证程序会发出一个分行符到内核调试程序如果系统关闭未完成 20 分钟后启动它。 驱动程序验证程序将指定的系统关闭开始为 Windows 内核开始其各种子系统，例如注册表、 插即用设备或 I/O manager 子系统正在关闭的时间。

如果内核调试器未附加到系统中，驱动程序验证程序会发出[ **Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187)，0x115，而不是此断点的参数 1 值。

通常情况下，不能在 20 分钟内完成系统关闭表示该系统运行的驱动因素之一运行不正常。 运行 **！ 分析-v**从内核调试器将显示负责关闭系统工作线程的堆栈跟踪。 您应检查该堆栈跟踪并确定是否关闭线程被阻止通过正在测试的驱动因素之一。

有时系统不能关闭，因为它受到超负荷测试-即使所有驱动程序是否正常。 用户可以选择此驱动程序验证程序断点后继续执行并检查系统是否最终关闭。

 

 





