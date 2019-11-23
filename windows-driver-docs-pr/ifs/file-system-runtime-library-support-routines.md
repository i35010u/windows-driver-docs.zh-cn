---
title: 文件系统运行时库支持例程
description: 文件系统运行时库支持例程
ms.assetid: e3c2e109-891a-494a-b62c-e6ccc7afc9d8
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: c4858296e65e288f9d84bdf18793b7755d210bbc
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955783"
---
# <a name="file-system-runtime-library-support-routines"></a>文件系统运行时库支持例程

以下系统提供的文件系统运行时库支持函数和宏可以由内核模式文件系统和文件系统筛选器驱动程序调用。 它们按字母顺序列出。

**头文件：** *ntifs*

**前缀： FsRtl * Xxx***

| 函数或宏 | 描述 |
| ----------------- | ----------- |
| **FsRtlAcknowledgeEcp** | 将额外的 create parameter （ECP）上下文结构标记为已确认。 |
| **FsRtlAcquireFileExclusive** | 保留供系统使用。 |
| **FsRtlAddLargeMcbEntry** | 将新的映射添加到现有的地图控制块（MCB）。 |
| **FsRtlAddMcbEntry** | 已过时。 |
| **FsRtlAddToTunnelCache** | 缓存在重命名或删除文件时从目录中删除的文件名。 |
| **FsRtlAllocateExtraCreateParameter** | 为用户定义的额外 create 参数（ECP）上下文结构分配内存并生成指向该结构的指针。 |
| **FsRtlAllocateExtraCreateParameterFromLookasideList** | 从给定的后备链表列表中为额外的 create parameter （ECP）上下文结构分配内存池，并生成指向该结构的指针。 |
| **FsRtlAllocateExtraCreateParameterList** | 为 ECP_LIST 结构分配分页池内存，并生成指向该结构的指针。 |
| **FsRtlAllocateFileLock** | 分配并初始化新的 FILE_LOCK 结构。 |
| **FsRtlAllocatePool** | 已过时。 |
| **FsRtlAllocatePoolWithQuota** | 已过时。 |
| **FsRtlAllocatePoolWithQuotaTag** | 分配池内存，根据当前进程充电配额。 |
| **FsRtlAllocatePoolWithTag** | 分配池内存。 |
| **FsRtlAllocateResource** | 已过时。 |
| **FsRtlAreNamesEqual** | 确定两个 Unicode 字符串是否相等。 |
| **FsRtlAreThereCurrentFileLocks** | 检查指定文件是否存在任何字节范围锁。 |
| **FsRtlAreThereCurrentOrInProgressFileLocks** | 确定是否为文件分配了字节范围锁或对该文件进行的任何锁定操作。
| **FsRtlAreThereWaitingFileLocks** | 检查文件锁定队列是否有任何等待的文件锁定。 |
| **FsRtlAreVolumeStartupApplicationsComplete** | 确定卷启动应用程序是否已完成处理。 |
| **FsRtlBalanceReads** | 向容错磁盘驱动程序发出信号，表明现在可以安全地开始平衡镜像驱动器的读取。 |
| **FsRtlCancellableWaitForMultipleObjects** | 对一个或多个调度程序对象执行可取消等待操作（可终止的等待）。 |
| **FsRtlCancellableWaitForSingleObject** | 执行调度程序对象上的可取消等待操作（可终止等待）。 |
| **FsRtlChangeBackingFileObject** | 将当前文件对象替换为新的文件对象。 |
| **FsRtlCheckLockForReadAccess** | 确定与给定 IRP 关联的进程是否具有对文件锁定区域的读取访问权限。 |
| **FsRtlCheckLockForWriteAccess** | 确定与给定 IRP 关联的进程对文件锁定区域是否具有写入访问权限。 |
| **FsRtlCheckLockForOplockRequest** | 检查文件分配大小内的锁。 检查 file lock 对象是否存在将阻止对 oplock 请求授予的字节范围锁。 |
| **FsRtlCheckOplock** | 使用文件的当前机会锁（oplock）状态同步文件 i/o 操作的 IRP。 |
| **FsRtlCheckOplockEx** | 使用文件的当前机会锁（oplock）状态同步文件 i/o 操作的 IRP。 |
| **FsRtlCheckUpperOplock** | 当 oplock 保存更改状态时，提供辅助或分层文件系统中的机会锁（oplock）检查。 |
| **FsRtlCompleteRequest** | 完成具有指定状态的 IRP。 |
| **FsRtlCopyRead** | 将数据从缓存文件复制到用户缓冲区。 |
| **FsRtlCopyWrite** | 将数据从用户缓冲区复制到缓存文件。 |
| **FsRtlCreateSectionForDataScan** | 创建节对象。 请特别小心使用此例程。 |
| **FsRtlCurrentBatchOplock** | 文件系统或筛选器驱动程序调用此例程来确定文件是否有任何批处理或筛选器机会锁（oplock）。 |
| **FsRtlCurrentOplock** | 文件系统或筛选器驱动程序调用此例程来确定文件是否有任何机会锁（oplock）。 |
| **FsRtlCurrentOplockH** | 文件系统或筛选器驱动程序调用此例程来确定文件是否存在任何 CACHE_HANDLE_LEVEL 机会锁（oplock）。 |
| **FsRtlDeleteExtraCreateParameterLookasideList** | 释放额外的 create parameter （ECP）后备链表 list。 |
| **FsRtlDeleteKeyFromTunnelCache** | 删除正在删除的目录中的文件的任何隧道缓存条目。 |
| **FsRtlDeleteTunnelCache** | 删除隧道缓存。 |
| **FsRtlDeregisterUncProvider** | 注销使用多 UNC 提供程序（MUP）注册为通用命名约定（UNC）提供程序的重定向程序。 |
| **FsRtlDissectDbcs** | 给定 ANSI 或双字节字符集（DBCS）路径名字符串，此例程将返回两个字符串：一个包含字符串中找到的第一个文件名，另一个包含路径名字符串的剩余未分析部分。 |
| **FsRtlDissectName** | 给定一个 Unicode 路径名字符串，此例程将返回两个字符串：一个包含字符串中找到的第一个文件名，另一个包含路径名字符串的剩余未分析部分。 |
| **FsRtlDoesDbcsContainWildCards** | 确定 ANSI 或双字节字符集（DBCS）字符串是否包含通配符。 |
| **FsRtlDoesNameContainWildCards** | 确定 Unicode 字符串是否包含通配符。 |
| **FsRtlEnterFileSystem** | 暂时禁用正常内核模式异步过程调用（APC）的传送。 还提供了特殊的内核模式 Apc。
| **FsRtlExitFileSystem** | 重新启用正常内核模式 Apc 的传递，这些功能由前面对**FsRtlEnterFileSystem**的调用禁用。 |
| **FsRtlFastCheckLockForRead** | 确定指定进程是否对文件的锁定字节范围具有读取访问权限。 |
| **FsRtlFastCheckLockForWrite** | 确定指定进程是否对文件的锁定字节范围具有写入访问权限。 |
| **FsRtlFastLock** | 由文件系统和筛选器驱动程序用于请求文件流的字节范围锁。 |
| **FsRtlFastUnlockAll** | 释放由指定进程为文件获取的所有字节范围锁。 |
| **FsRtlFastUnlockAllByKey** | 释放由指定的进程使用指定的键值为文件获取的所有字节范围锁。 |
| **FsRtlFastUnlockSingle** | 使用指定的键值、文件偏移量和长度（对于文件），释放由指定进程获取的字节范围锁。 |
| **FsRtlFindExtraCreateParameter** | 在给定的 ECP 列表中搜索给定类型的 ECP 上下文结构，如果找到，则返回指向此结构的指针。 |
| **FsRtlFindInTunnelCache** | 在隧道缓存中搜索与指定名称匹配的匹配项。 |
| **FsRtlFreeExtraCreateParameter** | 释放 ECP 上下文结构的内存。 |
| **FsRtlFreeExtraCreateParameterList** | 释放额外的 create parameter （ECP）列表结构。 |
| **FsRtlFreeFileLock** | 取消和释放文件锁结构。 |
| **FsRtlGetEcpListFromIrp** | 返回一个指针，该指针指向与给定 IRP_MJ_CREATE 操作关联的额外创建参数（ECP）上下文结构列表。 |
| **FsRtlGetFileSize** | 用于获取文件的大小。 |
| **FsRtlGetNextExtraCreateParameter** | 返回一个指针，该指针指向给定 ECP 列表中的下一个（或第一个）额外 create 参数（ECP）上下文结构。 |
| **FsRtlGetNextFileLock** | 用于枚举指定文件当前存在的字节范围锁。 |
| **FsRtlGetNextLargeMcbEntry** | 从地图控制块（MCB）检索映射运行。 |
| **FsRtlGetNextMcbEntry** | 已过时。 |
| **FsRtlGetPerFileContextPointer** | 返回打开的文件的*FileContextSupportPointer* 。 |
| **FsRtlGetPerStreamContextPointer** | 返回文件流的文件系统的流上下文。 |
| **FsRtlGetSectorSizeInformation** | 检索存储卷的物理和逻辑扇区大小信息。 |
| **FsRtlGetSupportedFeatures** | 返回附加到指定设备对象的卷支持的功能。 |
| **FsRtlIncrementCcFastMdlReadWait** | 在处理器控制块（PRCB）对象中递增缓存管理器的 CcFastMdlReadWait 性能计数器成员。 |
| **FsRtlIncrementCcFastReadNotPossible** | 递增缓存管理器系统计数器的每个处理器控制块中的**CcFastReadNotPossible**性能计数器。 |
| **FsRtlIncrementCcFastReadNoWait** | 递增缓存管理器系统计数器的每个处理器控制块中的**CcFastReadNoWait**性能计数器。 |
| **FsRtlIncrementCcFastReadResourceMiss** | 递增缓存管理器系统计数器的每个处理器控制块中的**CcFastReadNotPossible**性能计数器。 |
| **FsRtlIncrementCcFastReadWait** | 递增缓存管理器系统计数器的每个处理器控制块中的**CcFastReadWait**性能计数器。 |
| **FsRtlInitExtraCreateParameterLookasideList** | 初始化分页或非分页池后备链表列表，用于分配固定大小的一个或多个额外 create create 参数上下文结构（ECPs）。 |
| **FsRtlInitializeExtraCreateParameter** | 初始化额外的 create parameter （ECP）上下文结构。 |
| **FsRtlInitializeExtraCreateParameterList** | 初始化额外的 create parameter （ECP）上下文结构列表。 |
| **FsRtlInitializeFileLock** | 初始化 FILE_LOCK 结构。 |
| **FsRtlInitializeLargeMcb** | 初始化地图控制块（MCB）结构。 |
| **FsRtlInitializeMcb** | 已过时。 |
| **FsRtlInitializeOplock** | 初始化机会锁（oplock）指针。 |
| **FsRtlInitializeTunnelCache** | 为卷初始化新的隧道缓存。 |
| **FsRtlInitPerFileContext** | 初始化 FSRTL_PER_FILE_CONTEXT 结构。 |
| **FsRtlInitPerFileObjectContext** | 初始化 FSRTL_PER_FILEOBJECT_CONTEXT 结构。 |
| **FsRtlInitPerStreamContext** | 初始化筛选器驱动程序的上下文结构。 |
| **FsRtlInsertExtraCreateParameter** | 在 ECP 列表中插入额外的 create parameter （ECP）上下文结构。 |
| **FsRtlInsertPerFileContext** | 将 FSRTL_PER_FILE_CONTEXT 对象与文件的驱动程序指定的上下文对象相关联。 |
| **FsRtlInsertPerFileObjectContext** | 对于 "旧式" 文件系统筛选器驱动程序， | \* * FsRtlInsertPerFileObjectContext 函数将上下文信息与文件对象相关联。 |
| **FsRtlInsertPerStreamContext** | 将文件系统筛选器驱动程序的每个流的上下文结构与文件流相关联。 |
| **FsRtlIsAnsiCharacterLegal** | 确定字符是否为合法的 ANSI 字符。 |
| **FsRtlIsAnsiCharacterLegalFat** | 确定 ANSI 字符对于 FAT 文件名是否合法。 |
| **FsRtlIsAnsiCharacterLegalHpfs** | 确定 ANSI 字符对 HPFS 文件名是否合法。 |
| **FsRtlIsAnsiCharacterLegalNtfs** | 确定 ANSI 字符对于 NTFS 文件名是否合法。 |
| **FsRtlIsAnsiCharacterLegalNtfsStream** | 确定 ANSI 字符对于 NTFS 流名称是否合法。 |
| **FsRtlIsAnsiCharacterWild** | 确定 ANSI 字符是否为通配符。 |
| **FsRtlIsDbcsInExpression** | 确定 ANSI 或双字节字符集（DBCS）字符串是否与指定的模式匹配。 |
| **FsRtlIsEcpAcknowledged** | 确定给定的额外 create 参数（ECP）上下文结构是否已标记为已确认。 |
| **FsRtlIsEcpFromUserMode** | 确定是否从用户模式产生额外的 create parameter （ECP）上下文结构。 |
| **FsRtlIsFatDbcsLegal** | 确定指定的 ANSI 或双字节字符集（DBCS）字符串是否为合法的 FAT 文件名。 |
| **FsRtlIsHpfsDbcsLegal** | 确定指定的 ANSI 或双字节字符集（DBCS）字符串是否为合法的 HPFS 文件名。 |
| **FsRtlIsLeadDbcsCharacter** | 确定字符是否是双字节字符集（DBCS）中的前导字节（字符的第一个字节）。 |
| **FsRtlIsNameInExpression** | 确定 Unicode 字符串是否与指定的模式匹配。 |
| **FsRtlIsNtstatusExpected** | 确定异常筛选器是否处理指定的异常。 |
| **FsRtlIsPagingFile** | 确定给定的文件是否为页面文件。 |
| **FsRtlIssueDeviceIoControl** | 将同步设备 i/o 控制请求发送到目标设备对象。 |
| **FsRtlIsSystemPagingFile** | 确定给定文件当前是否为系统分页文件。 |
| **FsRtlIsTotalDeviceFailure** | 确定是否发生了介质或其他硬件故障。 |
| **FsRtlIsUnicodeCharacterWild** | 确定 Unicode 字符是否为通配符。 |
| **FsRtlLogCcFlushError** | 记录丢失的延迟写入错误并向用户显示一个对话框。 |
| **FsRtlLookupLargeMcbEntry** | 给定一个虚拟块号（VBN）和一个地图控制块（MCB）后，此例程会在 MCB 中搜索对应于指定 VBN 的映射信息。 |
| **FsRtlLookupLastLargeMcbEntry** | 检索存储在地图控制块（MCB）中的最后一个映射条目。 |
| **FsRtlLookupLastLargeMcbEntryAndIndex** | 检索存储在给定地图控制块（MCB）中的最后一个映射条目。 |
| **FsRtlLookupLastMcbEntry** | 已过时。 |
| **FsRtlLookupMcbEntry** | 已过时。 |
| **FsRtlLookupPerFileContext** | 返回一个指向与指定文件关联的 FSRTL_PER_FILE_CONTEXT 对象的指针。 |
| **FsRtlLookupPerFileObjectContext** | 对于 "旧式" 文件系统筛选器驱动程序，此函数检索以前与 file 对象关联的上下文信息。 |
| **FsRtlLookupPerStreamContext** | 检索文件流的每个流的上下文结构。 |
| **FsRtlLookupPerStreamContextInternal** | 保留供系统使用。 |
| **FsRtlMdlReadCompleteDev** | 完成**FsRtlMdlReadDev**例程启动的读取操作。 |
| **FsRtlMdlReadDev** | 返回一个内存描述符列表（MDL），该列表直接指向文件缓存中的指定字节范围。 |
| **FsRtlMdlReadEx** | 执行快速缓存的 MDL 读取。 如果未缓存请求的数据，则例程会恢复为基于 IRP 的 MDL 读取操作。 |
| **FsRtlMdlWriteCompleteDev** | 释放**FsRtlPrepareMdlWriteDev**分配的资源。 |
| **FsRtlMupGetProviderIdFromName** | 获取网络重定向程序的提供程序标识符，该标识符从网络重定向程序的设备名称注册到多 UNC 提供程序（MUP）。 |
| **FsRtlMupGetProviderInfoFromFileObject** | 从位于远程文件系统上的文件的文件对象中获取注册到多 UNC 提供程序（MUP）的网络重定向程序的相关信息。 |
| **FsRtlNormalizeNtstatus** | 将任意异常转换为由异常筛选器处理的状态值。 |
| **FsRtlNotifyCleanup** | 当释放文件对象的最后一个句柄时，此例程将从指定的通知列表中删除该文件对象的通知结构（如果存在）。 |
| **FsRtlNotifyCleanupAll** | Temoves 指定通知列表的所有成员。 |
| **FsRtlNotifyFilterChangeDirectory** | 为 IRP_MN_NOTIFY_CHANGE_DIRECTORY 请求创建通知结构，并将其添加到指定的通知列表。 |
| **Fsrtlnotifyfilterreportchange 并且** | 完成指定通知列表中挂起 IRP_MN_NOTIFY_CHANGE_DIRECTORY 请求。 |
| **FsRtlNotifyFullChangeDirectory** | 为通知请求创建通知结构，并将其添加到指定的通知列表。 |
| **FsRtlNotifyFullReportChange** | 完成挂起的通知更改 Irp。 |
| **FsRtlNotifyInitializeSync** | 分配并初始化通知列表的同步对象。 |
| **FsRtlNotifyUninitializeSync** | 释放通知列表的同步对象。 |
| **FsRtlNotifyVolumeEvent** | 通知所有已注册的应用程序发生卷事件。 |
| **FsRtlNotifyVolumeEventEx** | 通知所有已注册的应用程序发生卷事件。 卷事件包括正在锁定、未锁定、已装载或已设为只读的卷。 |
| **FsRtlNumberOfRunsInLargeMcb** | 返回地图控制块（MCB）中的运行数。 |
| **FsRtlNumberOfRunsInMcb** | 已过时。 |
| **FsRtlOplockBreakH** | 中断 CACHE_HANDLE_LEVEL 机会锁（oplock）。 |
| **FsRtlOplockBreakToNone** | 已过时。 |
| **FsRtlOplockBreakToNoneEx** | 立即中断所有机会锁（oplock），而不考虑任何 oplock 项。 |
| **FsRtlOplockFsctrl** | 代表文件系统或筛选器驱动程序执行各种机会锁（oplock）操作。 |
| **FsRtlOplockFsctrlEx** | 代表文件系统或筛选器驱动程序执行各种机会锁（oplock）操作。 |
| **FsRtlOplockIsFastIoPossible** | 检查文件的机会锁（oplock）状态，以确定是否可以对文件执行快速 i/o。 |
| **FsRtlOplockIsSharedRequest** | 确定对机会锁（oplock）的请求是否需要共享 oplock。 |
| **FsRtlOplockKeysEqual** | 比较存储在两个文件对象的文件对象扩展中的机会锁（oplock）键。 |
| **FsRtlPostPagingFileStackOverflow** | 将分页文件堆栈溢出项发布到堆栈溢出线程。 |
| **FsRtlPostStackOverflow** | 将堆栈溢出项发布到堆栈溢出线程。 |
| **FsRtlPrepareMdlWriteDev** | 返回连接到指定范围的内存描述符列表（MDLs）的内存描述符列表，该列表将数据直接写入缓存。 |
| **FsRtlPrepareMdlWriteEx** | 返回连接到指定范围的内存描述符列表（MDLs）的内存描述符列表，该列表将数据直接写入缓存。 如果写入的缓存支持不可用，则例程会恢复为基于 IRP 的 MDL 写入操作。 |
| **FsRtlPrepareToReuseEcp** | 重置额外的 create parameter （ECP）上下文结构，使其做好重复使用的准备。 |
| **FsRtlPrivateLock** | 已过时。 |
| **FsRtlProcessFileLock** | 处理和完成文件锁定操作的 IRP。 |
| **FsRtlQueryCachedVdl** | 检索缓存文件的当前有效数据长度（VDL）。 |
| **FsRtlRegisterFileSystemFilterCallbacks** | 文件系统筛选器驱动程序和文件系统调用此例程来注册当基础文件系统执行特定操作时要调用的通知回调例程。 |
| **FsRtlRegisterUncProvider** | 使用系统多 UNC 提供程序（MUP）将网络重定向程序注册为通用命名约定（UNC）提供程序。 |
| **FsRtlRegisterUncProviderEx** | 使用系统多 UNC 提供程序（MUP）将网络重定向程序注册为通用命名约定（UNC）提供程序。 |
| **FsRtlReleaseFile** | 保留供系统使用。 |
| **FsRtlRemoveDotsFromPath** | 删除不必要的 "." 和 "..." 从指定的路径。 |
| **FsRtlRemoveExtraCreateParameter** | 在 ECP 列表中搜索 ECP 上下文结构，如果找到，则将其从 ECP 列表中分离。 |
| **FsRtlRemoveLargeMcbEntry** | 从地图控制块（MCB）中删除一个或多个映射。 |
| **FsRtlRemoveMcbEntry** | 已过时。 |
| **FsRtlRemovePerFileContext** | 返回一个指向与文件关联的**FSRTL_PER_FILE_CONTEXT 对象**的指针。 **FsRtlRemovePerFileContext**将从它所占用的列表中删除**FSRTL_PER_FILE_CONTEXT**对象以及关联的特定于驱动程序的上下文信息。 |
| **FsRtlRemovePerFileObjectContext** | 对于 "旧式" 文件系统筛选器驱动程序，此函数将从以前与 file 对象关联的每个文件对象上下文的列表中断开每个文件对象的上下文信息结构。 |
| **FsRtlRemovePerStreamContext** | 从与文件流关联的每个流的上下文列表中删除每个流的上下文结构。 |
| **FsRtlResetLargeMcb** | 截断地图控制块（MCB）结构，使其包含零个映射对。 它不会收缩映射对数组。 |
| **FsRtlSetEcpListIntoIrp** | 将额外的 create parameter （ECP）上下文列表附加到 IRP_MJ_CREATE 操作。 |
| **FsRtlSetupAdvancedHeader** | 由文件系统用来初始化用于筛选上下文的 * * FSRTL_ADVANCED_FCB_HEADER 结构。 |
| **FsRtlSetupAdvancedHeaderEx** | 由文件系统用来初始化 | 用于流和文件上下文的**FSRTL_ADVANCED_FCB_HEADER**结构。 |
| **FsRtlSplitLargeMcb** | 将一个洞插入地图控制块（MCB）中的映射。 |
| **FsRtlSupportsPerFileContexts** | 检查与指定 FILE_OBJECT 关联的文件系统是否支持每个文件上下文信息。 |
| **FsRtlSupportsPerStreamContexts** | 确定文件系统是否支持给定文件流的每个流的上下文。 |
| **FsRtlTeardownPerFileContexts** | 文件系统调用此例程来释放与文件控制块（FCB）结构关联的**FSRTL_PER_FILE_CONTEXT**对象。 |
| **FsRtlTeardownPerStreamContexts** | 释放与给定的所有关联的每个流的上下文结构 | \* * FsRtl_ADVANCED_FCB_HEADER 结构。 |
| **FsRtlTestAnsiCharacter** | 确定 ANSI 或双字节字符集（DBCS）字符是否满足指定的条件。 |
| **FsRtlTruncateLargeMcb** | 截断大地图控制块（MCB）。 |
| **FsRtlTruncateMcb** | 已过时。 |
| **FsRtlUninitializeFileLock** | 取消 FILE_LOCK 结构。 |
| **FsRtlUninitializeLargeMcb** | 取消大型地图控制块（MCB）。 |
| **FsRtlUninitializeMcb** | 已过时。 |
| **FsRtlUninitializeOplock** | 取消机会锁（oplock）指针。 |
| **FsRtlUpperOplockFsctrl**处理辅助或分层文件系统的机会锁（oplock）请求和确认。 |
| **FsRtlValidateReparsePointBuffer**| 验证指定的重新分析点缓冲区是否有效。 |
