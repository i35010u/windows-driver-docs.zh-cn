---
title: Bug 检查 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION
description: DRIVER_VERIFIER_DETECTED_VIOLATION bug 检查具有 0x000000C4 值。 这是发现的驱动程序验证程序的致命错误常规错误检查代码。
ms.assetid: 7814f827-05fc-419b-b428-4565978bbb52
keywords:
- Bug 检查 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION
- DRIVER_VERIFIER_DETECTED_VIOLATION
ms.date: 10/04/2017
topic_type:
- apiref
api_name:
- DRIVER_VERIFIER_DETECTED_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dc331c1266defef14cdbe656f0f040339c0fca6d
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238588"
---
# <a name="bug-check-0xc4-driververifierdetectedviolation"></a>Bug 检查 0xC4：驱动程序\_VERIFIER\_检测到\_冲突


该驱动程序\_VERIFIER\_检测到\_冲突错误检查的值为 0x000000C4。 这是发现的驱动程序验证程序的致命错误常规错误检查代码。 有关详细信息，请参阅[处理 Bug 检查时驱动程序验证程序已启用](handling-a-bug-check-when-driver-verifier-is-enabled.md)。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="driververifierdetectedviolation-parameters"></a>驱动程序\_VERIFIER\_检测到\_冲突参数


参数 1 标识冲突的类型。 剩余参数的含义取决于参数 1 的值。 下表所述的参数值。

**请注意**  如果遇到此表中查看所有 5 个列的问题，请尝试以下：
-   在浏览器窗口放大为实际大小。
-   将光标置于表中，使用箭头键来滚动左侧和右侧。
 
|参数 1|参数 2|参数 3|参数 4|错误的原因|
|--- |--- |--- |--- |--- |
|0x00|当前 IRQL|池类型|0|该驱动程序请求的零字节池分配。|
|0x01|当前 IRQL|池类型|分配，以字节为单位的大小|该驱动程序尝试分配的 IRQL 与分页的内存 > APC_LEVEL。|
|0x02|当前 IRQL|池类型|分配，以字节为单位的大小|该驱动程序尝试分配的 IRQL 与非分页的内存 > DISPATCH_LEVEL。|
|0x10|地址错误|0|0|该驱动程序尝试以释放分配调用未返回的地址。|
|0x11|当前 IRQL|池类型|池的地址|该驱动程序尝试以释放 IRQL 与页面缓冲的池 > APC_LEVEL。|
|0x12|当前 IRQL|池类型|池的地址|该驱动程序尝试以释放 IRQL 与非分页缓冲的池 > DISPATCH_LEVEL。|
|0x9、0x10、0x13 或 0x14|保留|指向池标头|池标头内容|该驱动程序尝试以释放已释放的内存池。|
|0x16|保留|池地址|0|尝试免费池错误地址，驱动程序或驱动程序传递给内存例程的参数无效。|
|0x30|当前 IRQL|请求的 IRQL|0|该驱动程序传递到参数无效[KeRaiseIrql](https://msdn.microsoft.com/library/windows/hardware/ff553079)。 （该参数是值低于当前 irql，因此或的值大于 HIGH_LEVEL。 这可能是使用未初始化的参数的结果。）|
|0x31|当前 IRQL|请求的 IRQL|0:新的 IRQL 为错误 1:新的 IRQL DPC 例程中无效|该驱动程序传递到参数无效[KeLowerIrql](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kelowerirql~r1)。 （该参数为的值大于当前 irql，因此或的值大于 HIGH_LEVEL。 这可能是使用未初始化的参数的结果。）|
|0x32|当前 IRQL|数值调节钮锁地址|0|该驱动程序调用[KeReleaseSpinLock](https://msdn.microsoft.com/library/windows/hardware/ff553145) DISPATCH_LEVEL 以外的 IRQL 在。 （这可能是由于双发布的自旋锁。）|
|0x33|当前 IRQL|快速互斥体地址|0|该驱动程序尝试获取快速互斥体，IRQL > APC_LEVEL。|
|0x34|当前 IRQL|快速互斥体地址|0|该驱动程序试图释放 APC_LEVEL 以外的 IRQL 在快速互斥体。|
|0x35|当前 IRQL|数值调节钮锁地址|旧的 IRQL|内核发布 IRQL 不等于 DISPATCH_LEVEL 的自旋锁。|
|0x36|当前 IRQL|数值调节钮锁数|旧的 IRQL|内核发布 IRQL 不等于 DISPATCH_LEVEL 的排队的自旋锁。|
|0x37|当前 IRQL|线程 APC 禁用计数|资源|该驱动程序尝试获取资源，但未禁用 Apc。|
|0x38|当前 IRQL|线程 APC 禁用计数|资源|该驱动程序尝试释放资源，但未禁用 Apc。|
|0x39|当前 IRQL|线程 APC 禁用计数|互斥体|尝试获取互斥体"unsafe"不等于 APC_LEVEL 条目的 IRQL 与驱动程序。|
|0x3A|当前 IRQL|线程 APC 禁用计数|互斥体|尝试释放互斥体"unsafe"不等于 APC_LEVEL 条目的 IRQL 与驱动程序。|
|0x3C|句柄传递给例程|对象类型|0|该驱动程序调用[ObReferenceObjectByHandle](https://msdn.microsoft.com/library/windows/hardware/ff558679)与错误的句柄。|
|0x3D|0|0|错误的资源的地址|该驱动程序传递到的错误 （不对齐） 资源[ExAcquireResourceExclusive](https://msdn.microsoft.com/library/windows/hardware/ff544345)。|
|0x3E|0|0|0|该驱动程序调用[KeLeaveCriticalRegion](https://msdn.microsoft.com/library/windows/hardware/ff552964)的线程的当前不在临界区。|
|0x3F|对象地址|新的对象引用计数。 -1： 取消引用案例 1： 引用用例|0|应用驱动程序[ObReferenceObject](https://msdn.microsoft.com/library/windows/hardware/ff558678)对象的引用计数为零或驱动程序应用到[ObDereferenceObject](https://msdn.microsoft.com/library/windows/hardware/ff557724)到其引用计数为零的对象。|
|0x40|当前 IRQL|数值调节钮锁地址|0|该驱动程序调用[KeAcquireSpinLockAtDpcLevel](https://msdn.microsoft.com/library/windows/hardware/ff551921) IRQL 与 < DISPATCH_LEVEL。|
|0x41|当前 IRQL|数值调节钮锁地址|0|该驱动程序调用[KeReleaseSpinLockFromDpcLevel](https://msdn.microsoft.com/library/windows/hardware/ff553150) IRQL 与 < DISPATCH_LEVEL。|
|0x42|当前 IRQL|数值调节钮锁地址|0|该驱动程序调用[KeAcquireSpinLock](https://msdn.microsoft.com/library/windows/hardware/ff551917) IRQL 与 > DISPATCH_LEVEL。|
|0x51|分配的基址|引用超出分配的地址|计费的字节数|该驱动程序试图编写分配结束后释放内存。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，会发生使用此参数的 bug 检查。|
|0x52|分配的基址|保留|计费的字节数|该驱动程序试图编写分配结束后释放内存。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，会发生使用此参数的 bug 检查。|
|0x53、 0x54 或 0x59|分配的基址|保留|保留|该驱动程序试图编写分配结束后释放内存。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，会发生使用此参数的 bug 检查。|
|0x60|从页面缓冲池分配的字节数|从非分页缓冲池分配的字节数|不释放的分配总数|该驱动程序正在卸载不首先释放其池分配。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，会发生使用此参数的 bug 检查。|
|0x61|从页面缓冲池分配的字节数|从非分页缓冲池分配的字节数|不释放的分配总数|驱动程序线程尝试卸载该驱动程序时分配池的内存。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，会发生使用此参数的 bug 检查。|
|0x62|驱动程序的名称|保留|已不释放，包括分页和非分页池的分配总数|该驱动程序正在卸载不首先释放其池分配。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，会发生使用此参数的 bug 检查。|
|0x70|当前 IRQL|MDL 地址|访问模式|该驱动程序调用[MmProbeAndLockPages](https://msdn.microsoft.com/library/windows/hardware/ff554664) IRQL 与 > DISPATCH_LEVEL。|
|0x71|当前 IRQL|MDL 地址|进程地址|驱动程序调用 IRQL 与 MmProbeAndLockProcessPages > DISPATCH_LEVEL。|
|0x72|当前 IRQL|MDL 地址|进程地址|驱动程序调用 IRQL 与 MmProbeAndLockSelectedPages > DISPATCH_LEVEL。|
|0x73|当前 IRQL|在 32 位 Windows:较低的物理地址在 64 位 Windows 的 32 位： 64 位物理地址|字节数|该驱动程序调用[MmMapIoSpace](https://msdn.microsoft.com/library/windows/hardware/ff554618) IRQL 与 > DISPATCH_LEVEL。|
|0x74|当前 IRQL|MDL 地址|访问模式|该驱动程序调用[MmMapLockedPages](https://msdn.microsoft.com/library/windows/hardware/ff554622)在内核模式下使用 IRQL > DISPATCH_LEVEL。|
|0x75|当前 IRQL|MDL 地址|访问模式|该驱动程序调用[MmMapLockedPages](https://msdn.microsoft.com/library/windows/hardware/ff554622)在用户模式下使用 IRQL > APC_LEVEL。|
|0x76|当前 IRQL|MDL 地址|访问模式|该驱动程序调用[MmMapLockedPagesSpecifyCache](https://msdn.microsoft.com/library/windows/hardware/ff554629)在内核模式下使用 IRQL > DISPATCH_LEVEL。|
|0x77|当前 IRQL|MDL 地址|访问模式|该驱动程序调用[MmMapLockedPagesSpecifyCache](https://msdn.microsoft.com/library/windows/hardware/ff554629)在用户模式下使用 IRQL > APC_LEVEL。|
|0x78|当前 IRQL|MDL 地址|0|该驱动程序调用[MmUnlockPages](https://msdn.microsoft.com/library/windows/hardware/ff556381) IRQL 与 > DISPATCH_LEVEL。|
|0x79|当前 IRQL|正在取消映射的虚拟地址|MDL 地址|该驱动程序调用[MmUnmapLockedPages](https://msdn.microsoft.com/library/windows/hardware/ff556391)在内核模式下使用 IRQL > DISPATCH_LEVEL。|
|0x7A|当前 IRQL|正在取消映射的虚拟地址|MDL 地址|该驱动程序调用[MmUnmapLockedPages](https://msdn.microsoft.com/library/windows/hardware/ff556391)在用户模式下使用 IRQL > APC_LEVEL。|
|0x7B|当前 IRQL|正在取消映射的虚拟地址|字节数|该驱动程序调用[MmUnmapIoSpace](https://msdn.microsoft.com/library/windows/hardware/ff556387) IRQL 与 > APC_LEVEL。|
|0x7C|MDL 地址|MDL 标志|0|该驱动程序调用[MmUnlockPages](https://msdn.microsoft.com/library/windows/hardware/ff556381)，并传递的 MDL 已永远不会成功锁定的页。|
|0x7D|MDL 地址|MDL 标志|0|该驱动程序调用[MmUnlockPages](https://msdn.microsoft.com/library/windows/hardware/ff556381)，并传递其页面是从非分页缓冲池 MDL。 （这些永远不应解锁。）|
|0x7E|当前 IRQL|DISPATCH_LEVEL|0|该驱动程序调用[MmAllocatePagesForMdl](https://msdn.microsoft.com/library/windows/hardware/ff554482)， [MmAllocatePagesForMdlEx](https://msdn.microsoft.com/library/windows/hardware/ff554489)，或[MmFreePagesFromMdl](https://msdn.microsoft.com/library/windows/hardware/ff554521) IRQL 与 > DISPATCH_LEVEL。|
|0x7F|当前 IRQL|MDL 地址|MDL 标志|该驱动程序调用[BuildMdlForNonPagedPool](https://msdn.microsoft.com/library/windows/hardware/ff554498)并传递其页面是从页面缓冲池 MDL。|
|0x80|当前 IRQL|事件地址|0|该驱动程序调用[KeSetEvent](https://msdn.microsoft.com/library/windows/hardware/ff553253) IRQL 与 > DISPATCH_LEVEL。|
|0x81|MDL 地址|MDL 标志|0|该驱动程序调用[MmMapLockedPages](https://msdn.microsoft.com/library/windows/hardware/ff554622)。 (您应使用[MmMapLockedPagesSpecifyCache](https://msdn.microsoft.com/library/windows/hardware/ff554629)相反，使用 BugCheckOnFailure 参数设置为 FALSE。)|
|0x82|MDL 地址|MDL 标志|0|该驱动程序调用[MmMapLockedPagesSpecifyCache](https://msdn.microsoft.com/library/windows/hardware/ff554629)与 BugCheckOnFailure 参数等于 TRUE。 （此参数应设置为 FALSE。）|
|0x83|若要映射的物理地址范围的开始|要映射的字节数|第一页不锁定的帧数|该驱动程序调用[MmMapIoSpace](https://msdn.microsoft.com/library/windows/hardware/ff554618)而无需具有锁定 MDL 页。 要映射的物理地址范围所表示的物理页必须已被锁定在进行此调用之前。|
|0x85|MDL 地址|要映射的页数|第一页不锁定的帧数|该驱动程序调用[MmMapLockedPages](https://msdn.microsoft.com/library/windows/hardware/ff554622)而无需具有锁定 MDL 页。|
|0x89|MDL 地址|指针到 MDL 中的非内存页|在 MDL 非内存页面数|MDL 未标记为"I/O"，但它包含非内存页地址。|
|0x91|保留|保留|保留|该驱动程序切换堆栈使用不受操作系统的方法。 扩展内核模式堆栈的唯一受支持的方法是使用[KeExpandKernelStackAndCallout](https://msdn.microsoft.com/library/windows/hardware/ff552030)。|
|0xA0 （Windows Server 2003 和更高版本仅操作系统）|指向 IRP 发出读取或写入请求|较低的设备的设备对象|在其中检测到错误的扇区数|在硬盘上检测到循环冗余校验 (CRC) 错误。 仅当驱动程序验证程序的磁盘完整性检查选项处于活动状态时，会发生使用此参数的 bug 检查。|
|0xA1 （Windows Server 2003 和更高版本仅操作系统）|IRP 进行读取或写入请求的副本。 （实际 IRP 已经完成。）|较低的设备的设备对象|在其中检测到错误的扇区数|CRC 错误检测到上一个扇区 （异步）。 仅当驱动程序验证程序的磁盘完整性检查选项处于活动状态时，会发生使用此参数的 bug 检查。|
|0xA2 （Windows Server 2003 和更高版本仅操作系统）|进行读取或写入请求，还是一份此 IRP 的 IRP|较低的设备的设备对象|在其中检测到错误的扇区数|CRCDISK 校验和副本不匹配。 这可能是分页错误。 仅当驱动程序验证程序的磁盘完整性检查选项处于活动状态时，会发生使用此参数的 bug 检查。|
|0xB0 （Windows Vista 和更高版本仅操作系统）|MDL 地址|MDL 标志|不正确 MDL 标志|该驱动程序调用[MmProbeAndLockPages](https://msdn.microsoft.com/library/windows/hardware/ff554664)为 MDL 与不正确的标志。 例如，驱动程序传递由创建 MDL [MmBuildMdlForNonPagedPool](https://msdn.microsoft.com/library/windows/hardware/ff554498) MmProbeAndLockPages 到。|
|说是 0xB1 （Windows Vista 和更高版本仅操作系统）|MDL 地址|MDL 标志|不正确 MDL 标志|为与不正确的标志 MDL 调用 MmProbeAndLockProcessPages 驱动程序。 例如，驱动程序传递由创建 MDL [MmBuildMdlForNonPagedPool](https://msdn.microsoft.com/library/windows/hardware/ff554498) MmProbeAndLockProcessPages 到。|
|0xB2 （Windows Vista 和更高版本仅操作系统）|MDL 地址|MDL 标志|不正确 MDL 标志|该驱动程序调用[MmMapLockedPages](https://msdn.microsoft.com/library/windows/hardware/ff554622)为 MDL 与不正确的标志。 例如，驱动程序传递的已映射到系统地址或的未锁定到 MmMapLockedPages MDL。|
|0xB3 （Windows Vista 和更高版本仅操作系统）|MDL 地址|MDL 标志|缺少 MDL 标志 （至少一个预期的）|该驱动程序调用[MmMapLockedPages](https://msdn.microsoft.com/library/windows/hardware/ff554622)为 MDL 与不正确的标志。 例如，驱动程序传递未锁定 MDL MmMapLockedPages 到。|
|0xB4 （Windows Vista 和更高版本仅操作系统）|MDL 地址|MDL 标志|意外的部分 MDL 标志|该驱动程序调用[MmUnlockPages](https://msdn.microsoft.com/library/windows/hardware/ff556381)的部分 MDL。 部分 MDL 是指已通过[IoBuildPartialMdl](https://msdn.microsoft.com/library/windows/hardware/ff548324)。|
|0xB8 （Windows Vista 和更高版本仅操作系统）|MDL 地址|MDL 标志|保留|仍然映射由 MDL 描述的页面。 该驱动程序必须调用 IoFreeMdl 之前取消映射页。|
|0xC0 （Windows Vista 和更高版本仅操作系统）|IRP 的地址|保留|保留|该驱动程序调用[IoCallDriver](https://msdn.microsoft.com/library/windows/hardware/ff548336)都会在禁用。|
|0xC1 （Windows Vista 和更高版本仅操作系统）|驱动程序调度例程的地址|保留|保留|驱动程序调度例程返回都会在禁用。|
|0xC2 （Windows Vista 和更高版本仅操作系统）|保留|保留|保留|已禁用，中断后，驱动程序将调用快速 I/O 调度例程。|
|0xC3 （Windows Vista 和更高版本仅操作系统）|驱动程序快速 I/O 调度例程的地址|保留|保留|驱动程序快速 I/O 调度例程返回都会在禁用。|
|0xC5 （Windows Vista 和更高版本仅操作系统）|驱动程序调度例程的地址|当前线程的 APC 禁用计数|线程的 APC 禁用驱动程序调度例程在调用前的计数|驱动程序调度例程已更改线程的 APC 禁用计数。 APC 禁用计数将减少每次将驱动程序调用[KeEnterCriticalRegion](https://msdn.microsoft.com/library/windows/hardware/ff552021)， [FsRtlEnterFileSystem](https://msdn.microsoft.com/library/windows/hardware/ff545900)，或获取互斥锁。 APC 禁用计数每的次递增一个驱动程序调用[KeLeaveCriticalRegion](https://msdn.microsoft.com/library/windows/hardware/ff552964)， [KeReleaseMutex](https://msdn.microsoft.com/library/windows/hardware/ff553140)，或[FsRtlExitFileSystem](https://msdn.microsoft.com/library/windows/hardware/ff545908)。 由于这些调用应该总是以对，APC 禁用计数应为零，每当线程退出。 负值指示的驱动程序具有未重新启用这些情况下禁用 APC 的调用。 正值指示反向为 true。|
|为 0xC6 （Windows Vista 和更高版本仅操作系统）|驱动程序快速 I/O 调度例程的地址|当前线程的 APC 禁用计数|线程的 APC 禁用快速 I/O 驱动程序调度例程在调用前的计数|驱动程序快速 I/O 调度例程已更改线程的 APC 禁用计数。 APC 禁用计数将减少每次将驱动程序调用[KeEnterCriticalRegion](https://msdn.microsoft.com/library/windows/hardware/ff552021)， [FsRtlEnterFileSystem](https://msdn.microsoft.com/library/windows/hardware/ff545900)，或获取互斥锁。 APC 禁用计数每的次递增一个驱动程序调用[KeLeaveCriticalRegion](https://msdn.microsoft.com/library/windows/hardware/ff552964)， [KeReleaseMutex](https://msdn.microsoft.com/library/windows/hardware/ff553140)，或[FsRtlExitFileSystem](https://msdn.microsoft.com/library/windows/hardware/ff545908)。 由于这些调用应该总是以对，APC 禁用计数应为零，每当线程退出。 负值指示的驱动程序具有未重新启用这些情况下禁用 APC 的调用。 正值指示反向为 true。|
|位 0xCA （Windows Vista 和更高版本仅操作系统）|后备链列表地址|保留|保留|该驱动程序已尝试重新初始化后备链列表。|
|0xCB （Windows Vista 和更高版本仅操作系统）|后备链列表地址|保留|保留|该驱动程序已尝试删除未初始化后备链列表。|
|0xCC （Windows Vista 和更高版本仅操作系统）|后备链列表地址|池分配的起始地址|池分配的大小|该驱动程序已尝试免费包含的活动的后备链列表的池分配。|
|0xcd 填充 （Windows Vista 和更高版本仅操作系统）|后备链列表地址|指定由调用方的块大小|最小支持的块大小|该驱动程序已尝试创建一个后备链列表太小的分配块大小。|
|0xD0 （Windows Vista 和更高版本仅操作系统）|ERESOURCE 结构的地址|保留|保留|该驱动程序已尝试重新初始化 ERESOURCE 结构。|
|0xD1 （Windows Vista 和更高版本仅操作系统）|ERESOURCE 结构的地址|保留|保留|该驱动程序已尝试删除未初始化的 ERESOURCE 结构。|
|0xD2 （Windows Vista 和更高版本仅操作系统）|ERESOURCE 结构的地址|池分配的起始地址|池分配的大小|该驱动程序已尝试免费包含的活动 ERESOURCE 结构的池分配。|
|0xD5 （Windows Vista 和更高版本仅操作系统）|IO_REMOVE_LOCK 结构创建的调试内部版本版本的驱动程序的地址|当前[IoReleaseRemoveLock](https://msdn.microsoft.com/library/windows/hardware/ff549560)标记|保留|当前[IoReleaseRemoveLock](https://msdn.microsoft.com/library/windows/hardware/ff549560)标记不匹配上一个[IoAcquireRemoveLock](https://msdn.microsoft.com/library/windows/hardware/ff548204)标记。 如果调用 IoReleaseRemoveLock 的驱动程序不在已检验版本中，参数 2 为代表该驱动程序创建驱动程序验证程序的卷影 IO_REMOVE_LOCK 结构的地址。 在这种情况下，驱动程序使用的 IO_REMOVE_LOCK 结构的地址是根本不使用，因为驱动程序验证程序替换所有删除锁 Api 的锁地址。 仅当驱动程序验证程序的 I/O 验证选项处于活动状态时，会发生使用此参数的 bug 检查。|
|0xD6 （Windows Vista 和更高版本仅操作系统）|IO_REMOVE_LOCK 结构创建的调试内部版本版本的驱动程序的地址|标记不匹配以前[IoAcquireRemoveLock](https://msdn.microsoft.com/library/windows/hardware/ff548204)标记|以前[IoAcquireRemoveLock](https://msdn.microsoft.com/library/windows/hardware/ff548204)标记|当前[IoReleaseRemoveLockAndWait](https://msdn.microsoft.com/library/windows/hardware/ff549567)标记不匹配上一个[IoAcquireRemoveLock](https://msdn.microsoft.com/library/windows/hardware/ff548204)标记。 如果驱动程序调用[IoReleaseRemoveLock](https://msdn.microsoft.com/library/windows/hardware/ff549560)不是已检验的版本中，参数 2 是代表该驱动程序创建驱动程序验证程序的卷影 IO_REMOVE_LOCK 结构的地址。 在这种情况下，驱动程序使用的 IO_REMOVE_LOCK 结构的地址是根本不使用，因为驱动程序验证程序替换所有删除锁 Api 的锁地址。 仅当驱动程序验证程序的 I/O 验证选项处于活动状态时，会发生使用此参数的 bug 检查。|
|0xD7 (Windows 7 操作系统及更高版本)|驱动程序验证程序供内部使用的已检验的版本删除锁结构的地址|指定驱动程序的删除锁结构的地址|保留|删除锁不能为重新初始化，即使它会调用[IoReleaseRemoveLockAndWait](https://msdn.microsoft.com/library/windows/hardware/ff549567)，因为其他线程可能仍将使用该锁 (通过调用[IoAcquireRemoveLock](https://msdn.microsoft.com/library/windows/hardware/ff548204))。 该驱动程序应分配其设备扩展，在删除锁定并对其进行初始化一次。 将与设备扩展一起删除锁。|
|0xDA （Windows Vista 和更高版本仅操作系统）|驱动程序的起始地址|驱动程序内的 WMI 回调地址|保留|尝试卸载具有未取消注册其 WMI 的回调函数的驱动程序。|
|0xDB （Windows Vista 和更高版本仅操作系统）|设备对象的地址|保留|保留|尝试从 WMI 中删除未取消注册的设备对象。|
|0xDC （Windows Vista 和更高版本仅操作系统）|保留|保留|保留|作为函数的参数指定了无效的 RegHandle 值[EtwUnregister](https://msdn.microsoft.com/library/windows/hardware/ff545613)。|
|0xdd 填充 （Windows Vista 和更高版本仅操作系统）|EtwRegister 调用的地址|正在卸载驱动程序的起始地址|对于 Windows 8 和更高版本中，此参数是 ETW RegHandle 值。|尝试卸载驱动程序而无需调用[EtwUnregister](https://msdn.microsoft.com/library/windows/hardware/ff545613)。|
|0xDF (Windows 7 操作系统及更高版本)|同步对象地址|同步对象是会话地址空间中。 因为它们可以从另一个会话或尚未会话虚拟地址空间的系统线程操作会话地址空间中不允许同步对象。|
|0xE0 （Windows Vista 和更高版本仅操作系统）|使用作为参数的用户模式地址|大小 （字节），作为参数使用的地址范围|保留|为用户模式地址指定为参数的操作系统内核函数调用了。|
|0xE1 （Windows Vista 和更高版本仅操作系统）|同步对象的地址|保留|保留|找到同步对象具有无效或可分页的地址。|
|0xE2 （Windows Vista 和更高版本仅操作系统）|IRP 的地址|用户模式地址位于 IRP|保留|使用 Irp irp->requestormode 设置为 KernelMode 找具有用户模式地址作为其成员之一。|
|0xE3 （Windows Vista 和更高版本仅操作系统）|对 API 调用的地址|用户模式地址作为 API 中的参数|保留|驱动程序已对用户模式地址使用的内核模式 ZwXxx 例程的调用作为参数。|
|0xE4 （Windows Vista 和更高版本仅操作系统）|对 API 调用的地址|格式不正确的 UNICODE_STRING 结构的地址|保留|驱动程序已对具有格式不正确的 UNICODE_STRING 结构的内核模式 ZwXxx 例程的调用作为参数。|
|0xE5 （Windows Vista 和更高版本仅操作系统）|当前 IRQL|保留|保留|调用了不正确的 IRQL 在内核 API。|
|0xE6 （Windows Vista 和更高版本仅操作系统）|解决在驱动程序进行 Zw API 调用|当前 IRQL|特殊内核 Apc。|内核 Zw API 未调用在 IRQL = passive_level 调用和具有特殊内核 Apc 启用。|
|0xEA （Windows Vista 和更高版本仅操作系统）|当前 IRQL|线程的 APC 禁用计数|Pushlock 的地址|驱动程序已尝试获取 pushlock 启用 Apc 时。|
|0xEB （Windows Vista 和更高版本仅操作系统）|当前 IRQL|线程的 APC 禁用计数|Pushlock 的地址|驱动程序已尝试启用 Apc 的同时释放 pushlock。|
|0xF0 （Windows Vista 和更高版本仅操作系统）|目标缓冲区的地址|源缓冲区的地址|要复制的字节数|驱动程序调用具有重叠的源和目标缓冲区的 memcpy 函数。|
|0xF5 （Windows Vista 和更高版本仅操作系统）|NULL 句柄的地址|对象类型|保留|驱动程序传递的 NULL 句柄[ObReferenceObjectByHandle](https://msdn.microsoft.com/library/windows/hardware/ff558679)。|
|0xF6 (Windows 7 操作系统及更高版本)|所引用的句柄值|当前进程的地址|在执行引用不正确的驱动程序地址|驱动程序引用作为内核模式的用户模式下句柄。|
|0xF7 (Windows 7 操作系统及更高版本)|指定由调用方的句柄值|由调用方指定的对象类型|指定由调用方的 AccessMode|驱动程序正尝试在系统进程的上下文中的内核句柄的用户模式下引用。|
|0xFA (Windows 7 操作系统及更高版本)|完成例程的地址。|调用完成例程之前的 IRQL 值|当前 IRQL 值之后它将调用完成例程|在调用返回了不同于 IRQL 例程的 IRQL 在 IRP 完成例程。|
|0xFB (Windows 7 操作系统及更高版本)|完成例程的地址|当前线程的 APC 禁用计数|线程的 APC 调用 IRP 完成例程之前禁用计数|线程的 APC 禁用计数进行了更改的驱动程序的 IRP 完成例程。 APC 禁用计数将减少每次将驱动程序调用[KeEnterCriticalRegion](https://msdn.microsoft.com/library/windows/hardware/ff552021)， [FsRtlEnterFileSystem](https://msdn.microsoft.com/library/windows/hardware/ff545900)，或获取互斥锁。 APC 禁用计数每的次递增一个驱动程序调用[KeLeaveCriticalRegion](https://msdn.microsoft.com/library/windows/hardware/ff552964)， [KeReleaseMutex](https://msdn.microsoft.com/library/windows/hardware/ff553140)，或[FsRtlExitFileSystem](https://msdn.microsoft.com/library/windows/hardware/ff545908)。 由于这些调用应该总是以对，APC 禁用计数应为零，每当线程退出。 负值指示的驱动程序具有未重新启用这些情况下禁用 APC 的调用。 正值指示反向为 true。|
|0x105 (Windows 7 操作系统及更高版本)|IRP 的地址|该驱动程序使用而不是 IoFreeIrp ExFreePool 来释放 IRP。|
|0x10A (Windows 7 操作系统及更高版本)|驱动程序将尝试收费到空闲进程池配额。|
|0x10B (Windows 7 操作系统及更高版本)|驱动程序将尝试从 DPC 例程的池配额进行收费。 这是不正确，因为当前进程上下文是未定义。|
|0x110 (Windows 7 操作系统及更高版本)|中断服务例程的地址|扩展执行 ISR 前已保存的上下文的地址|扩展上下文的地址执行 ISR 后已保存|该驱动程序中断服务例程 (ISR) 已损坏的扩展的线程上下文。|
|0x111 (Windows 7 操作系统及更高版本)|中断服务例程的地址|执行 ISR 之前的 IRQL|执行 ISR 后的 IRQL|中断服务例程返回更改的 IRQL。|
|0x115 (Windows 7 操作系统及更高版本)|负责关闭，进而可能会发生死锁的线程的地址|驱动程序验证程序检测到系统所用的时间超过 20 分钟关闭未完成。|
|0x11A (Windows 7 操作系统及更高版本)|当前 IRQL|该驱动程序调用的 IRQL KeEnterCriticalRegion > APC_LEVEL。|
|0x11B (Windows 7 操作系统及更高版本)|当前 IRQL|该驱动程序调用的 IRQL KeLeaveCriticalRegion > APC_LEVEL。|
|0x120 (Windows 7 操作系统及更高版本)|地址的 IRQL 值|若要等待的对象的地址|超时值的地址|在线程等待在 IRQL > DISPATCH_LEVEL。 KeWaitForSingleObject 或 KeWaitForMultipleObjects 的调用方都必须运行在 IRQL < = DISPATCH_LEVEL。|
|0x121 (Windows 7 操作系统及更高版本)|地址的 IRQL 值|若要等待的对象的地址|超时值的地址|在线程等待在 IRQL 等于 DISPATCH_LEVEL 和超时值为 NULL。 KeWaitForSingleObject 或 KeWaitForMultipleObjects 的调用方可以运行在 IRQL < = DISPATCH_LEVEL。 如果超时为提供一个 NULL 指针，则调用线程一直处于等待状态的对象发出信号。|
|0x122 (Windows 7 操作系统及更高版本)|地址的 IRQL 值|若要等待的对象的地址|超时值的地址|在线程等待在 DISPATCH_LEVEL 和超时值不等于零 (0)。 如果在超时 ！ = 0，KeWaitForSingleObject 或 KeWaitForMultipleObjects 的调用方都必须运行在 IRQL < = APC_LEVEL。|
|0x123 (Windows 7 操作系统及更高版本)|若要等待的对象的地址|KeWaitForSingleObject 或 KeWaitForMultipleObjects 的调用方指定等待为用户模式，但该对象是内核堆栈上。|
|0x130 (Windows 7 操作系统及更高版本)|工作项的地址|工作项处于会话地址空间。 因为它们可以从另一个会话或尚未会话虚拟地址空间的系统线程操作会话地址空间中不允许工作项。|
|0x131 (Windows 7 操作系统及更高版本)|工作项的地址|工作项是在可分页内存中。 工作项必须位于不可分页的内存，因为内核在 DISPATCH_LEVEL 中使用它们。|
|0x135|IRP 的地址|之间的毫秒数允许[IoCancelIrp](https://msdn.microsoft.com/library/windows/hardware/ff548338)调用和此 irp 完成|已取消的 IRP 未在预期时间，该驱动程序花费的时间超过预期完成取消的 IRP 未完成。|
|0x13A|要释放的池块的地址|不正确的值|值不正确的地址|该驱动程序已调用[ExFreePool](https://msdn.microsoft.com/library/windows/hardware/ff544590)和驱动程序验证程序检测到错误，在内部用于跟踪池使用的值之一。|
|0x13B|要释放的池块的地址|值不正确的地址|不正确的内存页的指针的地址|该驱动程序已调用[ExFreePool](https://msdn.microsoft.com/library/windows/hardware/ff544590)和驱动程序验证程序检测到错误，在内部用于跟踪池使用的值之一。|
|0x13C|要释放的池块的地址|不正确的值|值不正确的地址|该驱动程序已调用[ExFreePool](https://msdn.microsoft.com/library/windows/hardware/ff544590)和驱动程序验证程序检测到错误，在内部用于跟踪池使用的值之一。|
|0x13D|要释放的池块的地址|值不正确的地址|应有的正确值|该驱动程序已调用[ExFreePool](https://msdn.microsoft.com/library/windows/hardware/ff544590)和驱动程序验证程序检测到错误，在内部用于跟踪池使用的值之一。|
|0x13E|由调用方指定的池块地址|跟踪驱动程序验证程序的池块地址|指向由驱动程序验证程序时进行跟踪的池块地址|池阻止的调用方指定的地址[ExFreePool](https://msdn.microsoft.com/library/windows/hardware/ff544590)不同于跟踪的驱动程序验证程序的地址。|
|0x13F|要释放的池块的地址|要释放的字节数|指向由驱动程序验证程序跟踪的字节数|正在对的调用中释放的内存字节数[ExFreePool](https://msdn.microsoft.com/library/windows/hardware/ff544590)不同于跟踪的驱动程序验证程序的字节数。|
|0x140|当前 IRQL|MDL 地址|与此 MDL 相关联的虚拟地址|非锁定 MDL 是从可分页或 tradable 内存构造。|
|0x1000 |该资源的地址|保留|保留|自发生死锁：当前线程已尝试以递归方式获取资源。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，会发生使用此参数的 bug 检查。|
|0x1001 |最终导致死锁资源的地址|保留|保留|死锁：已找到锁层次结构冲突。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，会发生使用此参数的 bug 检查。 (使用[！ 死锁](-deadlock.md)扩展有关的详细信息。)|
|0x1002 |该资源的地址|保留|保留|未初始化的资源：已获取资源而无需首先尚未初始化。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，会发生使用此参数的 bug 检查。|
|0x1003 |地址被释放的资源发生死锁|应已发布了第一次该资源的地址|保留|意外的版本：资源已经发布了顺序不正确。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，会发生使用此参数的 bug 检查。|
|0x1004 |该资源的地址|获取资源的线程的地址|当前线程的地址|意外的线程：错误的线程释放资源。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，会发生使用此参数的 bug 检查。|
|0x1005 |该资源的地址|保留|保留|多次初始化：资源被初始化一次。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，会发生使用此参数的 bug 检查。|
|0x1007 |该资源的地址|保留|保留|获得的资源：之前已获取，则释放资源。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，会发生使用此参数的 bug 检查。|
|0x1008 相关联 (Windows 7 操作系统及更高版本)|锁地址|驱动程序验证工具内部数据|驱动程序验证工具内部数据|该驱动程序尝试使用此锁类型不匹配的 API 获取的锁。|
|0x1009 (Windows 7 操作系统及更高版本)|锁地址|驱动程序验证工具内部数据|驱动程序验证工具内部数据|该驱动程序尝试使用此锁类型不匹配的 API 释放锁。|
|0x100A (Windows 7 操作系统及更高版本)|所有者线程地址|驱动程序验证工具内部数据|终止的线程拥有该锁。|
|0x100B (Windows 7 操作系统及更高版本)|锁地址|所有者线程地址|驱动程序验证工具内部地址|已删除的锁仍属于一个线程。|
|0xA001 (Windows 8.1 操作系统及更高版本)|指向 NetBufferList 对象的指针|指向虚拟交换机对象 （如果非 NULL) 的指针|保留 （未使用）|VM 交换机：必须设置为调用方提供 NetBufferList SourceHandle。 请参阅[AllocateNetBufferListForwardingContext](https://msdn.microsoft.com/library/windows/hardware/hh598134)例程。|
|0xA002 (Windows 8.1 操作系统及更高版本)|指向 NetBufferList 对象的指针|一个指向虚拟交换机对象 （如果非 NULL)。|保留 （未使用）|VM 交换机：调用方提供 NetBufferList 转发详细信息不为零。 请参阅[AllocateNetBufferListForwardingContext](https://msdn.microsoft.com/library/windows/hardware/hh598134)例程。|
|0xA003 (Windows 8.1 操作系统及更高版本)|指向 NetBufferList 对象的指针|一个指向虚拟交换机对象 （如果非 NULL)。|保留 （未使用）|VM 交换机：调用方提供 NetBufferList 数据包标头或为 NULL 的路由上下文。 请参阅[可扩展交换机数据路径的数据包管理准则](https://msdn.microsoft.com/library/windows/hardware/hh582270)。|
|0xA004 (Windows 8.1 操作系统及更高版本)|无效的端口的 ID|NIC 索引|一个指向虚拟交换机对象 （如果非 NULL)。|VM 交换机：调用方指定一个无效的端口和 NIC 索引组合。 请参阅[的 HYPER-V 可扩展交换机端口和网络适配器状态](https://msdn.microsoft.com/library/windows/hardware/hh598182)。|
|0xA005 (Windows 8.1 操作系统及更高版本)|指向 NetBufferList 对象的指针|指向目标列表的指针。|一个指向虚拟交换机对象 （如果非 NULL)。|VM 交换机：调用方提供的目标无效。 请参阅[AddNetBufferListDestination](https://msdn.microsoft.com/library/windows/hardware/hh598133)并[UpdateNetBufferListDestinations](https://msdn.microsoft.com/library/windows/hardware/hh598303)。|
|0xA006 (Windows 8.1 操作系统及更高版本)|指向 NetBufferList 对象的指针|一个指向虚拟交换机对象 （如果非 NULL)。|保留 （未使用）|VM 交换机：调用方提供无效的源 NIC 或端口对象。 请参阅[的 HYPER-V 可扩展交换机端口和网络适配器状态](https://msdn.microsoft.com/library/windows/hardware/hh598182)。|
|0xA007 (Windows 8.1 操作系统及更高版本)|指向 NetBufferList 对象的指针|一个指向虚拟交换机对象 （如果非 NULL)。|保留 （未使用）|VM 交换机：调用方提供的无效目标列表。 请参阅[AddNetBufferListDestination](https://msdn.microsoft.com/library/windows/hardware/hh598133)并[UpdateNetBufferListDestinations](https://msdn.microsoft.com/library/windows/hardware/hh598303)。|
|0xA008 (Windows 8.1 操作系统及更高版本)|父 NIC 对象|NIC 索引|一个指向虚拟交换机对象 （如果非 NULL)。|VM 交换机：尝试引用时不允许使用的 NIC。 请参阅[的 HYPER-V 可扩展交换机端口和网络适配器状态](https://msdn.microsoft.com/library/windows/hardware/hh598182)。|
|0xA009 (Windows 8.1 操作系统及更高版本)|所引用的端口|指向虚拟交换机对象 （如果非 NULL) 的指针|保留 （未使用）|VM 交换机：尝试引用时不允许使用的端口。 请参阅[的 HYPER-V 可扩展交换机端口和网络适配器状态](https://msdn.microsoft.com/library/windows/hardware/hh598182)。|
|0xA00A (Windows 8.1 操作系统及更高版本)|指向 NetBufferList 对象的指针|ContextTypeInfo 对象|保留 （未使用）|VM 交换机：已设置失败上下文。 请参阅[SetNetBufferListSwitchContext](https://msdn.microsoft.com/library/windows/hardware/hh846223)。|
|0xA00B (Windows 8.1 操作系统及更高版本)|指向 NetBufferList 对象的指针|NDIS_SWITCH_REPORT_FILTERED_NBL_FLAGS_*|指向虚拟交换机对象 （如果非 NULL) 的指针|VM 交换机：提供有关已删除 NetBufferList 的方向无效。 请参阅[ReportFilteredNetBufferLists](https://msdn.microsoft.com/library/windows/hardware/hh598297)。|
|0xA00C (Windows 8.1 操作系统及更高版本)|指向 NetBufferList 对象的指针|发送标志值|指向虚拟交换机对象 （如果非 NULL) 的指针|VM 交换机：NetBufferList 链具有多个源端口设置 NDIS_SEND_FLAGS_SWITCH_SINGLE_SOURCE 标志。 请参阅[的 HYPER-V 可扩展交换机发送和接收标志](https://msdn.microsoft.com/library/windows/hardware/hh598186)。|
|0xA00D (Windows 8.1 操作系统及更高版本)|指向 NetBufferList 对象的指针|一个指向虚拟交换机上下文|指向虚拟交换机对象 （如果非 NULL) 的指针|VM 交换机：链中的一个或多个 NetBufferLists 具有无效的目标设置 NDIS_RECEIVE_FLAGS_SWITCH_DESTINATION_GROUP 标志。 请参阅[的 HYPER-V 可扩展交换机发送和接收标志](https://msdn.microsoft.com/library/windows/hardware/hh598186)。|
|0x2000 (Windows 7 操作系统及更高版本)|第一个参数传递给[StorPortInitialize](https://msdn.microsoft.com/library/windows/hardware/ff567108)例程。 此参数是指向传递给微型端口驱动程序的第一个参数中的微型端口驱动程序的操作系统的驱动程序对象的指针[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程。|第二个参数传递给[StorPortInitialize](https://msdn.microsoft.com/library/windows/hardware/ff567108)例程。 此参数是指向传递给操作系统的上下文信息的微型端口驱动程序的第二个参数中的微型端口驱动程序[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程。|保留|Storport 微型端口驱动程序错误的参数 （NULL 指针） 传递给[StorPortInitialize](https://msdn.microsoft.com/library/windows/hardware/ff567108)例程。|
|0x00020002 (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlApcLte](https://msdn.microsoft.com/library/windows/hardware/ff547740)。 该规则指定驱动程序必须调用[ObGetObjectSecurity](https://msdn.microsoft.com/library/windows/hardware/ff557738)并[ObReleaseObjectSecurity](https://msdn.microsoft.com/library/windows/hardware/ff558695)仅当 IRQL < = APC_LEVEL。|
|0x00020003 (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlDispatch](https://msdn.microsoft.com/library/windows/hardware/ff547743)。 IrqlDispatch 规则指定驱动程序必须调用某些例程时，才 IRQL = DISPATCH_LEVEL|
|0x00020004 (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlExAllocatePool](https://msdn.microsoft.com/library/windows/hardware/ff547747)。 IrqlExAllocatePool 规则指定驱动程序调用[ExAllocatePoolWithTag](https://msdn.microsoft.com/library/windows/hardware/ff544520)并[ExAllocatePoolWithTagPriority](https://msdn.microsoft.com/library/windows/hardware/ff544523)仅当在 IRQL < = DISPATCH_LEVEL。|
|0x00020005 (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlExApcLte1](https://msdn.microsoft.com/library/windows/hardware/ff547748)。 IrqlExApcLte1 规则指定驱动程序只能在 IRQL 中，调用 ExAcquireFastMutex 和 ExTryToAcquireFastMutex < = APC_LEVEL。|
|0x00020006 (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlExApcLte2](https://msdn.microsoft.com/library/windows/hardware/ff547751)。 IrqlExApcLte2 规则指定驱动程序调用某些例程时，才 IRQL < = APC_LEVEL。|
|0x00020007 (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlExApcLte3](https://msdn.microsoft.com/library/windows/hardware/ff547753)。 IrqlExApcLte3 规则指定驱动程序必须调用某些执行支持例程时，才 IRQL < = APC_LEVEL。|
|0x00020008 (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlExPassive](https://msdn.microsoft.com/library/windows/hardware/ff547756)。 IrqlExPassive 规则指定驱动程序必须调用某些执行支持例程时，才 IRQL = passive_level 调用。|
|0x00020009 (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlIoApcLte](https://msdn.microsoft.com/library/windows/hardware/ff547759)。 IrqlIoApcLte 规则指定驱动程序必须调用某些 I/O 管理器例程时，才 IRQL < = APC_LEVEL。|
|0x0002000A (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlIoPassive1](https://msdn.microsoft.com/library/windows/hardware/ff547763)。 IrqlIoPassive1 规则指定驱动程序必须调用某些 I/O 管理器例程时，才 IRQL = passive_level 调用。|
|0x0002000B (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlIoPassive2](https://msdn.microsoft.com/library/windows/hardware/ff547766)。 IrqlIoPassive2 规则指定驱动程序必须调用某些 I/O 管理器例程时，才 IRQL = passive_level 调用。|
|0x0002000C (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlIoPassive3](https://msdn.microsoft.com/library/windows/hardware/ff547780)。 IrqlIoPassive3 规则指定驱动程序必须调用某些 I/O 管理器例程时，才 IRQL = passive_level 调用。|
|0x0002000D (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlIoPassive4](https://msdn.microsoft.com/library/windows/hardware/ff547787)。 IrqlIoPassive4 规则指定驱动程序必须调用某些 I/O 管理器例程时，才 IRQL = passive_level 调用。|
|0x0002000E (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlIoPassive5](https://msdn.microsoft.com/library/windows/hardware/ff547796)。 IrqlIoPassive5 规则指定驱动程序必须调用某些 I/O 管理器例程时，才 IRQL = passive_level 调用。|
|0x0002000F (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlKeApcLte1](https://msdn.microsoft.com/library/windows/hardware/ff547803)。 IrqlKeApcLte1 规则指定驱动程序必须调用某些内核例程时，才 IRQL < = APC_LEVEL。|
|0x00020010 (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlKeApcLte2](https://msdn.microsoft.com/library/windows/hardware/ff547806)。 IrqlKeApcLte2 规则指定驱动程序必须调用某些内核例程时，才 IRQL < = APC_LEVEL。|
|0x00020011 (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlKeDispatchLte](https://msdn.microsoft.com/library/windows/hardware/ff547812)。 IrqlKeDispatchLte 规则指定驱动程序必须调用某些内核例程时，才 IRQL < = DISPATCH_LEVEL。|
|0x00020015 (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlKeReleaseSpinLock](https://msdn.microsoft.com/library/windows/hardware/ff547830)。 该驱动程序必须调用 KeReleaseSpinLock IrqlKeReleaseSpinLock 规则指定仅当 IRQL = DISPATCH_LEVEL。|
|0x00020016 (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlKeSetEvent](https://msdn.microsoft.com/library/windows/hardware/ff547835)。 IrqlKeSetEvent 规则规定[KeSetEvent](https://msdn.microsoft.com/library/windows/hardware/ff553253)在 IRQL 仅调用例程 < 时等待设置为 FALSE，而在 IRQL = DISPATCH_LEVEL < = APC_LEVEL 等待设置为 TRUE 时。|
|0x00020019 (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlMmApcLte](https://msdn.microsoft.com/library/windows/hardware/ff547855)。 IrqlMmApcLte 规则指定驱动程序，必须调用某些内存管理器例程时，才 IRQL < = APC_LEVEL。|
|0x0002001A (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlMmDispatch](https://msdn.microsoft.com/library/windows/hardware/hh975186)。 IrqlMmDispatch 规则指定驱动程序必须调用[MmFreeContiguousMemory](https://msdn.microsoft.com/library/windows/hardware/ff554503)仅当 IRQL = DISPATCH_LEVEL。|
|0x0002001B (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlObPassive](https://msdn.microsoft.com/library/windows/hardware/ff547873)。 IrqlObPassive 规则指定驱动程序必须调用[ObReferenceObjectByHandle](https://msdn.microsoft.com/library/windows/hardware/ff558679)仅当 IRQL = passive_level 调用。|
|0x0002001C (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlPsPassive](https://msdn.microsoft.com/library/windows/hardware/ff547882)。 IrqlPsPassive 规则指定，该驱动程序必须调用某些进程和线程管理器例程时，才 IRQL = passive_level 调用。|
|0x0002001D (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序违反 DDI 符合性规则[IrqlReturn](https://msdn.microsoft.com/library/windows/hardware/ff547886)。|
|0x0002001E (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlRtlPassive](https://msdn.microsoft.com/library/windows/hardware/ff547893)。 IrqlRtlPassive 规则指定驱动程序必须调用[RtlDeleteRegistryValue](https://msdn.microsoft.com/library/windows/hardware/ff561829)仅当 IRQL = passive_level 调用。|
|0x0002001F (Windows 8 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|规则的可选指针状态 variable(s)。|保留|该驱动程序违反 DDI 符合性规则[IrqlZwPassive](https://msdn.microsoft.com/library/windows/hardware/ff547897)。 IrqlZwPassive 规则指定驱动程序必须调用[ZwClose](https://msdn.microsoft.com/library/windows/hardware/ff566417)仅当 IRQL = passive_level 调用。|
|0x00020022 (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|保留 （未使用）|保留 （未使用）|该驱动程序违反 DDI 符合性规则[IrqlIoDispatch](https://msdn.microsoft.com/library/windows/hardware/jj157234)。|
|0x00040003 (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序违反 DDI 符合性规则[CriticalRegions](https://msdn.microsoft.com/library/windows/hardware/ff543603)。|
|0x00040006 (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序违反 DDI 符合性规则[QueuedSpinLock](https://msdn.microsoft.com/library/windows/hardware/ff551494)。|
|0x00040007 (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序违反 DDI 符合性规则[QueuedSpinLockRelease](https://msdn.microsoft.com/library/windows/hardware/ff551496)。|
|0x00040009 (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序违反 DDI 符合性规则[SpinLock](https://msdn.microsoft.com/library/windows/hardware/ff551861)。|
|0x0004000B (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序违反 DDI 符合性规则[SpinlockRelease](https://msdn.microsoft.com/library/windows/hardware/ff552780)。|
|0x0004000E (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序违反 DDI 符合性规则[GuardedRegions](https://msdn.microsoft.com/library/windows/hardware/hh975150)。|
|0x0004100B (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|保留|保留|该驱动程序违反 DDI 符合性规则[RequestedPowerIrp](https://msdn.microsoft.com/library/windows/hardware/ff551613)。|
|0x0004100F (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序违反 DDI 符合性规则[IoSetCompletionExCompleteIrp](https://msdn.microsoft.com/library/windows/hardware/hh975178)。|
|0x00043006 (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|保留|保留|该驱动程序违反 DDI 符合性规则[PnpRemove](https://msdn.microsoft.com/library/windows/hardware/dn322052)。|
|0x00091001 (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序违反 DDI 符合性规则[NdisOidComplete](https://msdn.microsoft.com/library/windows/hardware/dn305115)。|
|0x00091002 (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序违反 DDI 符合性规则[NdisOidDoubleComplete](https://msdn.microsoft.com/library/windows/hardware/dn305116)。|
|0x0009100E (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序违反 DDI 符合性规则[NdisOidDoubleRequest](https://msdn.microsoft.com/library/windows/hardware/dn305117)。|
|0x00092003 (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序 NDIS/WIFI 验证规则冲突[NdisTimedOidComplete](https://msdn.microsoft.com/library/windows/hardware/dn305120)。|
|0x0009200D (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序 NDIS/WIFI 验证规则冲突[NdisTimedDataSend](https://msdn.microsoft.com/library/windows/hardware/dn305119)。|
|0x0009200F (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序 NDIS/WIFI 验证规则冲突[NdisTimedDataHang](https://msdn.microsoft.com/library/windows/hardware/dn305118)。|
|0x00093004 (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序 NDIS/WIFI 验证规则冲突[WlanAssociation](https://msdn.microsoft.com/library/windows/hardware/dn305122)。|
|0x00093005 (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序 NDIS/WIFI 验证规则冲突[WlanConnectionRoaming](https://msdn.microsoft.com/library/windows/hardware/dn305123)。|
|0x00093006 (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序 NDIS/WIFI 验证规则冲突[WlanDisassociation](https://msdn.microsoft.com/library/windows/hardware/dn305124)。|
|0x00094007 (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序 NDIS/WIFI 验证规则冲突[WlanTimedAssociation](https://msdn.microsoft.com/library/windows/hardware/dn305125)。|
|0x00094008 (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序 NDIS/WIFI 验证规则冲突[WlanTimedConnectionRoaming](https://msdn.microsoft.com/library/windows/hardware/dn305126)。|
|0x00094009 (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序 NDIS/WIFI 验证规则冲突[WlanTimedConnectRequest](https://msdn.microsoft.com/library/windows/hardware/dn305127)。|
|0x0009400B (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序 NDIS/WIFI 验证规则冲突[WlanTimedLinkQuality](https://msdn.microsoft.com/library/windows/hardware/dn305128)。|
|0x0009400C (Windows 8.1 操作系统及更高版本)|指向描述违反的规则条件的字符串指针。|地址的内部规则状态 (第二个参数为 ！ ruleinfo)。|补充状态的地址 (第三个参数 ！ ruleinfo)。|该驱动程序 NDIS/WIFI 验证规则冲突[WlanTimedScan](https://msdn.microsoft.com/library/windows/hardware/dn305129)。|




<a name="cause"></a>原因
-----

请参阅每个代码的原因说明的 Parameters 节中的说明。 可以通过使用获取详细信息[ **！ 分析-v** ](-analyze.md)扩展。

<a name="resolution"></a>分辨率
----------

当驱动程序验证程序已指示，若要监视一个或多个驱动程序时，才会发生此错误检查。 如果您不打算使用驱动程序验证程序，应停用它。 此外可以考虑删除驱动程序导致此问题。

如果你是驱动程序编写器，使用通过此 bug 检查获取的信息以在代码中修复的错误。

有关驱动程序验证程序的完整详细信息，请参阅[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)部分的 Windows Driver Kit (WDK)。

<a name="remarks"></a>备注
-------

\_池\_Ntddk.h 中枚举类型代码。 具体而言， **0** （零） 指示非分页缓冲的池并**1** （一个） 指示页面缓冲的池。

*（Windows 8 和更高版本的 Windows）* 如果[DDI 符合性检查](https://msdn.microsoft.com/library/windows/hardware/hh454208)导致的 bug 检查，运行[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)于驱动程序源代码，并指定 DDI 符合性规则 （由参数 1 值标识） 导致错误检查。 Static Driver Verifier 可帮助您在源代码中找到问题的原因。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[在启用驱动程序验证程序的情况下处理 Bug 检查](handling-a-bug-check-when-driver-verifier-is-enabled.md)

 

 




