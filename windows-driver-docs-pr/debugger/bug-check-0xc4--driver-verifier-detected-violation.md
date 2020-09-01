---
title: Bug 检查 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION
description: DRIVER_VERIFIER_DETECTED_VIOLATION bug 检查的值为0x000000C4。 这是驱动程序验证程序发现的致命错误的一般 bug 检查代码。
ms.assetid: 7814f827-05fc-419b-b428-4565978bbb52
keywords:
- Bug 检查 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION
- DRIVER_VERIFIER_DETECTED_VIOLATION
ms.date: 04/10/2020
topic_type:
- apiref
api_name:
- DRIVER_VERIFIER_DETECTED_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4c3edcb21824d75cd63df291ada696eb547c3950
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211248"
---
# <a name="bug-check-0xc4-driver_verifier_detected_violation"></a>Bug 检查0xC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突

驱动程序 \_ 验证程序 \_ 检测到 \_ 违反 bug 检查的值为0x000000C4。 这是驱动程序验证程序发现的致命错误的一般 bug 检查代码。 有关详细信息，请参阅 [在启用驱动程序验证程序时处理 Bug 检查](handling-a-bug-check-when-driver-verifier-is-enabled.md)。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。

## <a name="driver_verifier_detected_violation-parameters"></a>驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突参数

参数1标识冲突类型。 其余参数的含义因参数1的值而异。 下表对参数值进行了说明。

**注意**   如果在此表中查看所有5列时遇到问题，请尝试以下操作：
- 将浏览器窗口展开为完整大小。
- 将光标放在表中，并使用箭头键向左和向右滚动。

### <a name="0x00-to-0x70"></a>0x00 到0x70

|参数 1|参数2|参数3|参数4|错误的原因|
|--- |--- |--- |--- |--- |
|0x00|当前 IRQL|池类型|字节数|驱动程序请求了零字节的池分配。|
|0x01|当前 IRQL|池类型|分配大小（以字节为单位）|驱动程序尝试 APC_LEVEL > 分配分页内存。|
|0x02|当前 IRQL|池类型|分配大小（以字节为单位）|驱动程序尝试以 IRQL > DISPATCH_LEVEL 分配未分页的内存。|
|0x03| | | |调用方尝试分配的多个必须成功的池，但一页是此 API 允许的最大值。 |
|0x10|地址错误|0|0|驱动程序尝试释放未从分配调用返回的地址。|
|0x11|当前 IRQL|池类型|池地址|驱动程序尝试将 > APC_LEVEL 的 IRQL 释放页面缓冲池。|
|0x12|当前 IRQL|池类型|池地址|驱动程序尝试 DISPATCH_LEVEL > 具有 IRQL 的非分页池。|
|0x13 或0x14|预留|指向池标头的指针|池标头内容|驱动程序尝试释放已释放的内存池。|
|0x15|计时器条目|池类型|要释放的池地址|调用方尝试释放的池包含活动的计时器。|
|0x16|预留|池地址|0|驱动程序尝试在错误的地址释放池，或驱动程序将无效参数传递给了内存例程。|
|0X17|资源条目 | 池类型 |要释放的池地址 |调用方尝试释放的池包含活动的 ERESOURCE。 |
|0x30|当前 IRQL|请求的 IRQL|0|驱动程序向 [KeRaiseIrql](/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)传递了无效参数。  (参数是低于当前 IRQL 的值或大于 HIGH_LEVEL 的值。 这可能是使用未初始化的参数的结果。 ) |
|0x31|当前 IRQL|请求的 IRQL|0：新的 IRQL 错误1：新的 IRQL 在 DPC 例程内无效|驱动程序向 [KeLowerIrql](/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql~r1)传递了无效参数。  (参数是比当前 IRQL 更高的值或大于 HIGH_LEVEL 的值。 这可能是使用未初始化的参数的结果。 ) |
|0x32|当前 IRQL|旋转锁地址|0|驱动程序调用 [KeReleaseSpinLock 的](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock) 不是 DISPATCH_LEVEL。  (这可能是由于旋转锁的双释放导致的。 ) |
|0x33|当前 IRQL|快速 mutex 地址|0|驱动程序尝试 APC_LEVEL > 获取快速 mutex，并提供 IRQL。|
|0x34|当前 IRQL|线程 APC 禁用计数|快速 mutex 地址|驱动程序尝试以不同于 APC_LEVEL 的 IRQL 释放快速 mutex。|
|0x35|当前 IRQL|旋转锁地址|旧 IRQL|内核释放了一个不等于 DISPATCH_LEVEL 的自旋锁。|
|0x36|当前 IRQL|旋转锁定号|旧 IRQL|内核释放了一个不等于 DISPATCH_LEVEL 的排队自旋锁。|
|0x37|当前 IRQL|线程 APC 禁用计数|资源|驱动程序试图获取资源，但 Apc 未被禁用。|
|0x38|当前 IRQL|线程 APC 禁用计数|资源|驱动程序尝试释放资源，但 Apc 未被禁用。|
|0x39|当前 IRQL|线程 APC 禁用计数|Mutex|驱动程序尝试获取互斥体 "unsafe"，其中 IRQL 不等于 APC_LEVEL 输入。|
|0x3A|当前 IRQL|线程 APC 禁用计数|Mutex|驱动程序尝试发布一个互斥体 "unsafe"，其中 IRQL 不等于 APC_LEVEL 输入。|
|0x3B|当前 IRQL|要等待的对象|超时参数|正在 DISPATCH_LEVEL 或更高版本调用 KeWaitXxx 例程。|
|0x3C|传递给例程的句柄|对象类型|0|驱动程序调用 [ObReferenceObjectByHandle](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle) 时使用了错误的句柄。|
|0x3D|0|0|错误资源的地址|驱动程序将错误 (未对齐的) 资源传递给 [ExAcquireResourceExclusive](../kernel/mmcreatemdl.md)。|
|0x3E|0|0|0|对于当前不在关键区域中的线程，驱动程序调用 [KeLeaveCriticalRegion](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion) 。|
|0x3F|对象地址|新的对象引用计数。 -1：取消引用 case 1：引用大小写|0|驱动程序将 [ObReferenceObject](/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject) 应用到引用计数为零的对象， [或者将该驱动程序应用到](/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject) 引用计数为零的对象。|
|0x40|当前 IRQL|旋转锁地址|0|名为 [KeAcquireSpinLockAtDpcLevel](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel) 的驱动程序 DISPATCH_LEVEL <。|
|0x41|当前 IRQL|旋转锁地址|0|名为 [KeReleaseSpinLockFromDpcLevel](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel) 的驱动程序 DISPATCH_LEVEL <。|
|0x42|当前 IRQL|旋转锁地址|0|名为 [KeAcquireSpinLock](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) 的驱动程序 DISPATCH_LEVEL >。|
|0x51|分配的基址|超出分配的引用的地址|收费字节数|驱动程序在写入超过分配末尾后，尝试释放内存。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x52|分配的基址|哈希条目|收费字节数|驱动程序在写入超过分配末尾后，尝试释放内存。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x53|分配的基址|标头|预留|驱动程序在写入超过分配末尾后，尝试释放内存。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x54|分配的基址|预留|池哈希大小|驱动程序在写入超过分配末尾后，尝试释放内存。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x59|分配的基址|Listindex|预留|驱动程序在写入超过分配末尾后，尝试释放内存。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x60|从分页池分配的字节数|从非分页池分配的字节数|未释放的分配总数|卸载驱动程序时，不首先释放其池分配。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x61|从分页池分配的字节数|从非分页池分配的字节数|未释放的分配总数|驱动程序正在卸载时，驱动程序线程正在尝试分配池内存。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x62|驱动程序名称|预留|未释放的总分配数，包括分页池和非分页池|卸载驱动程序时，不首先释放其池分配。 仅当驱动程序验证程序的池跟踪选项处于活动状态时，才会发生带有此参数的 bug 检查。 键入！ verifier 3 drivername.sys 来了解导致错误检测的已泄漏分配的信息。|
|0x6F|MDL 地址|正在锁定的物理页|系统中的最高物理页面|在不在 PFN 数据库中的页上调用了 MmProbeAndLockPages。 这通常是一个调用此例程的驱动程序，用于锁定其自己的专用 dualport RAM。  这并不是必需的，它还会损坏具有非连续物理 RAM 的计算机上的内存。|

### <a name="0x70-to-0x91"></a>0x70 到0x91

|参数 1|参数2|参数3|参数4|错误的原因|
|--- |--- |--- |--- |--- |
|0x70|当前 IRQL|MDL 地址|访问模式|名为 [MmProbeAndLockPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages) 的驱动程序 DISPATCH_LEVEL >。|
|0x71|当前 IRQL|MDL 地址|进程地址|名为 MmProbeAndLockProcessPages 的驱动程序 DISPATCH_LEVEL >。|
|0x72|当前 IRQL|MDL 地址|进程地址|名为 MmProbeAndLockSelectedPages 的驱动程序 DISPATCH_LEVEL >。|
|0x73|当前 IRQL|在32位 Windows 中：64位 Windows 中物理地址的低32位：64位物理地址|字节数|名为 [MmMapIoSpace](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace) 的驱动程序 DISPATCH_LEVEL >。|
|0x74|当前 IRQL|MDL 地址|访问模式|在内核模式下，名为 [MmMapLockedPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages) 的驱动程序 DISPATCH_LEVEL >。|
|0x75|当前 IRQL|MDL 地址|访问模式|在用户模式下名为 [MmMapLockedPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages) 的驱动程序 APC_LEVEL >。|
|0x76|当前 IRQL|MDL 地址|访问模式|在内核模式下，名为 [MmMapLockedPagesSpecifyCache](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache) 的驱动程序 DISPATCH_LEVEL >。|
|0x77|当前 IRQL|MDL 地址|访问模式|在用户模式下名为 [MmMapLockedPagesSpecifyCache](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache) 的驱动程序 APC_LEVEL >。|
|0x78|当前 IRQL|MDL 地址|0|名为 [MmUnlockPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages) 的驱动程序 DISPATCH_LEVEL >。|
|0x79|当前 IRQL|正在取消映射的虚拟地址|MDL 地址|在内核模式下，名为 [MmUnmapLockedPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmaplockedpages) 的驱动程序 DISPATCH_LEVEL >。|
|0x7A|当前 IRQL|正在取消映射的虚拟地址|MDL 地址|在用户模式下名为 [MmUnmapLockedPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmaplockedpages) 的驱动程序 APC_LEVEL >。|
|0x7B|当前 IRQL|正在取消映射的虚拟地址|字节数|名为 [MmUnmapIoSpace](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace) 的驱动程序 APC_LEVEL >。|
|0x7C|MDL 地址|MDL 标志|0|驱动程序调用 [MmUnlockPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)，并通过其页从未成功锁定的 MDL。|
|0x7D|MDL 地址|MDL 标志|0|驱动程序调用 [MmUnlockPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)，并通过其页面来自非分页池的 MDL。  (不要解除锁定。 ) |
|0x7E|当前 IRQL|DISPATCH_LEVEL|0|名为 [MmAllocatePagesForMdl](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdl)、 [MmAllocatePagesForMdlEx](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdlex)或 [MmFreePagesFromMdl](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreepagesfrommdl) 的驱动程序 > DISPATCH_LEVEL。|
|0x7F|当前 IRQL|MDL 地址|MDL 标志|该驱动程序调用 [BuildMdlForNonPagedPool](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool) ，并传递其页面来自页面缓冲池的 MDL。|
|0x80|当前 IRQL|事件地址|0|名为 [KeSetEvent](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent) 的驱动程序 DISPATCH_LEVEL >。|
|0x81|MDL 地址|MDL 标志|0|称为 [MmMapLockedPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages)的驱动程序。  (应改用 [MmMapLockedPagesSpecifyCache](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache) ，并将 BugCheckOnFailure 参数设置为 FALSE。 ) |
|0x82|MDL 地址|MDL 标志|0|驱动程序调用 [MmMapLockedPagesSpecifyCache](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache) ，BugCheckOnFailure 参数等于 TRUE。  (此参数应设置为 FALSE。 ) |
|0x83|要映射的物理地址范围的开头|要映射的字节数|未锁定的第一个页面框架编号|驱动程序调用 [MmMapIoSpace](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace) ，但未锁定 MDL 页面。 在进行此调用之前，必须锁定由要映射的物理地址范围表示的物理页面。|
|0x85|MDL 地址|要映射的页数|未锁定的第一个页面框架编号|驱动程序调用 [MmMapLockedPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages) ，但未锁定 MDL 页面。|
|0x89|MDL 地址|指向 MDL 中的非内存页的指针|MDL 中的非内存页码|MDL 未标记为 "i/o"，但它包含非内存页面地址。|
|0x91|预留|预留|预留|驱动程序使用操作系统不支持的方法交换堆栈。 扩展内核模式堆栈的唯一受支持的方法是使用 [KeExpandKernelStackAndCallout](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keexpandkernelstackandcallout)。|

### <a name="0xa0-to-0x140"></a>0xA0 到0x140

|参数 1|参数2|参数3|参数4|错误的原因|
|--- |--- |--- |--- |--- |
|0xA0|一个指针，指向用于进行读取或写入请求的 IRP|较低设备的设备对象|检测到错误的扇区数|在硬盘上检测到 (CRC) 错误的循环冗余检查。 仅当驱动程序验证程序的磁盘完整性检查选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0xA1|进行读取或写入请求的 IRP 副本。  (实际 IRP 已完成。 ) |较低设备的设备对象|检测到错误的扇区数|在 (异步) 的扇区上检测到 CRC 错误。 仅当驱动程序验证程序的磁盘完整性检查选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0xA2|创建读取或写入请求的 IRP，或此 IRP 的副本|较低设备的设备对象|检测到错误的扇区数|CRCDISK 校验和副本不匹配。 这可能是分页错误。 仅当驱动程序验证程序的磁盘完整性检查选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0xB0 |MDL 地址|MDL 标志|MDL 标志不正确|对于具有错误标志的 MDL，驱动程序调用 [MmProbeAndLockPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages) 。 例如，驱动程序将 [MmBuildMdlForNonPagedPool](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool) 创建的 MDL 传递到 MmProbeAndLockPages。|
|0xB1 |MDL 地址|MDL 标志|MDL 标志不正确|对于具有错误标志的 MDL，驱动程序调用 MmProbeAndLockProcessPages。 例如，驱动程序将 [MmBuildMdlForNonPagedPool](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool) 创建的 MDL 传递到 MmProbeAndLockProcessPages。|
|0xB2 |MDL 地址|MDL 标志|MDL 标志不正确|对于具有错误标志的 MDL，驱动程序调用 [MmMapLockedPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages) 。 例如，驱动程序通过了已映射到系统地址或未锁定到 MmMapLockedPages 的 MDL。|
|0xB3 |MDL 地址|MDL 标志|缺少 MDL 标志 (应该至少有一个) |对于具有错误标志的 MDL，驱动程序调用 [MmMapLockedPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages) 。 例如，驱动程序将一个未锁定的 MDL 传递到 MmMapLockedPages。|
|0xB4 |MDL 地址|MDL 标志|意外的部分 MDL 标志|部分 MDL 的驱动程序调用 [MmUnlockPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages) 。 部分 MDL 是由 [IoBuildPartialMdl](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl)创建的 MDL。|
|0xB5|MDL 地址|MDL 标志|意外的部分 MDL 标志|使用 [IoBuildPartialMdl](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl)) 创建的部分 MDL (上调用了 MmUnmapLockedPages。|
|0xB6|MDL 地址|MDL 标志|缺少 MDL 标志|对未映射到系统地址的 MDL 调用了 MmUnmapLockedPages。|
|0xB7|损坏的物理页数。|第一个损坏的物理页。|上次损坏的物理页。|在睡眠转换期间，系统 BIOS 的物理内存已损坏。|
|0xB8 |MDL 地址|MDL 标志|预留|MDL 描述的页面仍已映射。 在调用 IoFreeMdl 之前，驱动程序必须取消页面映射。|
|0xB9 |正在取消映射的地址。|MDL 地址。|预留|使用错误的用户空间地址调用了 MmUnmapLockedPages。|
|0xC0 |IRP 的地址|0|预留|已禁用中断的驱动程序调用 [IoCallDriver](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 。|
|0xC1 |驱动程序调度例程的地址|预留|预留|返回了驱动程序调度例程，并禁用了中断。|
|0xC2 |0|0|0|禁用中断后，该驱动程序称为快速 i/o 调度例程。|
|0xC3 |驱动程序快速 i/o 调度例程的地址|预留|预留|返回驱动程序快速 i/o 调度例程，并禁用中断。|
|0xC5 |驱动程序调度例程的地址|当前线程的 APC 禁用计数|调用驱动程序调度例程之前线程的 APC 禁用计数|驱动程序调度例程已更改线程的 APC 禁用计数。 每次驱动程序调用 [KeEnterCriticalRegion](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)、 [FsRtlEnterFileSystem](../ifs/fsrtlenterfilesystem.md)或获取互斥体时，APC 禁用计数都将减少。 每次驱动程序调用 [KeLeaveCriticalRegion](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)、 [KeReleaseMutex](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex)或 [FsRtlExitFileSystem](../ifs/fsrtlexitfilesystem.md)时，APC 禁用计数都将递增。 由于这些调用应始终成对出现，因此每当退出线程时，APC 禁用计数都应为零。 负值表示驱动程序已禁用 APC 调用，而无需重新启用它们。 正值指示反转为 true。|
|0xC6 |驱动程序快速 i/o 调度例程的地址|当前线程的 APC 禁用计数|调用 Fast i/o 驱动程序调度例程之前线程的 APC 禁用计数|驱动程序快速 i/o 调度例程已更改线程的 APC 禁用计数。 每次驱动程序调用 [KeEnterCriticalRegion](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)、 [FsRtlEnterFileSystem](../ifs/fsrtlenterfilesystem.md)或获取互斥体时，APC 禁用计数都将减少。 每次驱动程序调用 [KeLeaveCriticalRegion](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)、 [KeReleaseMutex](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex)或 [FsRtlExitFileSystem](../ifs/fsrtlexitfilesystem.md)时，APC 禁用计数都将递增。 由于这些调用应始终成对出现，因此每当退出线程时，APC 禁用计数都应为零。 负值表示驱动程序已禁用 APC 调用，而无需重新启用它们。 正值指示反转为 true。|
|0xCA |后备链表列表的地址|预留|预留|驱动程序已尝试重新初始化后备链表列表。|
|0xCB |后备链表列表的地址|预留|预留|驱动程序已尝试删除未初始化的后备链表列表。|
|0xCC |后备链表列表的地址|池分配的起始地址|池分配的大小|驱动程序已尝试释放包含活动后备链表列表的池分配。|
|0xCD |后备链表列表的地址|调用方指定的块大小|支持的最小块大小|驱动程序尝试创建的后备链表列表的分配块大小太小。|
|0xD0 |ERESOURCE 结构的地址|预留|预留|驱动程序已尝试重新初始化 ERESOURCE 结构。|
|0xD1 |ERESOURCE 结构的地址|预留|预留|驱动程序已尝试删除未初始化的 ERESOURCE 结构。|
|0xD2 |ERESOURCE 结构的地址|池分配的起始地址|池分配的大小|驱动程序已尝试释放包含活动 ERESOURCE 结构的池分配。|
|0xD5 |由该驱动程序的已检查内部版本创建的 IO_REMOVE_LOCK 结构的地址|当前 [IoReleaseRemoveLock](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock) 标记|预留|当前 [IoReleaseRemoveLock](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock) 标记与上一个 [IoAcquireRemoveLock](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) 标记不匹配。 如果调用 IoReleaseRemoveLock 的驱动程序不在已检查的内部版本中，则参数2为驱动程序验证程序代表驱动程序创建的卷影 IO_REMOVE_LOCK 结构的地址。 在这种情况下，驱动程序使用的 IO_REMOVE_LOCK 结构的地址根本不使用，因为驱动程序验证器将替换所有删除锁定 Api 的锁定地址。 仅当驱动程序验证程序的 i/o 验证选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0xD6 |由该驱动程序的已检查内部版本创建的 IO_REMOVE_LOCK 结构的地址|与上一个 [IoAcquireRemoveLock](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) 标记不匹配的标记|上一个 [IoAcquireRemoveLock](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) 标记|当前 [IoReleaseRemoveLockAndWait](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait) 标记与上一个 [IoAcquireRemoveLock](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) 标记不匹配。 如果调用 [IoReleaseRemoveLock](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock) 的驱动程序不是已检查的生成，则参数2是由驱动程序验证程序代表驱动程序创建的卷影 IO_REMOVE_LOCK 结构的地址。 在这种情况下，驱动程序使用的 IO_REMOVE_LOCK 结构的地址根本不使用，因为驱动程序验证器将替换所有删除锁定 Api 的锁定地址。 仅当驱动程序验证程序的 i/o 验证选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0xD7|驱动程序验证程序内部使用的已检查生成删除锁定结构的地址|驱动程序指定的移除锁结构的地址|预留|即使删除锁调用了 [IoReleaseRemoveLockAndWait](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)，也不能对其进行重新初始化，因为其他线程可能仍会通过调用 [IoAcquireRemoveLock](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)) 使用该锁 (。 驱动程序应在其设备扩展内分配删除锁定，并对其进行一次初始化。 锁定将与设备扩展一起删除。|
|0xDA |驱动程序的起始地址|驱动程序中的 WMI 回调地址|预留|尝试卸载未取消注册其 WMI 回调函数的驱动程序。|
|0xDB |设备对象的地址|预留|预留|尝试删除未从 WMI 取消注册的设备对象。|
|0xDC |预留|预留|预留|指定了无效的 RegHandle 值作为函数 [EtwUnregister](/windows-hardware/drivers/ddi/wdm/nf-wdm-etwunregister)的参数。|
|0xDD |调用 EtwRegister 的地址|卸载驱动程序的起始地址|对于 Windows 8 及更高版本，此参数是 ETW RegHandle 值。|尝试在不调用 [EtwUnregister](/windows-hardware/drivers/ddi/wdm/nf-wdm-etwunregister)的情况下卸载驱动程序。|
|0xDF |同步对象地址|0|0|同步对象处于会话地址空间中。 不允许在会话地址空间中使用同步对象，因为它们可以从其他会话或没有会话虚拟地址空间的系统线程进行操作。|
|0xE0 |用作参数的用户模式地址|用作参数的地址范围的大小（以字节为单位）|预留|调用了将用户模式地址指定为参数的操作系统内核函数。|
|0xE1 |同步对象的地址|预留|预留|发现同步对象具有无效或可分页的地址。|
|0xE2 |IRP 的地址|IRP 中存在的用户模式地址|预留|发现使用 Irp >Irp->requestormode 设置为 KernelMode 的 IRP 将用户模式地址作为其成员之一。|
|0xE3 |对 API 的调用的地址|用作 API 中的参数的用户模式地址|预留|驱动程序已调用使用用户模式地址作为参数的内核模式 ZwXxx 例程。|
|0xE4 |对 API 的调用的地址|格式不正确的 UNICODE_STRING 结构的地址|预留|驱动程序调用了具有格式不正确的 UNICODE_STRING 结构作为参数的内核模式 ZwXxx 例程。|
|0xE5 |当前 IRQL|预留|预留|对内核 API 进行的调用出现错误的 IRQL。|
|0xE6 |发出 Zw API 调用的驱动程序中的地址|当前 IRQL|特殊内核 Apc。|未在 IRQL = PASSIVE_LEVEL 和启用了特殊内核 Apc 的情况调用内核 Zw API。|
|0xEA |当前 IRQL|线程的 APC 禁用计数|Pushlock 的地址|当启用 Apc 时，驱动程序已尝试获取 pushlock。|
|0xEB |当前 IRQL|线程的 APC 禁用计数|Pushlock 的地址|当启用 Apc 时，驱动程序已尝试发布 pushlock。|
|0xF0 |目标缓冲区的地址|源缓冲区的地址|要复制的字节数|一个名为 memcpy 函数的驱动程序，其中包含重叠的源和目标缓冲区。|
|0xF5 |NULL 句柄的地址|对象类型|预留|驱动程序将空句柄传递到 [ObReferenceObjectByHandle](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)。|
|0xF6 |正在引用的句柄值|当前进程的地址|执行错误引用的驱动程序中的地址|驱动程序将用户模式句柄作为内核模式引用。|
|0xF7 |调用方指定的句柄值|调用方指定的对象类型|调用方指定的 AccessMode|驱动程序在系统进程的上下文中尝试使用内核句柄的用户模式引用。|
|0xFA |完成例程地址。|IRQL 值，然后再调用完成例程|当前 IRQL 值，在调用完成例程后|IRP 完成例程返回的 IRQL 不同于调用例程的 irql。|
|0xFB |完成例程地址|当前线程的 APC 禁用计数|线程的 APC 禁用计数，然后再调用 IRP 完成例程|此线程的 APC 禁用计数已由驱动程序的 IRP 完成例程更改。 每次驱动程序调用 [KeEnterCriticalRegion](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)、 [FsRtlEnterFileSystem](../ifs/fsrtlenterfilesystem.md)或获取互斥体时，APC 禁用计数都将减少。 每次驱动程序调用 [KeLeaveCriticalRegion](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)、 [KeReleaseMutex](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex)或 [FsRtlExitFileSystem](../ifs/fsrtlexitfilesystem.md)时，APC 禁用计数都将递增。 由于这些调用应始终成对出现，因此每当退出线程时，APC 禁用计数都应为零。 负值表示驱动程序已禁用 APC 调用，而无需重新启用它们。 正值指示反转为 true。|
|0xFC |驱动程序中的地址，用于进行错误的 API 调用。|提供的 ApcContext 值。|预留|从具有不受支持的 ApcContext 值的内核模式) 调用 ZwNotifyChangeKey (。|

### <a name="0x105-to-0x140"></a>0x105 到0x140

|参数 1|参数2|参数3|参数4|错误的原因|
|--- |--- |--- |--- |--- |
|0x105 |IRP 的地址|0|0|驱动程序使用 ExFreePool 而不是 IoFreeIrp 来释放 IRP。|
|0x10A |0|0|0|驱动程序尝试将池配额计费到空闲进程。|
|0x10B |0|0|0|驱动程序尝试从 DPC 例程对池配额计费。 这是不正确的，因为当前进程上下文未定义。|
|0x110 |0|0|0|中断服务例程的地址|在执行 ISR 之前保存的扩展上下文的地址|扩展上下文的地址在执行 ISR 后保存|驱动程序 (ISR) 的中断服务例程已损坏扩展线程上下文。|
|0x111 |中断服务例程的地址|执行 ISR 之前的 IRQL|执行 ISR 后的 IRQL|中断服务例程返回了已更改的 IRQL。|
|0x115 |负责关闭的线程的地址，可能是死锁的。|0|0|驱动程序验证程序检测到系统已超过20分钟并且关闭未完成。|
|0x11A |当前 IRQL|0|0|驱动程序在 APC_LEVEL 的 IRQL > 调用 KeEnterCriticalRegion。|
|0x11B |当前 IRQL|0|0|驱动程序在 APC_LEVEL 的 IRQL > 调用 KeLeaveCriticalRegion。|
|0x120 |IRQL 值的地址|要等待的对象的地址|超时值的地址|线程 DISPATCH_LEVEL > 以 IRQL 为间隔。 KeWaitForSingleObject 或 KeWaitForMultipleObjects 的调用方必须以 IRQL <= DISPATCH_LEVEL 运行。|
|0x121 |IRQL 值的地址|要等待的对象的地址|超时值的地址|线程等待 IRQL 等于 DISPATCH_LEVEL，超时值为 NULL。 KeWaitForSingleObject 或 KeWaitForMultipleObjects 的调用方可以 <= DISPATCH_LEVEL 运行。 如果为超时提供了空指针，则调用线程将保持等待状态，直到终止对象。|
|0x122 |IRQL 值的地址|要等待的对象的地址|超时值的地址|线程在 DISPATCH_LEVEL 等待，超时值不等于零 (0) 。 如果 Timeout！ = 0，则 KeWaitForSingleObject 或 KeWaitForMultipleObjects 的调用方必须以 IRQL <= APC_LEVEL 运行。|
|0x123 |要等待的对象的地址|0|0|KeWaitForSingleObject 或 KeWaitForMultipleObjects 的调用方将 wait 指定为 UserMode，但该对象在内核堆栈上。|
|0x130 |工作项的地址|0|0|工作项在会话地址空间中。 会话地址空间中不允许使用工作项，因为它们可以从其他会话或没有会话虚拟地址空间的系统线程进行操作。|
|0x131 |工作项的地址|0|0|工作项位于可分页内存中。 工作项必须位于不可分页的内存中，因为内核在 DISPATCH_LEVEL 使用它们。|
|0x135|IRP 的地址|[IoCancelIrp](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)调用与此 IRP 的完成之间允许的毫秒数|0|在预期时间内，已取消的 IRP 未完成，驱动程序所用时间比预期时间长，无法完成取消的 IRP。|
|0x13A|正在释放的池块的地址|值不正确|不正确的值的地址|驱动程序调用了 [ExFreePool](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) ，驱动程序验证器在用于跟踪池使用情况的某个内部值中检测到错误。|
|0x13B|正在释放的池块的地址|不正确的值的地址|指向错误内存页的指针的地址|驱动程序调用了 [ExFreePool](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) ，驱动程序验证器在用于跟踪池使用情况的某个内部值中检测到错误。|
|0x13C|正在释放的池块的地址|值不正确|不正确的值的地址|驱动程序调用了 [ExFreePool](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) ，驱动程序验证器在用于跟踪池使用情况的某个内部值中检测到错误。|
|0x13D|正在释放的池块的地址|不正确的值的地址|应为正确的值|驱动程序调用了 [ExFreePool](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) ，驱动程序验证器在用于跟踪池使用情况的某个内部值中检测到错误。|
|0x13E|调用方指定的池块地址|驱动程序验证程序跟踪的池块地址|指向由驱动程序验证程序跟踪的池块地址的指针|[ExFreePool](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)的调用方指定的池块地址不同于 Driver Verifier 所跟踪的地址。|
|0x13F|正在释放的池块的地址|要释放的字节数|指向驱动程序验证器跟踪的字节数的指针|在对 [ExFreePool](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) 的调用中释放的内存字节数不同于 Driver Verifier 所跟踪的字节数。|
|0x140|当前 IRQL|MDL 地址|与此 MDL 关联的虚拟地址|非锁定 MDL 是从可分页或 tradable 内存构造的。|
|0x141|请求分配的驱动程序的最高物理地址|要分配的字节数|0|驱动程序在4GB 下显式请求物理内存。|

### <a name="0x1000-to-0x100b---deadlocks"></a>0x1000 到 0x100B-死锁

|参数 1|参数2|参数3|参数4|错误的原因|
|--- |--- |--- |--- |--- |
|0x1000 |资源地址|预留|预留|自死锁：当前线程已尝试以递归方式获取只拥有共享的资源。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x1001 |导致死锁的最后原因的资源的地址|预留|预留|死锁：发现锁层次结构冲突。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，才会发生带有此参数的 bug 检查。  (使用 [！死锁](-deadlock.md) 扩展获取详细信息。 ) |
|0x1002 |资源地址|预留|预留|未初始化的资源：在未首先初始化的情况下，已获取资源。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x1003 |被死锁的资源的地址|应该首先释放的资源的地址|预留|意外发布：按错误的顺序释放了资源。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x1004 |资源地址|获取资源的线程的地址|当前线程的地址|意外线程：错误的线程释放资源。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x1005 |资源地址|预留|预留|多次初始化：资源多次初始化。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x1007 |资源地址|预留|预留|Unacquired 资源：在获取资源之前释放资源。 仅当驱动程序验证程序的死锁检测选项处于活动状态时，才会发生带有此参数的 bug 检查。|
|0x1008 相关联 |锁定地址|预留|预留|驱动程序尝试使用对此锁定类型不匹配的 API 来获取锁定。|
|0x1009 |锁定地址|预留|预留|驱动程序尝试使用对此锁定类型不匹配的 API 来释放锁定。|
|0x100A |所有者线程地址|预留|终止的线程拥有该锁。|
|0x100B |锁定地址|所有者线程地址|预留|已删除的锁仍归线程所有。|
|0x1010 |写入 IRP 所颁发到的设备对象。|IRP 的地址。|MDL 描述的缓冲区的系统空间虚拟地址。|写入 Irp 的固定 MDL 缓冲区内容已修改。|
|0x1011 |写入 IRP 所颁发到的设备对象。|IRP 的地址。|MDL 描述的缓冲区的系统空间虚拟地址。|读取 Irp 的固定 MDL 缓冲区内容在调度或虚拟页面支持的缓冲区中被修改。|
|0x1012 |指向描述冲突的字符串的指针。|如果未使用) ，则此损坏所涉及的数据 (0。|如果未使用) ，则此损坏所涉及的数据 (0。|验证程序扩展状态存储检测到损坏。|
|0x1013 |指向驱动程序对象的指针。|指向捕获的原始 i/o 回调的指针。|保留 (未使用) 。|验证程序在捕获的原始 i/o 回调中检测到内部损坏。|

### <a name="0x2000-to-0x2005---code-integrity-issues"></a>0x2000 到 0x2005-代码完整性问题

|参数 1|参数2|参数3|参数4|错误的原因|
|--- |--- |--- |--- |--- |
|0x2000 |驱动程序代码中检测到错误的地址。 |池类型。 | 如果提供) ，则为池标记 (。|代码完整性问题：调用方指定了可执行的池类型。 需要 (： NonPagedPoolNx)  |
|0x2001 |驱动程序代码中检测到错误的地址。 |页面保护 (WIN32_PROTECTION_MASK) 。 | 0 |代码完整性问题：调用方指定了可执行页保护。 应 (：已清除 PAGE_EXECUTE * 位)  |
|0x2002 |驱动程序代码中检测到错误的地址。 |MM_PAGE_PRIORITY 逻辑或 MdlMapping * ) 的页面优先级 (。 |0|代码完整性问题：调用方指定了可执行的 MDL 映射。 需要 (： MdlMappingNoExecute)  |
|0x2003 |映像文件 (Unicode string) 的名称。 | 节标头的地址。|节名称 (UTF-8 编码字符串) 。 |代码完整性问题：映像包含可执行文件和可写部分。 |
|0x2004 |映像文件 (Unicode string) 的名称。 |节标头的地址。 |节名称 (UTF-8 编码字符串) 。 |代码完整性问题：图像包含不是页对齐的部分。 |
|0x2005 |映像文件 (Unicode string) 的名称。 | IAT 目录。|节名称 (UTF-8 编码字符串) 。 |代码完整性问题：映像包含位于可执行部分中的 IAT。 |

### <a name="0xa001-to-0xa00d---vm-switch-issues"></a>0xA001 到 0xA00D-VM 交换机问题

|参数 1|参数2|参数3|参数4|错误的原因|
|--- |--- |--- |--- |--- |
|0xA001 |指向 NetBufferList 对象的指针|如果非 NULL，则为指向虚拟交换机对象 (的指针) |保留 (未使用) |VM 交换机：必须设置调用方提供的 NetBufferList 的 SourceHandle。 请参阅 [AllocateNetBufferListForwardingContext](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context) 例程。|
|0xA002 |指向 NetBufferList 对象的指针|如果非 NULL) ，则为指向虚拟交换机对象 (的指针。|保留 (未使用) |VM 交换机：调用方提供的 NetBufferList 转发详细信息不为零。 请参阅 [AllocateNetBufferListForwardingContext](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context) 例程。|
|0xA003 |指向 NetBufferList 对象的指针|如果非 NULL) ，则为指向虚拟交换机对象 (的指针。|保留 (未使用) |VM 交换机：调用方提供的 NetBufferList 的数据包标头或路由上下文为空。 请参阅 [可扩展交换机数据路径的数据包管理准则](../network/packet-management-guidelines-for-the-extensible-switch-data-path.md)。|
|0xA004 |无效端口的 ID|NIC 索引|如果非 NULL) ，则为指向虚拟交换机对象 (的指针。|VM 交换机：调用方指定了无效的端口和 NIC 索引组合。 请参阅 [Hyper-v 可扩展交换机端口和网络适配器状态](../network/hyper-v-extensible-switch-port-and-network-adapter-states.md)。|
|0xA005 |指向 NetBufferList 对象的指针|指向目标列表的指针。|如果非 NULL) ，则为指向虚拟交换机对象 (的指针。|VM 交换机：调用方提供的目标无效。 请参阅 [AddNetBufferListDestination](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination) 和 [UpdateNetBufferListDestinations](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)。|
|0xA006 |指向 NetBufferList 对象的指针|如果非 NULL) ，则为指向虚拟交换机对象 (的指针。|保留 (未使用) |VM 交换机：调用方提供了无效的源 NIC 或端口对象。 请参阅 [Hyper-v 可扩展交换机端口和网络适配器状态](../network/hyper-v-extensible-switch-port-and-network-adapter-states.md)。|
|0xA007 |指向 NetBufferList 对象的指针|如果非 NULL) ，则为指向虚拟交换机对象 (的指针。|保留 (未使用) |VM 交换机：调用方提供了无效的目标列表。 请参阅 [AddNetBufferListDestination](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination) 和 [UpdateNetBufferListDestinations](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)。|
|0xA008 |父 NIC 对象|NIC 索引|如果非 NULL) ，则为指向虚拟交换机对象 (的指针。|VM 交换机：尝试引用不允许的 NIC。 请参阅 [Hyper-v 可扩展交换机端口和网络适配器状态](../network/hyper-v-extensible-switch-port-and-network-adapter-states.md)。|
|0xA009 |正在引用的端口|如果非 NULL，则为指向虚拟交换机对象 (的指针) |保留 (未使用) |VM 交换机：不允许时，尝试引用端口。 请参阅 [Hyper-v 可扩展交换机端口和网络适配器状态](../network/hyper-v-extensible-switch-port-and-network-adapter-states.md)。|
|0xA00A |指向 NetBufferList 对象的指针|ContextTypeInfo 对象|保留 (未使用) |VM 交换机：故障上下文已设置。 请参阅 [SetNetBufferListSwitchContext](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_set_net_buffer_list_switch_context)。|
|0xA00B |指向 NetBufferList 对象的指针|NDIS_SWITCH_REPORT_FILTERED_NBL_FLAGS_ *|如果非 NULL，则为指向虚拟交换机对象 (的指针) |VM 交换机：为删除的 NetBufferList 提供的方向无效。 请参阅 [ReportFilteredNetBufferLists](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)。|
|0xA00C |指向 NetBufferList 对象的指针|发送标志值|如果非 NULL，则为指向虚拟交换机对象 (的指针) |VM 交换机：设置 NDIS_SEND_FLAGS_SWITCH_SINGLE_SOURCE 标志时，NetBufferList 链具有多个源端口。 请参阅 [Hyper-v 可扩展交换机发送和接收标志](../network/hyper-v-extensible-switch-send-and-receive-flags.md)。|
|0xA00D |指向 NetBufferList 对象的指针|指向虚拟交换机上下文的指针|如果非 NULL，则为指向虚拟交换机对象 (的指针) |VM 交换机：设置 NDIS_RECEIVE_FLAGS_SWITCH_DESTINATION_GROUP 标志时，链中的一个或多个 NetBufferLists 的目标无效。 请参阅 [Hyper-v 可扩展交换机发送和接收标志](../network/hyper-v-extensible-switch-send-and-receive-flags.md)。|
|0xA00E|指向 NetBufferLists 对象的指针。 |指向虚拟交换机上下文的指针。 |如果非 NULL) ，则为指向虚拟交换机对象 (的指针。 |VM 交换机：设置 VMS_NBL_ROUTING_CONTEXT_FLAG_NO_WNV_PROCESSING 标志时，尝试通过 WNV 完成 NetBufferList。|

### <a name="0x00020002-to-0x00020022---ddi-compliance-rule-violations"></a>0x00020002 到 0x00020022-DDI 符合性规则冲突

|参数 1|参数2|参数3|参数4|错误的原因|
|--- |--- |--- |--- |--- |
|0x00020002 |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlApcLte](../devtest/wdm-irqlapclte.md)。 规则指定只有当 IRQL <= APC_LEVEL 时，驱动程序才能调用 [ObGetObjectSecurity](/windows-hardware/drivers/ddi/wdm/nf-wdm-obgetobjectsecurity) 和 [ObReleaseObjectSecurity](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreleaseobjectsecurity) 。|
|0x00020003 |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlDispatch](../devtest/wdm-irqldispatch.md)。 IrqlDispatch 规则指定只有当 IRQL = 时，驱动程序才能调用特定例程 DISPATCH_LEVEL|
|0x00020004 |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlExAllocatePool](../devtest/wdm-irqlexallocatepool.md)。 IrqlExAllocatePool 规则指定，仅当<= DISPATCH_LEVEL 时，驱动程序才调用 [ExAllocatePoolWithTag](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) 和 [ExAllocatePoolWithTagPriority](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority) 。|
|0x00020005 |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlExApcLte1](../devtest/wdm-irqlexapclte1.md)。 IrqlExApcLte1 规则指定驱动程序仅调用 ExAcquireFastMutex 和 ExTryToAcquireFastMutex，<= APC_LEVEL。|
|0x00020006 |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlExApcLte2](/windows-hardware/drivers/ddi/index)。 IrqlExApcLte2 规则指定只有当 IRQL <= APC_LEVEL 时，驱动程序才调用特定例程。|
|0x00020007 |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlExApcLte3](../devtest/wdm-irqlexapclte3.md)。 IrqlExApcLte3 规则指定只有当 IRQL <= APC_LEVEL 时，驱动程序才能调用特定的执行程序支持例程。|
|0x00020008 |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlExPassive](../devtest/wdm-irqlexpassive.md)。 IrqlExPassive 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用特定的执行程序支持例程。|
|0x00020009 |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlIoApcLte](../devtest/wdm-irqlioapclte.md)。 IrqlIoApcLte 规则指定只有当 IRQL <= APC_LEVEL 时，驱动程序才能调用特定的 i/o 管理器例程。|
|0x0002000A |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlIoPassive1](../devtest/wdm-irqliopassive1.md)。 IrqlIoPassive1 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用特定的 i/o 管理器例程。|
|0x0002000B |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlIoPassive2](../devtest/wdm-irqliopassive2.md)。 IrqlIoPassive2 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用特定的 i/o 管理器例程。|
|0x0002000C |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlIoPassive3](../devtest/wdm-irqliopassive3.md)。 IrqlIoPassive3 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用特定的 i/o 管理器例程。|
|0x0002000D |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlIoPassive4](../devtest/wdm-irqliopassive4.md)。 IrqlIoPassive4 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用特定的 i/o 管理器例程。|
|0x0002000E |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlIoPassive5](../devtest/wdm-irqliopassive5.md)。 IrqlIoPassive5 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用特定的 i/o 管理器例程。|
|0x0002000F |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlKeApcLte1](../devtest/wdm-irqlkeapclte1.md)。 IrqlKeApcLte1 规则指定只有当 IRQL <= APC_LEVEL 时，驱动程序才能调用某些内核例程。|
|0x00020010 |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlKeApcLte2](../devtest/wdm-irqlkeapclte2.md)。 IrqlKeApcLte2 规则指定只有当 IRQL <= APC_LEVEL 时，驱动程序才能调用某些内核例程。|
|0x00020011 |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlKeDispatchLte](../devtest/wdm-irqlkedispatchlte.md)。 IrqlKeDispatchLte 规则指定只有当 IRQL <= DISPATCH_LEVEL 时，驱动程序才能调用某些内核例程。|
|0x00020015 |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlKeReleaseSpinLock](../devtest/wdm-irqlkereleasespinlock.md)。 IrqlKeReleaseSpinLock 规则指定只有当 IRQL = DISPATCH_LEVEL 时，驱动程序才能调用 KeReleaseSpinLock。|
|0x00020016 |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlKeSetEvent](../devtest/wdm-irqlkesetevent.md)。 IrqlKeSetEvent 规则指定在设置为 FALSE 时， [KeSetEvent](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent) 例程仅以 irql <= DISPATCH_LEVEL 调用，当 wait 设置为 TRUE 时，将在 irql <= APC_LEVEL。|
|0x00020019 |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlMmApcLte](../devtest/wdm-irqlmmapclte.md)。 IrqlMmApcLte 规则指定只有当 IRQL <= APC_LEVEL 时，驱动程序才能调用特定的内存管理器例程。|
|0x0002001A |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlMmDispatch](../devtest/wdm-irqlmmdispatch.md)。 IrqlMmDispatch 规则指定只有当 IRQL = DISPATCH_LEVEL 时，驱动程序才能调用 [MmFreeContiguousMemory](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreecontiguousmemory) 。|
|0x0002001B |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlObPassive](../devtest/wdm-irqlobpassive.md)。 IrqlObPassive 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用 [ObReferenceObjectByHandle](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle) 。|
|0x0002001C |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlPsPassive](../devtest/wdm-irqlpspassive.md)。 IrqlPsPassive 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用特定进程和线程管理器例程。|
|0x0002001D |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [IrqlReturn](../devtest/wdm-irqlreturn.md)。|
|0x0002001E |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlRtlPassive](../devtest/wdm-irqlrtlpassive.md)。 IrqlRtlPassive 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用 [RtlDeleteRegistryValue](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtldeleteregistryvalue) 。|
|0x0002001F |指向描述违反规则条件的字符串的指针。|指向规则状态变量的可选指针)  (s。|预留|驱动程序违反了 DDI 相容性规则 [IrqlZwPassive](../devtest/wdm-irqlzwpassive.md)。 IrqlZwPassive 规则指定只有当 IRQL = PASSIVE_LEVEL 时，驱动程序才能调用 [ZwClose](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose) 。|
|0x00020022 |指向描述违反规则条件的字符串的指针。|保留 (未使用) |保留 (未使用) |驱动程序违反了 DDI 相容性规则 [IrqlIoDispatch](../devtest/wdm-irqliodispatch.md)。|
|0x00020023 |指向描述违反规则条件的字符串的指针。 |保留 (未使用) 。 |保留 (未使用) 。 |驱动程序违反了 DDI 相容性规则  [IrqlIoRtlZwPassive](../devtest/wdm-irqliortlzwpassive.md)。 IrqlIoRtlZwPassive 规则指定，仅当该驱动程序以 IRQL = PASSIVE_LEVEL 执行时，才调用该规则中列出的 DDIs。|
|0x00020024 |指向描述违反规则条件的字符串的指针。 |保留 (未使用) 。 |保留 (未使用) 。 |驱动程序违反了 DDI 相容性规则 [IrqlNtifsApcPassive](../devtest/wdm-irqlntifsapcpassive.md)。 IrqlNtifsApcPassive 规则指定，仅当该驱动程序以 IRQL = PASSIVE_LEVEL 或 IRQL <= APC_LEVEL 执行时，才调用该规则中列出的 DDIs。|
|0x00020025 |指向描述违反规则条件的字符串的指针。 |保留 (未使用) 。 |保留 (未使用) 。 |驱动程序违反了 DDI 相容性规则 [IrqlKeMore](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkemore)。 IrqlKeMore 规则指定驱动程序以这些 DDIs 所需的 IRQL 调用规则中列出的 DDIs。|

### <a name="0x00040003-to-0x00043006---ddi-compliance-rule-violations"></a>0x00040003 到 0x00043006-DDI 符合性规则冲突

|参数 1|参数2|参数3|参数4|错误的原因|
|--- |--- |--- |--- |--- |
|0x00040003 |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [CriticalRegions](../devtest/wdm-criticalregions.md)。|
|0x00040006 |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [QueuedSpinLock](../devtest/wdm-queuedspinlock.md)。|
|0x00040007 |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [QueuedSpinLockRelease](../devtest/wdm-queuedspinlockrelease.md)。|
|0x00040009 |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [旋转锁](../devtest/wdm-spinlock.md)。|
|0x0004000A | 指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [SpinlockRelease](../devtest/wdm-spinlockrelease.md)。|
|0x0004000E |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [GuardedRegions](../devtest/wdm-guardedregions.md)。|
|0x0004100B |指向描述违反规则条件的字符串的指针。|保留 (未使用) |保留 (未使用) |驱动程序违反了 DDI 相容性规则 [RequestedPowerIrp](../devtest/wdm-requestedpowerirp.md)。|
|0x0004100F |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [IoSetCompletionExCompleteIrp](../devtest/wdm-iosetcompletionexcompleteirp.md)。|
|0x00043006 |指向描述违反规则条件的字符串的指针。|保留 (未使用) |保留 (未使用) |驱动程序违反了 DDI 相容性规则 [PnpRemove](../devtest/wdm-pnpremove.md)。|

### <a name="0x00081001-to-0x00082005---avstream-driver-compliance-rule-violations"></a>0x00081001 到 0x00082005-AVStream 驱动程序符合性规则冲突

|参数 1|参数2|参数3|参数4|错误的原因|
|--- |--- |--- |--- |--- |
|0x00081001 |指向描述违反规则条件的字符串的指针。 |内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [KsDeviceMutex](../devtest/ks-ksdevicemutex.md)。|
|0x00081002 |指向描述违反规则条件的字符串的指针。 |内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [KsStreamPointerClone](../devtest/ks-ksstreampointerclone.md)。|
|0x00081003 |指向描述违反规则条件的字符串的指针。 |保留 (未使用) |保留 (未使用) |驱动程序违反了 DDI 相容性规则 [KsStreamPointerLock](../devtest/ks-ksstreampointerlock.md)。|
|0x00081004 |指向描述违反规则条件的字符串的指针。 |内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [KsStreamPointerUnlock](../devtest/ks-ksstreampointerunlock.md)。|
|0x00081005 |指向描述违反规则条件的字符串的指针。 |保留 (未使用) |保留 (未使用) |驱动程序违反了 DDI 相容性规则 [KsCallbackReturn](../devtest/ks-kscallbackreturn.md)。|
|0x00081006 |指向描述违反规则条件的字符串的指针。 |内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [KsIrqlDeviceCallbacks](../devtest/ks-ksirqldevicecallbacks.md)。|
|0x00081007 |指向描述违反规则条件的字符串的指针。 |内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [KsIrqlFilterCallbacks](../devtest/ks-ksirqlfiltercallbacks.md)。|
|0x00081008 |指向描述违反规则条件的字符串的指针。 |内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [KsIrqlPinCallbacks](../devtest/ks-ksirqlpincallbacks.md)。|
|0x00081009 |指向描述违反规则条件的字符串的指针。 |保留 (未使用) |保留 (未使用) |驱动程序违反了 DDI 相容性规则  [KsIrqlDDIs](../devtest/ks-ksirqlddis.md)。|
|0x0008100A |指向描述违反规则条件的字符串的指针。 |内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [KsFilterMutex](../devtest/ks-ksfiltermutex.md)。|
|0x0008100B |指向描述违反规则条件的字符串的指针。 |内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [KsProcessingMutex](../devtest/ks-ksprocessingmutex.md)。|
|0x0008100C |指向描述违反规则条件的字符串的指针。 |内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [KsInvalidStreamPointer](../devtest/ks-ksinvalidstreampointer.md)。|
|0x00082001 |指向描述违反规则条件的字符串的指针。 |内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [KsTimedPinSetDeviceState](../devtest/ks-kstimedpinsetdevicestate.md)。|
|0x00082002 |指向描述违反规则条件的字符串的指针。 |内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [KsTimedDeviceCallbacks](../devtest/ks-kstimeddevicecallbacks.md)。|
|0x00082003 |指向描述违反规则条件的字符串的指针。 |内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [KsTimedFilterCallbacks](../devtest/ks-kstimedfiltercallbacks.md)。|
|0x00082004 |指向描述违反规则条件的字符串的指针。 |内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [KsTimedPinCallbacks](../devtest/ks-kstimedpincallbacks.md)。|
|0x00082005 |指向描述违反规则条件的字符串的指针。 |内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [KsTimedProcessingMutex](../devtest/ks-kstimedprocessingmutex.md)。|


### <a name="0x00091001-to-0x0009400c---ndis-ddi-compliance-rule-violations"></a>0x00091001 到 0x0009400C-NDIS DDI 相容性规则冲突

|参数 1|参数2|参数3|参数4|错误的原因|
|--- |--- |--- |--- |--- |
|0x00091001 |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [NdisOidComplete](../devtest/ndis-ndisoidcomplete.md)。|
|0x00091002 |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [NdisOidDoubleComplete](../devtest/ndis-ndisoiddoublecomplete.md)。|
|0x0009100E |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 DDI 相容性规则 [NdisOidDoubleRequest](../devtest/ndis-ndisoiddoublerequest.md)。|
|0x00092003 |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 NDIS/WIFI 验证规则 [NdisTimedOidComplete](../devtest/ndis-ndistimedoidcomplete.md)。|
|0x0009200D |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 NDIS/WIFI 验证规则 [NdisTimedDataSend](../devtest/ndis-ndistimeddatasend.md)。|
|0x0009200F |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 NDIS/WIFI 验证规则 [NdisTimedDataHang](../devtest/ndis-ndistimeddatahang.md)。|
|0x00092010 |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。 |驱动程序违反了 NDIS/WIFI 验证规则 [NdisFilterTimedPauseComplete](../devtest/ndisfiltertimedpausecomplete-.md)。|
|0x00092011 |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。 |驱动程序违反了 NDIS/WIFI 验证规则 [NdisFilterTimedDataSend](../devtest/ndisfiltertimeddatasend.md)。|
|0x00092012 |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。 |驱动程序违反了 NDIS/WIFI 验证规则 [NdisFilterTimedDataReceive](../devtest/ndisfiltertimeddatareceive.md)。|
|0x00093004 |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 NDIS/WIFI 验证规则 [WlanAssociation](../devtest/ndis-wlanassociation.md)。|
|0x00093005 |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 NDIS/WIFI 验证规则 [WlanConnectionRoaming](../devtest/ndis-wlanconnectionroaming.md)。|
|0x00093006 |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 NDIS/WIFI 验证规则 [WlanDisassociation](../devtest/ndis-wlandisassociation.md)。|
|0x00093101|指向描述违反规则条件的字符串的指针。 |保留 (未使用) |保留 (未使用) |驱动程序违反了 NDIS/WIFI 验证规则 [WlanAssert](../devtest/ndis-wlanassert.md)。|
|0x00094007 |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 NDIS/WIFI 验证规则 [WlanTimedAssociation](../devtest/ndis-wlantimedassociation.md)。|
|0x00094008 |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 NDIS/WIFI 验证规则 [WlanTimedConnectionRoaming](../devtest/ndis-wlantimedconnectionroaming.md)。|
|0x00094009 |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 NDIS/WIFI 验证规则 [WlanTimedConnectRequest](../devtest/ndis-wlantimedconnectrequest.md)。|
|0x0009400B |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 NDIS/WIFI 验证规则 [WlanTimedLinkQuality](../devtest/ndis-wlantimedlinkquality.md)。|
|0x0009400C |指向描述违反规则条件的字符串的指针。|内部规则状态 (第二个参数到！ ruleinfo) 的地址。|补充状态的地址 (第三个参数附加到！ ruleinfo) 。|驱动程序违反了 NDIS/WIFI 验证规则 [WlanTimedScan](../devtest/ndis-wlantimedscan.md)。|

<a name="cause"></a>原因
-----

有关原因的说明，请参阅参数部分中每个代码的说明。 可以通过使用 [**！分析-v**](-analyze.md) 扩展来获取进一步的信息。

<a name="resolution"></a>解决方法
----------

此 bug 检查只能在已指示驱动程序验证器监视一个或多个驱动程序时出现。 如果你不打算使用驱动程序验证程序，则应停用它。 你还可以考虑删除导致此问题的驱动程序。

如果您是驱动程序编写者，请使用通过此 bug 检查获取的信息来修复代码中的 bug。

有关驱动程序验证程序的完整详细信息，请参阅 [驱动程序验证](../devtest/driver-verifier.md)器。

<a name="remarks"></a>备注
-------

\_池 \_ 类型代码在 Ntddk 中进行枚举。 具体而言， **0** (零) 指示非分页池， **1** (一个) 表示页面缓冲池。

* (windows 8 及更高版本的 windows) * 如果 [DDI 相容性检查](../devtest/ddi-compliance-checking.md) 导致错误检查，请在驱动程序源代码上运行 [静态驱动程序验证](../devtest/static-driver-verifier.md) 程序，并指定由参数1值标识 (由导致 BUG 检查) 的 ddi 相容性规则。 静态驱动程序验证程序可帮助您在源代码中找到问题的原因。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅

[在启用驱动程序验证程序的情况下处理 Bug 检查](handling-a-bug-check-when-driver-verifier-is-enabled.md)