---
title: Bug 检查 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION
description: DRIVER_VERIFIER_DETECTED_VIOLATION bug 检查的值为0x000000C4。 这是驱动程序验证程序发现的致命错误的一般 bug 检查代码。
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
ms.openlocfilehash: ea60a93b1725363924af5797720d21cadb4c07e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837989"
---
# <a name="bug-check-0xc4-driver_verifier_detected_violation"></a>Bug 检查0xC4：检测到\_冲突的驱动程序\_验证程序\_


检测到\_冲突 bug 检查的驱动程序\_验证程序\_的值为0x000000C4。 这是驱动程序验证程序发现的致命错误的一般 bug 检查代码。 有关详细信息，请参阅[在启用驱动程序验证程序时处理 Bug 检查](handling-a-bug-check-when-driver-verifier-is-enabled.md)。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="driver_verifier_detected_violation-parameters"></a>检测到\_验证程序\_的驱动程序\_冲突参数


参数1标识冲突类型。 其余参数的含义因参数1的值而异。 下表对参数值进行了说明。

**请注意**  查看此表中的所有5列时遇到问题，请尝试以下操作：
-   将浏览器窗口展开为完整大小。
-   将光标放在表中，并使用箭头键向左和向右滚动。
 
|参数 1|参数2|参数3|参数4|错误的原因|
|--- |--- |--- |--- |--- |
|0x00|当前 IRQL|池类型|0|驱动程序请求了零字节的池分配。|
|0x01|当前 IRQL|池类型|分配大小（以字节为单位）|驱动程序尝试分配分页内存，并 > APC_LEVEL。|
|0x02|当前 IRQL|池类型|分配大小（以字节为单位）|驱动程序尝试以 IRQL > DISPATCH_LEVEL 分配非分页内存。|
|0x10|地址错误|0|0|驱动程序尝试释放未从分配调用返回的地址。|
|0x11|当前 IRQL|池类型|池地址|驱动程序尝试将 > APC_LEVEL 的 IRQL 释放页面缓冲池。|
|0x12|当前 IRQL|池类型|池地址|驱动程序尝试 > DISPATCH_LEVEL 的 IRQL 释放非分页池。|
|0x13 或0x14|保留|指向池标头的指针|池标头内容|驱动程序尝试释放已释放的内存池。|
|0x16|保留|池地址|0|驱动程序尝试在错误的地址释放池，或驱动程序将无效参数传递给了内存例程。|
|0x30|当前 IRQL|请求的 IRQL|0|驱动程序向[KeRaiseIrql](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)传递了无效参数。 （参数的值低于当前 IRQL，或大于 HIGH_LEVEL 的值。 这可能是使用未初始化的参数的结果。）|
|0x31|当前 IRQL|请求的 IRQL|0：新的 IRQL 错误1：新的 IRQL 在 DPC 例程内无效|驱动程序向[KeLowerIrql](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql~r1)传递了无效参数。 （参数的值大于当前的 IRQL，或大于 HIGH_LEVEL 的值。 这可能是使用未初始化的参数的结果。）|
|0x32|当前 IRQL|旋转锁地址|0|该驱动程序在 DISPATCH_LEVEL 以外的 IRQL 处调用[KeReleaseSpinLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock) 。 （这可能是由于旋转锁的双释放导致的。）|
|0x33|当前 IRQL|快速 mutex 地址|0|驱动程序尝试以 IRQL > APC_LEVEL 获取 fast mutex。|
|0x34 赋|当前 IRQL|快速 mutex 地址|0|驱动程序尝试以 APC_LEVEL 之外的 IRQL 释放快速 mutex。|
|0x35|当前 IRQL|旋转锁地址|旧 IRQL|内核释放的自旋锁的 IRQL 不等于 DISPATCH_LEVEL。|
|0x36|当前 IRQL|旋转锁定号|旧 IRQL|内核释放的排队自旋锁的 IRQL 不等于 DISPATCH_LEVEL。|
|0x37|当前 IRQL|线程 APC 禁用计数|资源|驱动程序试图获取资源，但 Apc 未被禁用。|
|0x38|当前 IRQL|线程 APC 禁用计数|资源|驱动程序尝试释放资源，但 Apc 未被禁用。|
|0x39|当前 IRQL|线程 APC 禁用计数|终端|驱动程序尝试获取互斥体 "unsafe"，它在输入时不等于 APC_LEVEL。|
|0x3A|当前 IRQL|线程 APC 禁用计数|终端|驱动程序尝试释放不等于 APC_LEVEL on entry 的互斥体 "unsafe"。|
|0x3C|传递给例程的句柄|对象类型|0|驱动程序调用[ObReferenceObjectByHandle](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)时使用了错误的句柄。|
|0x3D|0|0|错误资源的地址|驱动程序将错误（未对齐）资源传递到[ExAcquireResourceExclusive](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)。|
|0x3E|0|0|0|对于当前不在关键区域中的线程，驱动程序调用[KeLeaveCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion) 。|
|0x3F|对象地址|新的对象引用计数。 -1：取消引用 case 1：引用大小写|0|驱动程序将[ObReferenceObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)应用到引用计数为零的对象，[或者将该驱动程序应用到](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)引用计数为零的对象。|
|0x40|当前 IRQL|旋转锁地址|0|驱动程序名为[KeAcquireSpinLockAtDpcLevel](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel) ，其名称为 IRQL < DISPATCH_LEVEL。|
|0x41 向|当前 IRQL|旋转锁地址|0|驱动程序名为[KeReleaseSpinLockFromDpcLevel](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel) ，其名称为 IRQL < DISPATCH_LEVEL。|
|0x42|当前 IRQL|旋转锁地址|0|驱动程序名为[KeAcquireSpinLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) ，其名称为 IRQL > DISPATCH_LEVEL。|
|0x51|分配的基址|超出分配的引用的地址|收费字节数|驱动程序在写入超过分配末尾后，尝试释放内存。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x52|分配的基址|保留|收费字节数|驱动程序在写入超过分配末尾后，尝试释放内存。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x53、0x54 或0x59|分配的基址|保留|保留|驱动程序在写入超过分配末尾后，尝试释放内存。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x60|从分页池分配的字节数|从非分页池分配的字节数|未释放的分配总数|卸载驱动程序时，不首先释放其池分配。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x61|从分页池分配的字节数|从非分页池分配的字节数|未释放的分配总数|驱动程序正在卸载时，驱动程序线程正在尝试分配池内存。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x62|驱动程序名称|保留|未释放的总分配数，包括分页池和非分页池|卸载驱动程序时，不首先释放其池分配。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x70|当前 IRQL|MDL 地址|访问模式|驱动程序名为[MmProbeAndLockPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages) ，其名称为 IRQL > DISPATCH_LEVEL。|
|0x71|当前 IRQL|MDL 地址|进程地址|驱动程序名为 MmProbeAndLockProcessPages，其名称为 IRQL > DISPATCH_LEVEL。|
|0x72|当前 IRQL|MDL 地址|进程地址|驱动程序名为 MmProbeAndLockSelectedPages，其名称为 IRQL > DISPATCH_LEVEL。|
|0x73|当前 IRQL|在32位 Windows 中：64位 Windows 中物理地址的低32位：64位物理地址|字节数|驱动程序名为[MmMapIoSpace](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace) ，其名称为 IRQL > DISPATCH_LEVEL。|
|0x74|当前 IRQL|MDL 地址|访问模式|在内核模式下名为[MmMapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages)的驱动程序 > DISPATCH_LEVEL 的内核模式。|
|0x75|当前 IRQL|MDL 地址|访问模式|在用户模式下名为[MmMapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages)的驱动程序以 IRQL > APC_LEVEL 为依据。|
|0x76|当前 IRQL|MDL 地址|访问模式|在内核模式下名为[MmMapLockedPagesSpecifyCache](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache)的驱动程序 > DISPATCH_LEVEL 的内核模式。|
|0x77|当前 IRQL|MDL 地址|访问模式|在用户模式下名为[MmMapLockedPagesSpecifyCache](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache)的驱动程序以 IRQL > APC_LEVEL 为依据。|
|0x78|当前 IRQL|MDL 地址|0|驱动程序名为[MmUnlockPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages) ，其名称为 IRQL > DISPATCH_LEVEL。|
|0x79|当前 IRQL|正在取消映射的虚拟地址|MDL 地址|在内核模式下名为[MmUnmapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmaplockedpages)的驱动程序 > DISPATCH_LEVEL 的内核模式。|
|0x7A|当前 IRQL|正在取消映射的虚拟地址|MDL 地址|在用户模式下名为[MmUnmapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmaplockedpages)的驱动程序以 IRQL > APC_LEVEL 为依据。|
|0x7B|当前 IRQL|正在取消映射的虚拟地址|字节数|驱动程序名为[MmUnmapIoSpace](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace) ，其名称为 IRQL > APC_LEVEL。|
|0x7C|MDL 地址|MDL 标志|0|驱动程序调用[MmUnlockPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)，并通过其页从未成功锁定的 MDL。|
|0x7D|MDL 地址|MDL 标志|0|驱动程序调用[MmUnlockPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)，并通过其页面来自非分页池的 MDL。 （这些应永远不会解除锁定。）|
|0x7E|当前 IRQL|DISPATCH_LEVEL|0|名为[MmAllocatePagesForMdl](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdl)、 [MmAllocatePagesForMdlEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdlex)或[MMFREEPAGESFROMMDL](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreepagesfrommdl)的驱动程序 > DISPATCH_LEVEL。|
|0x7F|当前 IRQL|MDL 地址|MDL 标志|该驱动程序调用[BuildMdlForNonPagedPool](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool) ，并传递其页面来自页面缓冲池的 MDL。|
|0x80|当前 IRQL|事件地址|0|驱动程序名为[KeSetEvent](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent) ，其名称为 IRQL > DISPATCH_LEVEL。|
|0x81|MDL 地址|MDL 标志|0|称为[MmMapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages)的驱动程序。 （应改用[MmMapLockedPagesSpecifyCache](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache) ，并将 BugCheckOnFailure 参数设置为 FALSE。）|
|0x82|MDL 地址|MDL 标志|0|驱动程序调用[MmMapLockedPagesSpecifyCache](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache) ，BugCheckOnFailure 参数等于 TRUE。 （此参数应设置为 FALSE。）|
|0x83|要映射的物理地址范围的开头|要映射的字节数|未锁定的第一个页面框架编号|驱动程序调用[MmMapIoSpace](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace) ，但未锁定 MDL 页面。 在进行此调用之前，必须锁定由要映射的物理地址范围表示的物理页面。|
|0x85|MDL 地址|要映射的页数|未锁定的第一个页面框架编号|驱动程序调用[MmMapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages) ，但未锁定 MDL 页面。|
|0x89|MDL 地址|指向 MDL 中的非内存页的指针|MDL 中的非内存页码|MDL 未标记为 "i/o"，但它包含非内存页面地址。|
|0x91|保留|保留|保留|驱动程序使用操作系统不支持的方法交换堆栈。 扩展内核模式堆栈的唯一受支持的方法是使用[KeExpandKernelStackAndCallout](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keexpandkernelstackandcallout)。|
|0xA0 （仅限 Windows Server 2003 和更高版本的操作系统）|一个指针，指向用于进行读取或写入请求的 IRP|较低设备的设备对象|检测到错误的扇区数|在硬盘上检测到循环冗余检查（CRC）错误。 仅当驱动程序验证程序的磁盘完整性检查选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0xA1 （仅限 Windows Server 2003 和更高版本的操作系统）|进行读取或写入请求的 IRP 副本。 （实际 IRP 已经完成。）|较低设备的设备对象|检测到错误的扇区数|在扇区上检测到 CRC 错误（异步）。 仅当驱动程序验证程序的磁盘完整性检查选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0xA2 （仅限 Windows Server 2003 和更高版本的操作系统）|创建读取或写入请求的 IRP，或此 IRP 的副本|较低设备的设备对象|检测到错误的扇区数|CRCDISK 校验和副本不匹配。 这可能是分页错误。 仅当驱动程序验证程序的磁盘完整性检查选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0xB0 （仅适用于 Windows Vista 和更高版本的操作系统）|MDL 地址|MDL 标志|MDL 标志不正确|对于具有错误标志的 MDL，驱动程序调用[MmProbeAndLockPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages) 。 例如，驱动程序将[MmBuildMdlForNonPagedPool](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool)创建的 MDL 传递到 MmProbeAndLockPages。|
|0xB1 （仅适用于 Windows Vista 和更高版本的操作系统）|MDL 地址|MDL 标志|MDL 标志不正确|对于具有错误标志的 MDL，驱动程序调用 MmProbeAndLockProcessPages。 例如，驱动程序将[MmBuildMdlForNonPagedPool](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool)创建的 MDL 传递到 MmProbeAndLockProcessPages。|
|0xB2 （仅适用于 Windows Vista 和更高版本的操作系统）|MDL 地址|MDL 标志|MDL 标志不正确|对于具有错误标志的 MDL，驱动程序调用[MmMapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages) 。 例如，驱动程序通过了已映射到系统地址或未锁定到 MmMapLockedPages 的 MDL。|
|0xB3 （仅适用于 Windows Vista 和更高版本的操作系统）|MDL 地址|MDL 标志|缺少 MDL 标志（应该至少有一个）|对于具有错误标志的 MDL，驱动程序调用[MmMapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages) 。 例如，驱动程序将一个未锁定的 MDL 传递到 MmMapLockedPages。|
|0xB4 （仅适用于 Windows Vista 和更高版本的操作系统）|MDL 地址|MDL 标志|意外的部分 MDL 标志|部分 MDL 的驱动程序调用[MmUnlockPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages) 。 部分 MDL 是由[IoBuildPartialMdl](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl)创建的 MDL。|
|0xB8 （仅适用于 Windows Vista 和更高版本的操作系统）|MDL 地址|MDL 标志|保留|MDL 描述的页面仍已映射。 在调用 IoFreeMdl 之前，驱动程序必须取消页面映射。|
|0xC0 （仅适用于 Windows Vista 和更高版本的操作系统）|IRP 的地址|保留|保留|已禁用中断的驱动程序调用[IoCallDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 。|
|0xC1 （仅适用于 Windows Vista 和更高版本的操作系统）|驱动程序调度例程的地址|保留|保留|返回了驱动程序调度例程，并禁用了中断。|
|0xC2 （仅适用于 Windows Vista 和更高版本的操作系统）|保留|保留|保留|禁用中断后，该驱动程序称为快速 i/o 调度例程。|
|0xC3 （仅适用于 Windows Vista 和更高版本的操作系统）|驱动程序快速 i/o 调度例程的地址|保留|保留|返回驱动程序快速 i/o 调度例程，并禁用中断。|
|0xC5 （仅适用于 Windows Vista 和更高版本的操作系统）|驱动程序调度例程的地址|当前线程的 APC 禁用计数|调用驱动程序调度例程之前线程的 APC 禁用计数|驱动程序调度例程已更改线程的 APC 禁用计数。 每次驱动程序调用[KeEnterCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)、 [FsRtlEnterFileSystem](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlenterfilesystem)或获取互斥体时，APC 禁用计数都将减少。 每次驱动程序调用[KeLeaveCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)、 [KeReleaseMutex](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex)或[FsRtlExitFileSystem](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlexitfilesystem)时，APC 禁用计数都将递增。 由于这些调用应始终成对出现，因此每当退出线程时，APC 禁用计数都应为零。 负值表示驱动程序已禁用 APC 调用，而无需重新启用它们。 正值指示反转为 true。|
|0xC6 （仅适用于 Windows Vista 和更高版本的操作系统）|驱动程序快速 i/o 调度例程的地址|当前线程的 APC 禁用计数|调用 Fast i/o 驱动程序调度例程之前线程的 APC 禁用计数|驱动程序快速 i/o 调度例程已更改线程的 APC 禁用计数。 每次驱动程序调用[KeEnterCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)、 [FsRtlEnterFileSystem](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlenterfilesystem)或获取互斥体时，APC 禁用计数都将减少。 每次驱动程序调用[KeLeaveCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)、 [KeReleaseMutex](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex)或[FsRtlExitFileSystem](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlexitfilesystem)时，APC 禁用计数都将递增。 由于这些调用应始终成对出现，因此每当退出线程时，APC 禁用计数都应为零。 负值表示驱动程序已禁用 APC 调用，而无需重新启用它们。 正值指示反转为 true。|
|码0xca （仅适用于 Windows Vista 和更高版本的操作系统）|后备链表列表的地址|保留|保留|驱动程序已尝试重新初始化后备链表列表。|
|0xCB （仅适用于 Windows Vista 和更高版本的操作系统）|后备链表列表的地址|保留|保留|驱动程序已尝试删除未初始化的后备链表列表。|
|0xCC （仅适用于 Windows Vista 和更高版本的操作系统）|后备链表列表的地址|池分配的起始地址|池分配的大小|驱动程序已尝试释放包含活动后备链表列表的池分配。|
|0xCD （仅适用于 Windows Vista 和更高版本的操作系统）|后备链表列表的地址|调用方指定的块大小|支持的最小块大小|驱动程序尝试创建的后备链表列表的分配块大小太小。|
|0xD0 （仅适用于 Windows Vista 和更高版本的操作系统）|ERESOURCE 结构的地址|保留|保留|驱动程序已尝试重新初始化 ERESOURCE 结构。|
|0xD1 （仅适用于 Windows Vista 和更高版本的操作系统）|ERESOURCE 结构的地址|保留|保留|驱动程序已尝试删除未初始化的 ERESOURCE 结构。|
|0xD2 （仅适用于 Windows Vista 和更高版本的操作系统）|ERESOURCE 结构的地址|池分配的起始地址|池分配的大小|驱动程序已尝试释放包含活动 ERESOURCE 结构的池分配。|
|0xD5 （仅适用于 Windows Vista 和更高版本的操作系统）|由所选版本的驱动程序创建的 IO_REMOVE_LOCK 结构的地址|当前[IoReleaseRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)标记|保留|当前[IoReleaseRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)标记与上一个[IoAcquireRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)标记不匹配。 如果调用 IoReleaseRemoveLock 的驱动程序不在已检查的内部版本中，则参数2为驱动程序验证程序代表驱动程序创建的阴影 IO_REMOVE_LOCK 结构的地址。 在这种情况下，驱动程序使用的 IO_REMOVE_LOCK 结构的地址根本不使用，因为驱动程序验证器将替换所有删除锁定 Api 的锁定地址。 仅当驱动程序验证程序的 i/o 验证选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0xD6 （仅适用于 Windows Vista 和更高版本的操作系统）|由所选版本的驱动程序创建的 IO_REMOVE_LOCK 结构的地址|与上一个[IoAcquireRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)标记不匹配的标记|上一个[IoAcquireRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)标记|当前[IoReleaseRemoveLockAndWait](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)标记与上一个[IoAcquireRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)标记不匹配。 如果调用[IoReleaseRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)的驱动程序不是已检查的生成，则参数2为驱动程序验证器代表驱动程序创建的阴影 IO_REMOVE_LOCK 结构的地址。 在这种情况下，驱动程序使用的 IO_REMOVE_LOCK 结构的地址根本不使用，因为驱动程序验证器将替换所有删除锁定 Api 的锁定地址。 仅当驱动程序验证程序的 i/o 验证选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0xD7 （仅适用于 Windows 7 操作系统和更高版本）|驱动程序验证程序内部使用的已检查生成删除锁定结构的地址|驱动程序指定的移除锁结构的地址|保留|即使删除锁调用了[IoReleaseRemoveLockAndWait](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)，也不能对其重新初始化，因为其他线程可能仍在使用该锁（通过调用[IoAcquireRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)）。 驱动程序应在其设备扩展内分配删除锁定，并对其进行一次初始化。 锁定将与设备扩展一起删除。|
|0xDA （仅适用于 Windows Vista 和更高版本的操作系统）|驱动程序的起始地址|驱动程序中的 WMI 回调地址|保留|尝试卸载未取消注册其 WMI 回调函数的驱动程序。|
|0xDB （仅适用于 Windows Vista 和更高版本的操作系统）|设备对象的地址|保留|保留|尝试删除未从 WMI 取消注册的设备对象。|
|0xDC （仅适用于 Windows Vista 和更高版本的操作系统）|保留|保留|保留|指定了无效的 RegHandle 值作为函数[EtwUnregister](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-etwunregister)的参数。|
|0xDD （仅适用于 Windows Vista 和更高版本的操作系统）|调用 EtwRegister 的地址|卸载驱动程序的起始地址|对于 Windows 8 及更高版本，此参数是 ETW RegHandle 值。|尝试在不调用[EtwUnregister](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-etwunregister)的情况下卸载驱动程序。|
|0xDF （仅适用于 Windows 7 操作系统和更高版本）|同步对象地址|同步对象处于会话地址空间中。 不允许在会话地址空间中使用同步对象，因为它们可以从其他会话或没有会话虚拟地址空间的系统线程进行操作。|
|0xE0 （仅适用于 Windows Vista 和更高版本的操作系统）|用作参数的用户模式地址|用作参数的地址范围的大小（以字节为单位）|保留|调用了将用户模式地址指定为参数的操作系统内核函数。|
|0xE1 （仅适用于 Windows Vista 和更高版本的操作系统）|同步对象的地址|保留|保留|发现同步对象具有无效或可分页的地址。|
|0xE2 （仅适用于 Windows Vista 和更高版本的操作系统）|IRP 的地址|IRP 中存在的用户模式地址|保留|发现使用 Irp > Irp->requestormode 设置为 KernelMode 的 IRP 将用户模式地址作为其成员之一。|
|0xE3 （仅适用于 Windows Vista 和更高版本的操作系统）|对 API 的调用的地址|用作 API 中的参数的用户模式地址|保留|驱动程序已调用使用用户模式地址作为参数的内核模式 ZwXxx 例程。|
|0xE4 （仅适用于 Windows Vista 和更高版本的操作系统）|对 API 的调用的地址|格式错误的 UNICODE_STRING 结构的地址|保留|驱动程序已调用将格式不正确的 UNICODE_STRING 结构作为参数的内核模式 ZwXxx 例程。|
|0xE5 （仅适用于 Windows Vista 和更高版本的操作系统）|当前 IRQL|保留|保留|对内核 API 进行的调用出现错误的 IRQL。|
|0xE6 （仅适用于 Windows Vista 和更高版本的操作系统）|发出 Zw API 调用的驱动程序中的地址|当前 IRQL|特殊内核 Apc。|未在 IRQL = PASSIVE_LEVEL 和启用了特殊内核 Apc 的情况调用内核 Zw API。|
|0xEA （仅适用于 Windows Vista 和更高版本的操作系统）|当前 IRQL|线程的 APC 禁用计数|Pushlock 的地址|当启用 Apc 时，驱动程序已尝试获取 pushlock。|
|0xEB （仅适用于 Windows Vista 和更高版本的操作系统）|当前 IRQL|线程的 APC 禁用计数|Pushlock 的地址|当启用 Apc 时，驱动程序已尝试发布 pushlock。|
|0xF0 （仅适用于 Windows Vista 和更高版本的操作系统）|目标缓冲区的地址|源缓冲区的地址|要复制的字节数|一个名为 memcpy 函数的驱动程序，其中包含重叠的源和目标缓冲区。|
|0xF5 （仅适用于 Windows Vista 和更高版本的操作系统）|NULL 句柄的地址|对象类型|保留|驱动程序将空句柄传递到[ObReferenceObjectByHandle](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)。|
|0xF6 （Windows 7 操作系统和更高版本）|正在引用的句柄值|当前进程的地址|执行错误引用的驱动程序中的地址|驱动程序将用户模式句柄作为内核模式引用。|
|0xF7 （Windows 7 操作系统和更高版本）|调用方指定的句柄值|调用方指定的对象类型|调用方指定的 AccessMode|驱动程序在系统进程的上下文中尝试使用内核句柄的用户模式引用。|
|0xFA （Windows 7 操作系统和更高版本）|完成例程地址。|IRQL 值，然后再调用完成例程|当前 IRQL 值，在调用完成例程后|IRP 完成例程返回的 IRQL 不同于调用例程的 irql。|
|0xFB （Windows 7 操作系统和更高版本）|完成例程地址|当前线程的 APC 禁用计数|线程的 APC 禁用计数，然后再调用 IRP 完成例程|此线程的 APC 禁用计数已由驱动程序的 IRP 完成例程更改。 每次驱动程序调用[KeEnterCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)、 [FsRtlEnterFileSystem](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlenterfilesystem)或获取互斥体时，APC 禁用计数都将减少。 每次驱动程序调用[KeLeaveCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)、 [KeReleaseMutex](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex)或[FsRtlExitFileSystem](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlexitfilesystem)时，APC 禁用计数都将递增。 由于这些调用应始终成对出现，因此每当退出线程时，APC 禁用计数都应为零。 负值表示驱动程序已禁用 APC 调用，而无需重新启用它们。 正值指示反转为 true。|
|0x105 （Windows 7 操作系统和更高版本）|IRP 的地址|驱动程序使用 ExFreePool 而不是 IoFreeIrp 来释放 IRP。|
|0x10A （Windows 7 操作系统和更高版本）|驱动程序尝试将池配额计费到空闲进程。|
|0x10B （Windows 7 操作系统和更高版本）|驱动程序尝试从 DPC 例程对池配额计费。 这是不正确的，因为当前进程上下文未定义。|
|0x110 （Windows 7 操作系统和更高版本）|中断服务例程的地址|在执行 ISR 之前保存的扩展上下文的地址|扩展上下文的地址在执行 ISR 后保存|驱动程序的中断服务例程（ISR）已损坏扩展线程上下文。|
|0x111 （Windows 7 操作系统和更高版本）|中断服务例程的地址|执行 ISR 之前的 IRQL|执行 ISR 后的 IRQL|中断服务例程返回了已更改的 IRQL。|
|0x115 （Windows 7 操作系统和更高版本）|负责关闭的线程的地址，可能是死锁|驱动程序验证程序检测到系统已超过20分钟并且关闭未完成。|
|0x11A （Windows 7 操作系统和更高版本）|当前 IRQL|驱动程序调用 KeEnterCriticalRegion，APC_LEVEL >。|
|0x11B （Windows 7 操作系统和更高版本）|当前 IRQL|驱动程序调用 KeLeaveCriticalRegion，APC_LEVEL >。|
|0x120 （Windows 7 操作系统和更高版本）|IRQL 值的地址|要等待的对象的地址|超时值的地址|线程 > DISPATCH_LEVEL 以 IRQL 进行等待。 KeWaitForSingleObject 或 KeWaitForMultipleObjects 的调用方必须以 IRQL < = DISPATCH_LEVEL 运行。|
|0x121 （Windows 7 操作系统和更高版本）|IRQL 值的地址|要等待的对象的地址|超时值的地址|线程等待 IRQL 等于 DISPATCH_LEVEL，超时值为 NULL。 KeWaitForSingleObject 或 KeWaitForMultipleObjects 的调用方可以在 IRQL < = DISPATCH_LEVEL 上运行。 如果为超时提供了空指针，则调用线程将保持等待状态，直到终止对象。|
|0x122 （Windows 7 操作系统和更高版本）|IRQL 值的地址|要等待的对象的地址|超时值的地址|线程等待 DISPATCH_LEVEL，超时值不等于零（0）。 如果 Timeout！ = 0，则 KeWaitForSingleObject 或 KeWaitForMultipleObjects 的调用方必须以 IRQL < = APC_LEVEL 运行。|
|0x123 （Windows 7 操作系统和更高版本）|要等待的对象的地址|KeWaitForSingleObject 或 KeWaitForMultipleObjects 的调用方将 wait 指定为 UserMode，但该对象在内核堆栈上。|
|0x130 （Windows 7 操作系统和更高版本）|工作项的地址|工作项在会话地址空间中。 会话地址空间中不允许使用工作项，因为它们可以从其他会话或没有会话虚拟地址空间的系统线程进行操作。|
|0x131 （Windows 7 操作系统和更高版本）|工作项的地址|工作项位于可分页内存中。 工作项必须位于不可分页的内存中，因为内核在 DISPATCH_LEVEL 中使用它们。|
|0x135|IRP 的地址|[IoCancelIrp](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)调用与此 IRP 的完成之间允许的毫秒数|在预期时间内，已取消的 IRP 未完成，驱动程序所用时间比预期时间长，无法完成取消的 IRP。|
|0x13A|正在释放的池块的地址|值不正确|不正确的值的地址|驱动程序调用了[ExFreePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) ，驱动程序验证器在用于跟踪池使用情况的某个内部值中检测到错误。|
|0x13B|正在释放的池块的地址|不正确的值的地址|指向错误内存页的指针的地址|驱动程序调用了[ExFreePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) ，驱动程序验证器在用于跟踪池使用情况的某个内部值中检测到错误。|
|0x13C|正在释放的池块的地址|值不正确|不正确的值的地址|驱动程序调用了[ExFreePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) ，驱动程序验证器在用于跟踪池使用情况的某个内部值中检测到错误。|
|0x13D|正在释放的池块的地址|不正确的值的地址|应为正确的值|驱动程序调用了[ExFreePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) ，驱动程序验证器在用于跟踪池使用情况的某个内部值中检测到错误。|
|0x13E|调用方指定的池块地址|驱动程序验证程序跟踪的池块地址|指向由驱动程序验证程序跟踪的池块地址的指针|[ExFreePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)的调用方指定的池块地址不同于 Driver Verifier 所跟踪的地址。|
|0x13F|正在释放的池块的地址|要释放的字节数|指向驱动程序验证器跟踪的字节数的指针|在对[ExFreePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)的调用中释放的内存字节数不同于 Driver Verifier 所跟踪的字节数。|
|0x140|当前 IRQL|MDL 地址|与此 MDL 关联的虚拟地址|非锁定 MDL 是从可分页或 tradable 内存构造的。|
|0x1000 |资源地址|保留|保留|自死锁：当前线程已尝试以递归方式获取资源。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x1001 |导致死锁的最后原因的资源的地址|保留|保留|死锁：发现锁层次结构冲突。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，才会发生带有此参数的 bug 检查。 （有关详细信息，请使用[！死锁](-deadlock.md)扩展。）|
|0x1002 |资源地址|保留|保留|未初始化的资源：在未首先初始化的情况下，已获取资源。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x1003 |被死锁的资源的地址|应该首先释放的资源的地址|保留|意外发布：按错误的顺序释放了资源。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x1004 |资源地址|获取资源的线程的地址|当前线程的地址|意外线程：错误的线程释放资源。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x1005 |资源地址|保留|保留|多次初始化：资源多次初始化。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x1007 |资源地址|保留|保留|Unacquired 资源：在获取资源之前释放资源。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x1008 相关联（Windows 7 操作系统和更高版本）|锁定地址|驱动程序验证程序内部数据|驱动程序验证程序内部数据|驱动程序尝试使用对此锁定类型不匹配的 API 来获取锁定。|
|0x1009 （Windows 7 操作系统和更高版本）|锁定地址|驱动程序验证程序内部数据|驱动程序验证程序内部数据|驱动程序尝试使用对此锁定类型不匹配的 API 来释放锁定。|
|0x100A （Windows 7 操作系统和更高版本）|所有者线程地址|驱动程序验证程序内部数据|终止的线程拥有该锁。|
|0x100B （Windows 7 操作系统和更高版本）|锁定地址|所有者线程地址|驱动程序验证程序内部地址|已删除的锁仍归线程所有。|
|0xA001 （Windows 8.1 操作系统及更高版本）|指向 NetBufferList 对象的指针|指向虚拟交换机对象的指针（如果非 NULL）|已保留（未使用）|VM 交换机：必须设置调用方提供的 NetBufferList 的 SourceHandle。 请参阅[AllocateNetBufferListForwardingContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)例程。|
|0xA002 （Windows 8.1 操作系统及更高版本）|指向 NetBufferList 对象的指针|指向虚拟交换机对象的指针（如果非 NULL）。|已保留（未使用）|VM 交换机：调用方提供的 NetBufferList 转发详细信息不为零。 请参阅[AllocateNetBufferListForwardingContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)例程。|
|0xA003 （Windows 8.1 操作系统及更高版本）|指向 NetBufferList 对象的指针|指向虚拟交换机对象的指针（如果非 NULL）。|已保留（未使用）|VM 交换机：调用方提供的 NetBufferList 的数据包标头或路由上下文为空。 请参阅[可扩展交换机数据路径的数据包管理准则](https://docs.microsoft.com/windows-hardware/drivers/network/packet-management-guidelines-for-the-extensible-switch-data-path)。|
|0xA004 （Windows 8.1 操作系统及更高版本）|无效端口的 ID|NIC 索引|指向虚拟交换机对象的指针（如果非 NULL）。|VM 交换机：调用方指定了无效的端口和 NIC 索引组合。 请参阅[Hyper-v 可扩展交换机端口和网络适配器状态](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)。|
|0xA005 （Windows 8.1 操作系统及更高版本）|指向 NetBufferList 对象的指针|指向目标列表的指针。|指向虚拟交换机对象的指针（如果非 NULL）。|VM 交换机：调用方提供的目标无效。 请参阅[AddNetBufferListDestination](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)和[UpdateNetBufferListDestinations](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)。|
|0xA006 （Windows 8.1 操作系统及更高版本）|指向 NetBufferList 对象的指针|指向虚拟交换机对象的指针（如果非 NULL）。|已保留（未使用）|VM 交换机：调用方提供了无效的源 NIC 或端口对象。 请参阅[Hyper-v 可扩展交换机端口和网络适配器状态](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)。|
|0xA007 （Windows 8.1 操作系统及更高版本）|指向 NetBufferList 对象的指针|指向虚拟交换机对象的指针（如果非 NULL）。|已保留（未使用）|VM 交换机：调用方提供了无效的目标列表。 请参阅[AddNetBufferListDestination](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)和[UpdateNetBufferListDestinations](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)。|
|0xA008 （Windows 8.1 操作系统及更高版本）|父 NIC 对象|NIC 索引|指向虚拟交换机对象的指针（如果非 NULL）。|VM 交换机：尝试引用不允许的 NIC。 请参阅[Hyper-v 可扩展交换机端口和网络适配器状态](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)。|
|0xA009 （Windows 8.1 操作系统及更高版本）|正在引用的端口|指向虚拟交换机对象的指针（如果非 NULL）|已保留（未使用）|VM 交换机：不允许时，尝试引用端口。 请参阅[Hyper-v 可扩展交换机端口和网络适配器状态](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)。|
|0xA00A （Windows 8.1 操作系统及更高版本）|指向 NetBufferList 对象的指针|ContextTypeInfo 对象|已保留（未使用）|VM 交换机：故障上下文已设置。 请参阅[SetNetBufferListSwitchContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_set_net_buffer_list_switch_context)。|
|0xA00B （Windows 8.1 操作系统及更高版本）|指向 NetBufferList 对象的指针|NDIS_SWITCH_REPORT_FILTERED_NBL_FLAGS_*|指向虚拟交换机对象的指针（如果非 NULL）|VM 交换机：为删除的 NetBufferList 提供的方向无效。 请参阅[ReportFilteredNetBufferLists](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)。|
|0xA00C （Windows 8.1 操作系统及更高版本）|指向 NetBufferList 对象的指针|发送标志值|指向虚拟交换机对象的指针（如果非 NULL）|VM 交换机：设置 NDIS_SEND_FLAGS_SWITCH_SINGLE_SOURCE 标志时，NetBufferList 链具有多个源端口。 请参阅[Hyper-v 可扩展交换机发送和接收标志](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-send-and-receive-flags)。|
|0xA00D （Windows 8.1 操作系统及更高版本）|指向 NetBufferList 对象的指针|指向虚拟交换机上下文的指针|指向虚拟交换机对象的指针（如果非 NULL）|VM 交换机：设置 NDIS_RECEIVE_FLAGS_SWITCH_DESTINATION_GROUP 标志时，链中的一个或多个 NetBufferLists 的目标无效。 请参阅[Hyper-v 可扩展交换机发送和接收标志](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-send-and-receive-flags)。|
|0x2000 （Windows 7 操作系统和更高版本）|传递到[StorPortInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize)例程的第一个参数。 此参数是一个指针，指向在微型端口驱动程序的[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程的第一个参数中传递给微型端口驱动程序的驱动程序对象。|传递到[StorPortInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize)例程的第二个参数。 此参数是一个指针，指向在微型端口驱动程序的[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程的第二个参数中传递给微型端口驱动程序的操作系统的上下文信息。|保留|Storport 微型端口驱动程序向[StorPortInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize)例程传递了错误的参数（空指针）。|
|0x00020002 （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlApcLte](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlapclte)。 规则指定只有当 IRQL < = APC_LEVEL 时，驱动程序才能调用[ObGetObjectSecurity](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obgetobjectsecurity)和[ObReleaseObjectSecurity](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreleaseobjectsecurity) 。|
|0x00020003 （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlDispatch](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqldispatch)。 IrqlDispatch 规则指定只有当 IRQL = DISPATCH_LEVEL 时，驱动程序才能调用特定例程|
|0x00020004 （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlExAllocatePool](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexallocatepool)。 IrqlExAllocatePool 规则指定，仅当 < = DISPATCH_LEVEL 时，驱动程序才调用[ExAllocatePoolWithTag](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)和[ExAllocatePoolWithTagPriority](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority) 。|
|0x00020005 （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlExApcLte1](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexapclte1)。 IrqlExApcLte1 规则指定该驱动程序仅调用 ExAcquireFastMutex 和 ExTryToAcquireFastMutex，< = APC_LEVEL。|
|0x00020006 （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlExApcLte2](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。 IrqlExApcLte2 规则指定只有当 IRQL < = APC_LEVEL 时，驱动程序才调用特定例程。|
|0x00020007 （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlExApcLte3](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexapclte3)。 IrqlExApcLte3 规则指定只有当 IRQL < = APC_LEVEL 时，驱动程序才能调用特定的执行程序支持例程。|
|0x00020008 （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlExPassive](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexpassive)。 IrqlExPassive 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用特定的执行程序支持例程。|
|0x00020009 （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlIoApcLte](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlioapclte)。 IrqlIoApcLte 规则指定只有当 IRQL < = APC_LEVEL 时，驱动程序才能调用特定的 i/o 管理器例程。|
|0x0002000A （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlIoPassive1](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive1)。 IrqlIoPassive1 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用特定的 i/o 管理器例程。|
|0x0002000B （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlIoPassive2](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive2)。 IrqlIoPassive2 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用特定的 i/o 管理器例程。|
|0x0002000C （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlIoPassive3](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive3)。 IrqlIoPassive3 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用特定的 i/o 管理器例程。|
|0x0002000D （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlIoPassive4](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive4)。 IrqlIoPassive4 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用特定的 i/o 管理器例程。|
|0x0002000E （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlIoPassive5](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive5)。 IrqlIoPassive5 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用特定的 i/o 管理器例程。|
|0x0002000F （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlKeApcLte1](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkeapclte1)。 IrqlKeApcLte1 规则指定只有当 IRQL < = APC_LEVEL 时，驱动程序才能调用某些内核例程。|
|0x00020010 （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlKeApcLte2](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkeapclte2)。 IrqlKeApcLte2 规则指定只有当 IRQL < = APC_LEVEL 时，驱动程序才能调用某些内核例程。|
|0x00020011 （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlKeDispatchLte](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkedispatchlte)。 IrqlKeDispatchLte 规则指定只有当 IRQL < = DISPATCH_LEVEL 时，驱动程序才能调用某些内核例程。|
|0x00020015 （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlKeReleaseSpinLock](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkereleasespinlock)。 IrqlKeReleaseSpinLock 规则指定只有当 IRQL = DISPATCH_LEVEL 时，驱动程序才能调用 KeReleaseSpinLock。|
|0x00020016 （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlKeSetEvent](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkesetevent)。 IrqlKeSetEvent 规则指定，当 Wait 设置为 FALSE 时， [KeSetEvent](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)例程仅在 irql < = DISPATCH_LEVEL 上调用，而在 irql 设置为 TRUE 时则 < = APC_LEVEL。|
|0x00020019 （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlMmApcLte](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlmmapclte)。 IrqlMmApcLte 规则指定只有当 IRQL < = APC_LEVEL 时，驱动程序才能调用特定的内存管理器例程。|
|0x0002001A （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlMmDispatch](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlmmdispatch)。 IrqlMmDispatch 规则指定只有当 IRQL = DISPATCH_LEVEL 时，驱动程序才能调用[MmFreeContiguousMemory](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreecontiguousmemory) 。|
|0x0002001B （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlObPassive](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlobpassive)。 IrqlObPassive 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用[ObReferenceObjectByHandle](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle) 。|
|0x0002001C （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlPsPassive](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlpspassive)。 IrqlPsPassive 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用特定进程和线程管理器例程。|
|0x0002001D （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 DDI 相容性规则[IrqlReturn](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlreturn)。|
|0x0002001E （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlRtlPassive](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlrtlpassive)。 IrqlRtlPassive 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用[RtlDeleteRegistryValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtldeleteregistryvalue) 。|
|0x0002001F （Windows 8 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针。|保留|驱动程序违反了 DDI 相容性规则[IrqlZwPassive](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlzwpassive)。 IrqlZwPassive 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用[ZwClose](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose) 。|
|0x00020022 （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|已保留（未使用）|已保留（未使用）|驱动程序违反了 DDI 相容性规则[IrqlIoDispatch](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliodispatch)。|
|0x00040003 （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 DDI 相容性规则[CriticalRegions](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-criticalregions)。|
|0x00040006 （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 DDI 相容性规则[QueuedSpinLock](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-queuedspinlock)。|
|0x00040007 （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 DDI 相容性规则[QueuedSpinLockRelease](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-queuedspinlockrelease)。|
|0x00040009 （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 DDI 相容性规则[旋转锁](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-spinlock)。|
|0x0004000B （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 DDI 相容性规则[SpinlockRelease](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-spinlockrelease)。|
|0x0004000E （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 DDI 相容性规则[GuardedRegions](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-guardedregions)。|
|0x0004100B （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|保留|保留|驱动程序违反了 DDI 相容性规则[RequestedPowerIrp](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-requestedpowerirp)。|
|0x0004100F （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 DDI 相容性规则[IoSetCompletionExCompleteIrp](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-iosetcompletionexcompleteirp)。|
|0x00043006 （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|保留|保留|驱动程序违反了 DDI 相容性规则[PnpRemove](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-pnpremove)。|
|0x00091001 （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 DDI 相容性规则[NdisOidComplete](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoidcomplete)。|
|0x00091002 （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 DDI 相容性规则[NdisOidDoubleComplete](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoiddoublecomplete)。|
|0x0009100E （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 DDI 相容性规则[NdisOidDoubleRequest](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoiddoublerequest)。|
|0x00092003 （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 NDIS/WIFI 验证规则[NdisTimedOidComplete](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimedoidcomplete)。|
|0x0009200D （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 NDIS/WIFI 验证规则[NdisTimedDataSend](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimeddatasend)。|
|0x0009200F （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 NDIS/WIFI 验证规则[NdisTimedDataHang](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimeddatahang)。|
|0x00093004 （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 NDIS/WIFI 验证规则[WlanAssociation](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlanassociation)。|
|0x00093005 （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 NDIS/WIFI 验证规则[WlanConnectionRoaming](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlanconnectionroaming)。|
|0x00093006 （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 NDIS/WIFI 验证规则[WlanDisassociation](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlandisassociation)。|
|0x00094007 （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 NDIS/WIFI 验证规则[WlanTimedAssociation](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedassociation)。|
|0x00094008 （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 NDIS/WIFI 验证规则[WlanTimedConnectionRoaming](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedconnectionroaming)。|
|0x00094009 （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 NDIS/WIFI 验证规则[WlanTimedConnectRequest](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedconnectrequest)。|
|0x0009400B （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 NDIS/WIFI 验证规则[WlanTimedLinkQuality](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedlinkquality)。|
|0x0009400C （Windows 8.1 操作系统及更高版本）|指向描述违反规则条件的字符串的指针。|内部规则状态的地址（第二个参数为！ ruleinfo）。|补充状态的地址（第三个参数为！ ruleinfo）。|驱动程序违反了 NDIS/WIFI 验证规则[WlanTimedScan](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedscan)。|




<a name="cause"></a>原因
-----

有关原因的说明，请参阅参数部分中每个代码的说明。 可以通过使用[ **！分析-v**](-analyze.md)扩展来获取进一步的信息。

<a name="resolution"></a>分辨率
----------

此 bug 检查只能在已指示驱动程序验证器监视一个或多个驱动程序时出现。 如果你不打算使用驱动程序验证程序，则应停用它。 你还可以考虑删除导致此问题的驱动程序。

如果您是驱动程序编写者，请使用通过此 bug 检查获取的信息来修复代码中的 bug。

有关驱动程序验证程序的完整详细信息，请参阅 Windows 驱动程序工具包（WDK）中的[驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)部分。

<a name="remarks"></a>备注
-------

\_池\_类型代码在 Ntddk 中进行枚举。 具体而言， **0** （零）表示非分页池， **1** （一）表示页面缓冲池。

*（Windows 8 及更高版本的 windows）* 如果[DDI 相容性检查](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)导致错误检查，请在驱动程序源代码上运行[静态驱动程序验证](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)程序，并指定导致 bug 检查的 DDI 相容性规则（由参数1值标识）。 静态驱动程序验证程序可帮助您在源代码中找到问题的原因。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[启用驱动程序验证程序时处理 Bug 检查](handling-a-bug-check-when-driver-verifier-is-enabled.md)

 

 




