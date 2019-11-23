---
title: 微筛选器驱动程序支持例程
description: 微筛选器驱动程序支持例程
ms.assetid: ef3db0c7-7892-44dc-90ab-a1046e7d4af8
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: ba8c38d7558af2d431ddc7fa865c355132f05523
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955785"
---
# <a name="fltxxx-minifilter-support-routines"></a>FltXxx 微筛选器支持例程

以下系统提供的**Flt**_Xxx_支持函数和宏可由内核模式微筛选器驱动程序调用，但不能作为其他设备驱动程序调用。 它们按字母顺序列出。

**头文件：** *fltkernel*

**前缀： Flt**_Xxx_

| 函数或宏 | 描述 |
| ----------------- | ----------- |
| **FLT_IS_FASTIO_OPERATION** | 确定给定的回调数据结构是否表示快速 i/o 操作。 |
| **FLT_IS_FS_FILTER_OPERATION** | 确定给定的回调数据结构是否表示旧的文件系统筛选器（FSFilter）回调操作。 |
 | **FLT_IS_IRP_OPERATION** | 确定给定的回调数据结构是否表示基于 i/o 请求数据包（IRP）的 i/o 操作。 |
 | **FLT_IS_REISSUED_IO** | 确定给定的回调数据结构是否表示重新颁发的 i/o 操作。 |
 | **FLT_IS_SYSTEM_BUFFER** | 测试回调数据结构中的系统缓冲区标志。 |
 | **FltAcknowledgeEcp** | 将额外的 create 参数上下文（ECP）标记为已确认。 |
 | **FltAcquirePushLockExclusive** | 获取给定的推送锁以供调用线程独占访问。 |
 | **FltAcquirePushLockShared** | 通过调用线程获取给定的用于共享访问的推送锁。 |
 | **FltAcquireResourceExclusive** | 获取给定资源以供调用线程独占访问。 |
 | **FltAcquireResourceShared** | 为调用线程获取共享访问的给定资源。 |
 | **FltAdjustDeviceStackSizeForIoRedirection** | 增大源设备堆栈的大小，以允许微筛选器在目标堆栈比源堆栈更深层时将指定源实例中的 i/o 重定向到指定的目标实例。 |
 | **FltAllocateCallbackData** | 分配一个回调数据结构，微筛选器驱动程序可以使用该结构来启动 i/o 请求。 |
 | **FltAllocateCallbackDataEx** | 分配回调数据结构，并可以为微筛选器驱动程序可用于启动 i/o 请求的其他结构预分配内存。 |
 | **FltAllocateContext** | 为指定的上下文类型分配上下文结构。 |
 | **FltAllocateDeferredIoWorkItem** | 分配一个延迟 i/o 工作项。 |
| **FltAllocateExtraCreateParameter** | 为用户定义的额外 create 参数（ECP）上下文结构分配分页内存池，并生成指向该结构的指针。 |
 | **FltAllocateExtraCreateParameterFromLookasideList** | 从给定的后备链表列表中为额外的 create parameter （ECP）上下文结构分配内存池，并生成指向该结构的指针。 |
 | **FltAllocateExtraCreateParameterList** | 为额外的 create parameter （ECP）列表结构分配分页池内存，并生成指向该结构的指针。 |
 | **FltAllocateFileLock** | 分配并初始化新的 FILE_LOCK 结构。 |
 | **FltAllocateGenericWorkItem** | 分配一个通用工作项。 |
 | **FltAllocatePoolAlignedWithTag** | 分配用于非缓存 i/o 操作的设备对齐缓冲区。 |
 | **FltApplyPriorityInfoThread** | 由微筛选器驱动程序用于将优先级信息应用于线程。 |
 | **FltAttachVolume** | 创建新的微筛选器驱动程序实例，并将其附加到给定的卷。 |
 | **FltAttachVolumeAtAltitude** | 调试支持例程，它将微筛选器驱动程序实例附加到指定高度的某个卷，替代微筛选器驱动程序的 INF 文件中的任何设置。 |
 | **FltBuildDefaultSecurityDescriptor** | 生成用于 FltCreateCommunicationPort 的默认安全描述符 **。** |
 | **FltCancelFileOpen** | 导致新打开或创建的文件关闭。 |
 | **FltCancelIo** | 取消 i/o 操作。 |
 | **FltCancellableWaitForMultipleObjects** | 对一个或多个调度程序对象执行可取消等待操作（可终止的等待）。 |
**FltCancellableWaitForSingleObject** | 执行调度程序对象上的可取消等待操作（可终止等待）。 |
| **FltCbdqDisable** | 禁用微筛选器驱动程序的回调数据队列。 |
| **FltCbdqEnable** | 启用通过之前对**FltCbdqDisable**的调用而禁用的回调数据队列。 |
| **FltCbdqInitialize** | 初始化微筛选器驱动程序的回调数据队列调度表。 |
| **FltCbdqInsertIo** | 将 i/o 操作的回调数据结构插入微筛选器驱动程序的回调数据队列。 |
| **FltCbdqRemoveIo** | 从微筛选器驱动程序的回调数据队列中删除特定项。 |
| **FltCbdqRemoveNextIo** | 删除微筛选器驱动程序的回调数据队列中的下一个匹配项。 |
| **FltCheckAndGrowNameControl** | 检查 FLT_NAME_CONTROL 结构中的缓冲区是否足够大以容纳指定的字节数。 否则， **FltCheckAndGrowNameControl**会将其替换为较大的系统分配缓冲区。 |
| **FltCheckLockForReadAccess** | 确定调用方是否对文件的锁定字节范围具有读取访问权限。 |
| **FltCheckLockForWriteAccess** | 确定调用方是否对文件的锁定字节范围具有写入访问权限。 |
| **FltCheckOplock** | 将基于 IRP 的文件 i/o 操作的回调数据结构与文件的当前机会锁（oplock）状态进行同步。 |
| **FltCheckOplockEx** | 同步具有文件的当前机会锁（oplock）状态的基于 IRP 的文件 i/o 操作的回调数据结构。 |
| **FltClearCallbackDataDirty** | 清除回调数据结构中的回调脏标志。 |
| **FltClearCancelCompletion** | 清除为 i/o 操作指定的取消例程。 |
| **FltClose** | 关闭**FltCreateFile** **FltCreateFileEx**或**FltCreateFileEx2**打开的文件句柄。 |
| **FltCloseClientPort** | Coses 通信客户端端口。 |
| **FltCloseCommunicationPort** | 关闭微筛选器驱动程序的通信服务器端口。 |
| **FltCloseSectionForDataScan** | 关闭与文件流关联的 section 对象。 |
| **FltCommitComplete** | 确认 TRANSACTION_NOTIFY_COMMIT 通知。 |
| **FltCommitFinalizeComplete** | 确认 TRANSACTION_NOTIFY_COMMIT_FINALIZE 通知。 |
| **FltCompareInstanceAltitudes** | 比较两个微筛选器驱动程序实例的海拔高度。 |
| **FltCompletePendedPostOperation** | 恢复在微筛选器驱动程序的 postoperation 回调例程中挂起的 i/o 操作的完成处理。 |
| **FltCompletePendedPreOperation** | 恢复在微筛选器驱动程序的 preoperation 回调（PFLT_PRE_OPERATION_CALLBACK）例程中挂起的 i/o 操作的处理。 |
| **FltCreateCommunicationPort** | 创建一个通信服务器端口，微筛选器驱动程序可在此端口上接收来自用户模式应用程序的连接请求。 |
| **FltCreateFile** | 创建新文件或打开现有文件。 |
| **FltCreateFileEx** | 创建新文件或打开现有文件。 |
| **FltCreateFileEx2** | 创建新文件或打开现有文件。 此例程还包括一个可选的 create 上下文参数。 |
| **FltCreateMailslotFile** | 创建新的 mailslot 服务器或打开现有 mailslot。 |
| **FltCreateNamedPipeFile** | 创建新管道或打开现有管道。 |
| **FltCreateSectionForDataScan** | 为文件创建节对象。 筛选器管理器可以选择在创建的节中同步 i/o。 |
| **FltCreateSystemVolumeInformationFolder** | 验证文件系统卷上是否存在 "系统卷信息" 文件夹。 如果该文件夹不存在，则创建该文件夹。 |
| **FltCurrentBatchOplock** | 确定文件是否有任何批处理或筛选器机会锁（oplock）。 |
| **FltCurrentOplock** | 确定文件是否有任何机会锁（oplock）。 |
| **FltCurrentOplockH** | 确定文件是否存在任何 CACHE_HANDLE_LEVEL 机会锁（oplock）。 |
| **FltDecodeParameters** | 返回对 i/o 操作的内存描述符列表（MDL）地址、缓冲区指针、缓冲区长度和所需访问参数的指针。 这会使微筛选器驱动程序无需使用 switch 语句在帮助程序例程中查找这些参数的位置，这些参数可访问 MDL 地址、缓冲区指针、缓冲区长度和多种操作类型所需的访问权限。 |
| **FltDeleteContext** | 标记要删除的指定上下文。 |
| **FltDeleteExtraCreateParameterLookasideList** | 释放额外的 create parameter （ECP）后备链表 list。 |
| **FltDeleteFileContext** | 检索并删除给定的微筛选器驱动程序为给定文件设置的文件上下文。 |
| **FltDeleteInstanceContext** | 从给定的实例中删除上下文，并将上下文标记为删除。 |
| **FltDeletePushLock** | 删除给定的推送锁。 |
| **FltDeleteStreamContext** | 删除给定的微筛选器驱动程序实例已为给定流设置的上下文，并将上下文标记为要删除。 |
| **FltDeleteStreamHandleContext** | 删除给定的微筛选器驱动程序实例已为给定流句柄设置的上下文，并将上下文标记为要删除。 |
| **FltDeleteTransactionContext** | 从给定事务中删除上下文，并将上下文标记为删除。 |
| **FltDeleteVolumeContext** | 删除给定卷的给定微筛选器驱动程序设置的上下文，并将上下文标记为要删除。 |
| **FltDetachVolume** | 从卷中分离微筛选器驱动程序实例。 |
| **FltDeviceIoControlFile** | 将控制代码直接发送到指定的设备驱动程序，从而使相应的驱动程序执行指定的操作。 |
| **FltDoCompletionProcessingWhenSafe** | 如果可以安全地执行此操作，请执行微筛选器驱动程序 postoperation 回调例程。 |
| **FltEnlistInTransaction** | 在给定的事务中登记微筛选器驱动程序。 |
| **FltEnumerateFilterInformation** | 提供系统中所有已注册的筛选器驱动程序（包括微筛选器和旧式筛选器驱动程序）的相关信息。 |
| **FltEnumerateFilters** | 枚举系统中所有已注册的微筛选器驱动程序。 |
| **FltEnumerateInstanceInformationByDeviceObject** | 提供有关筛选器驱动程序实例和旧筛选器驱动程序的信息，这些驱动程序连接到与指定设备对象相关的卷。 |
| **FltEnumerateInstanceInformationByFilter** | 提供有关给定微筛选器驱动程序的实例的信息。 |
| **FltEnumerateInstanceInformationByVolume** | 提供有关连接到给定卷的微筛选器驱动程序实例和旧筛选器驱动程序（仅适用于 Windows Vista）的信息。 |
| **FltEnumerateInstanceInformationByVolumeName** | 提供有关筛选器驱动程序实例和旧筛选器驱动程序的信息，它们附加到具有指定名称的卷。 |
| **FltEnumerateInstances** | 枚举给定微筛选器驱动程序或卷的微筛选器驱动程序实例。 |
| **FltEnumerateVolumeInformation** | 提供有关筛选器管理器已知的卷的信息。 |
| **FltEnumerateVolumes** | 枚举系统中的所有卷。 |
| **FltFastIoMdlRead** | 返回一个内存描述符列表（MDL），该列表直接指向文件缓存中的指定字节范围。 |
| **FltFastIoMdlReadComplete** | 完成**FltFastIoMdlRead**例程启动的读取操作。 |
| **FltFastIoMdlWriteComplete** | 释放**FltFastIoPrepareMdlWrite**分配的资源。 |
| **FltFastIoPrepareMdlWrite** | 返回连接到指定范围的内存描述符列表（MDLs）的内存描述符列表，该列表将数据直接写入缓存。 |
| **FltFlushBuffers** | 将给定文件的刷新请求发送到文件系统。 |
| **FltFindExtraCreateParameter** | 在给定的 ECP 列表中搜索给定类型的 ECP 上下文结构，如果找到，则返回指向此结构的指针。 |
| **FltFreeCallbackData** | 释放由**FltAllocateCallbackData**例程分配的回调数据结构。 |
| **FltFreeDeferredIoWorkItem** | 释放由**FltAllocateDeferredIoWorkItem**例程分配的工作项。 |
| **FltFreeExtraCreateParameter** | 释放 ECP 上下文结构的内存。 |
| **FltFreeExtraCreateParameterList** | 释放额外的 create parameter （ECP）列表结构。 |
| **FltFreeFileLock** | 取消和释放已初始化的 FILE_LOCK 结构。 |
| **FltFreeGenericWorkItem** | 释放由**FltAllocateGenericWorkItem**例程分配的工作项。 |
| **FltFreePoolAlignedWithTag** | 释放由先前对**FltAllocatePoolAlignedWithTag**的调用分配的缓存对齐缓冲区。 |
| **FltFreeSecurityDescriptor** | 释放由**FltBuildDefaultSecurityDescriptor**例程分配的安全描述符。 |
| **FltFsControlFile** | 将控制代码直接发送到指定的文件系统或文件系统筛选器驱动程序，从而使相应的驱动程序执行指定的操作。 |
| **FltGetActivityIdCallbackData** | 检索与微筛选器的回调数据中的请求关联的当前活动 ID。 |
| **FltGetBottomInstance** | 为微筛选器驱动程序实例返回一个不透明的实例指针（如果有），该指针附加在给定卷的实例堆栈底部。 |
| **FltGetContexts** | 检索与当前操作相关的对象的微筛选器驱动程序上下文。 |
| **FltGetContextsEx** | 检索与当前操作相关的对象的微筛选器驱动程序上下文。 |
| **FltGetDestinationFileNameInformation** | 为正在重命名或正在为其创建 NTFS 硬链接的文件或目录构造完整的目标路径名。 |
| **FltGetDeviceObject** | 返回一个指针，该指针指向给定卷的筛选器管理器的卷设备对象（VDO）。 |
| **FltGetDiskDeviceObject** | 返回一个指向与给定卷关联的磁盘设备对象的指针。 |
| **FltGetEcpListFromCallbackData** | 返回一个指针，该指针指向与给定的创建操作回调数据对象关联的额外创建参数上下文（ECP）列表。 |
| **FltGetFileContext** | 检索给定微筛选器驱动程序实例为文件设置的上下文。 |
| **FltGetFileNameFormat** | 返回 * * FLT_FILE_NAME_OPTIONS 值的名称格式部分。 |
| **FltGetFileNameInformation** | 返回文件或目录的名称信息。 |
| **FltGetFileNameInformationUnsafe** | 返回打开的文件或目录的名称信息。 |
| **FltGetFileNameQueryMethod** | 返回 FLT_FILE_NAME_OPTIONS 值的名称查询方法部分。 |
| **FltGetFileSystemType** | 获取卷或实例对象，并提供卷的文件系统类型。 |
| **FltGetFilterFromInstance** | 返回创建给定实例的微筛选器驱动程序的不透明筛选器指针。 |
| **FltGetFilterFromName** | 为注册的微筛选器驱动程序返回一个不透明的筛选器指针，其名称与*FilterName*参数中的值相匹配。 |
| **FltGetFilterInformation** | 提供有关微筛选器驱动程序的信息。 |
| **FltGetInstanceContext** | 检索通过给定微筛选器驱动程序为实例设置的上下文。 |
| **FltGetInstanceInformation** | 返回有关微筛选器驱动程序实例的信息。 |
| **FltGetIoPriorityHint** | 获取来自回调数据的 IO 优先级信息。 |
| **FltGetIoPriorityHintFromCallbackData** | 获取来自回调数据的 IO 优先级信息。 |
| **FltGetIoPriorityHintFromFileObject** | 获取文件对象中的 IO 优先级信息。 |
| **FltGetIoPriorityHintFromThread** | 从线程获取 IO 优先级信息。 |
| **FltGetIrpName** | 以可打印字符串的形式返回主要函数代码的名称。 |
| **FltGetLowerInstance** | 对于下一个较低的微筛选器驱动程序实例，返回一个不透明的实例指针（如果有），它附加在同一卷上的给定微筛选器驱动程序实例下。 |
| **FltGetNewSystemBufferAddress** | 检索文件系统已分配的*AssociatedIrp 缓冲区。* 微筛选器驱动程序的回拨例程调用此函数。 |
| **FltGetNextExtraCreateParameter** | 返回一个指针，该指针指向给定 ECP 列表中的下一个（或第一个）额外的 create 参数上下文结构（ECP）。 |
| **FltGetRequestorProcess** | 返回请求给定 i/o 操作的线程的进程指针。 |
| **FltGetRequestorProcessId** | 返回与请求给定 i/o 操作的线程关联的进程的唯一32位进程 ID。 |
| **FltGetRequestorProcessIdEx** | 返回与请求给定 i/o 操作的线程关联的进程的内核模式句柄。 |
| **FltGetRequestorSessionId** | 返回最初请求指定 i/o 操作的进程的会话 ID。 |
| **FltGetRoutineAddress** | 返回指向由**FltMgrRoutineName**参数指定的例程的指针。 |
| **FltGetSectionContext** | 检索由指定的微筛选器驱动程序实例为文件流创建的节上下文。 |
| **FltGetStreamContext** | 检索由给定的微筛选器驱动程序实例为文件流设置的上下文。 |
| **FltGetStreamHandleContext** | 检索由给定微筛选器驱动程序实例为流句柄设置的上下文。 |
| **FltGetSwappedBufferMdlAddress** | 返回由微筛选器驱动程序交换的缓冲区的内存描述符列表（MDL）地址。 |
| **FltGetTopInstance** | 为给定卷的实例堆栈顶部附加的微筛选器驱动程序实例返回一个不透明的实例指针。 |
| **FltGetTransactionContext** | 检索由给定微筛选器驱动程序为事务设置的上下文。 |
| **FltGetTunneledName** | 为某个文件检索隧道名称，前提是先前调用了**FltGetFileNameInformation**、 **FltGetFileNameInformationUnsafe**或**FltGetDestinationFileNameInformation**文件的规范化名称。 |
| **FltGetUpperInstance** | 为下一个较高的微筛选器驱动程序实例返回一个不透明的实例指针（如果有），它附加在同一卷上的给定微筛选器驱动程序实例之上。 |
| **FltGetVolumeContext** | 检索由给定微筛选器驱动程序为卷设置的上下文。 |
| **FltGetVolumeFromDeviceObject** | 返回卷设备对象（VDO）表示的卷的不透明指针。 |
| **FltGetVolumeFromFileObject** | 返回给定文件流所在卷的不透明指针。 |
| **FltGetVolumeFromInstance** | 返回给定的微筛选器驱动程序实例所附加到的卷的不透明指针。|
| **FltGetVolumeFromName** | 返回其名称与*VolumeName*参数的值匹配的卷的不透明指针。 |
| **FltGetVolumeGuidName** | 返回给定卷的卷名，以全局唯一标识符（GUID）格式表示。 |
| **FltGetVolumeInformation** | 提供有关给定卷的信息。 |
| **FltGetVolumeInstanceFromName** | 返回给定卷上给定微筛选器驱动程序实例的不透明实例指针。 |
| **FltGetVolumeName** | 获取给定卷的卷名。 |
| **FltGetVolumeProperties** | 返回给定卷的卷属性信息。 |
| **FltInitExtraCreateParameterLookasideList** | 初始化分页或非分页池后备链表列表，该列表用于分配固定大小的一个或多个额外创建参数上下文结构（ECPs）。 |
| **FltInitializeFileLock** | 初始化调用方已从分页池分配的不透明 FILE_LOCK 结构。 |
| **FltInitializeOplock** | 初始化机会锁（oplock）指针。 |
| **FltInitializePushLock** | 初始化推送锁变量。 |
| **FltInsertExtraCreateParameter** | 在 ECP 列表中插入额外的 create parameter （ECP）上下文结构。 |
| **FltIs32bitProcess** |检查当前 i/o 操作的发起方是否为32位用户模式应用程序。 |
| **FltIsCallbackDataDirty** | 测试回调数据结构中的 FLTFL_CALLBACK_DATA_DIRTY 标志。 |
| **FltIsDirectory** | 确定给定的文件对象是否表示目录。 |
| **FltIsEcpAcknowledged** | 确定是否已将给定的额外 create 参数上下文（ECP）标记为已确认。 |
| **FltIsEcpFromUserMode** | 确定是否从用户模式产生额外的 create 参数上下文（ECP）。 |
| **FltIsFltMgrVolumeDeviceObject** | 确定给定设备对象是否属于筛选器管理器以及设备对象是否为卷设备对象。 |
| **FltIsIoCanceled** | 检查是否已取消基于 IRP 的操作。 |
| **FltIsIoRedirectionAllowed** | 确定是否可以将 i/o 从指定的源筛选器实例重定向到另一个指定的筛选器实例。 |
| **FltIsIoRedirectionAllowedForOperation** | 确定是否可以将 i/o 从与指定 FLT_CALLBACK_DATA 结构关联的筛选器实例重定向到指定的筛选器实例。 |
| **FltIsOperationSynchronous** | 确定给定的回调数据结构（FLT_CALLBACK_DATA）是否表示同步或异步 i/o 操作。 |
| **FltIsVolumeSnapshot** | 确定卷或微筛选器驱动程序实例是否连接到快照卷。 |
| **FltIsVolumeWritable** | 确定与卷或微筛选器驱动程序实例相对应的磁盘设备是否可写。 |
| **FltLoadFilter** | 将微筛选器驱动程序动态加载到当前正在运行的系统。 |
| **FltLockUserBuffer** | 锁定给定 i/o 操作的用户缓冲区。 |
| **FltNotifyFilterChangeDirectory** | 创建 IRP_MN_NOTIFY_CHANGE_DIRECTORY 操作的通知结构，并将其添加到指定的通知列表。 |
| **FltObjectDereference** | 从不透明的筛选器、实例或卷指针中删除断开引用。 |
| **FltObjectReference** | 向不透明的筛选器、实例或卷指针添加断开引用。 |
| **FltOpenVolume** | 返回给定的微筛选器驱动程序实例所附加到的文件系统卷的句柄和文件对象指针。 |
| **FltOplockBreakH** | 中断 CACHE_HANDLE_LEVEL 机会锁（oplock）。 |
| **FltOplockBreakToNone** | 立即中断所有机会锁（oplock），而不考虑任何 oplock 项。 |
| **FltOplockBreakToNoneEx** | 立即中断所有机会锁（oplock），而不考虑任何 oplock 项。 |
| **FltOplockFsctrl** | 代表微筛选器驱动程序执行各种机会锁（oplock）操作。 |
| **FltOplockFsctrlEx** | 代表微筛选器驱动程序执行各种机会锁（oplock）操作。 |
| **FltOplockIsFastIoPossible** | 检查文件的机会锁（oplock）状态，以确定是否可以对文件执行快速 i/o。 |
| **FltOplockIsSharedRequest** | 确定对机会锁（oplock）的请求是否需要共享 oplock。 |
| **FltOplockKeysEqual** | 比较存储在两个文件对象的文件对象扩展中的机会锁（oplock）键。 |
| **FltParseFileName** | 分析文件名称字符串的扩展、流和最终组件。 |
| **FltParseFileNameInformation** | 分析 FLT_FILE_NAME_INFORMATION 结构的内容。 |
| **FltPerformAsynchronousIo** | 启动异步 i/o 操作。 |
| **FltPerformSynchronousIo** | 在调用**FltAllocateCallbackData**以为操作分配回调数据结构后，启动同步 i/o 操作。 |
| **FltPrepareComplete** | 确认 TRANSACTION_NOTIFY_PREPARE 通知。 |
| **FltPrepareToReuseEcp** | 重置额外的 create parameter （ECP）上下文结构，使其做好重复使用的准备。 |
| **FltPrePrepareComplete** | 确认 TRANSACTION_NOTIFY_PREPREPARE 通知。 |
| **FltProcessFileLock** | 处理和完成文件锁定操作。 |
| **FltPropagateActivityIdToThread** | 将微筛选器的回调数据中的 IRP 的活动 ID 与当前线程关联。 |
| **FltPurgeFileNameInformationCache** | 从筛选器管理器的名称缓存中清除从给定的微筛选器驱动程序实例提供的名称生成的所有文件名信息结构。 |
| **FltQueryDirectoryFile** | 返回给定文件对象所指定目录中的文件的各种信息。 |
| **FltQueryEaFile** | 返回文件的扩展属性（EA）值的相关信息。 |
| **FltQueryInformationFile** | 检索给定文件的信息。 |
| **FltQueryQuotaInformationFile** | 检索与文件对象关联的配额条目。 |
| **FltQuerySecurityObject** | 检索对象的安全描述符的副本。 |
| **FltQueryVolumeInformation** | 检索有关给定实例所附加到的卷的信息。 |
| **FltQueryVolumeInformationFile** | 检索给定文件、目录、存储设备或卷的卷信息。 |
| **FltQueueDeferredIoWorkItem** | 将基于 IRP 的 i/o 操作发送到工作队列。 |
| **FltQueueGenericWorkItem** | 将不与特定 i/o 操作关联的工作项发布到工作队列。 |
| **FltReadFile** | 从打开的文件、流或设备读取数据。 |
| **FltReadFileEx** | 从打开的文件、流或设备读取数据。 此函数扩展**FltReadFile** ，以允许将 MDL 的可选用法用于读取数据而不是映射缓冲区地址。 |
| **FltReferenceContext** | 递增上下文结构上的引用计数。 |
| **FltReferenceFileNameInformation** | 递增文件名信息结构上的引用计数。 |
| **FltRegisterFilter** | 注册微筛选器驱动程序。 |
| **FltRegisterForDataScan** | 为附加到微筛选器实例的卷启用数据扫描。 |
| **FltReissueSynchronousIo** | 启动新的同步 i/o 操作，该操作使用之前同步的 i/o 操作中的参数。 |
| **FltReleaseContext** | 递减上下文中的引用计数。 |
| **FltReleaseContexts** | 释放给定 FLT_RELATED_CONTEXTS 结构中的每个上下文。 |
| **FltReleaseContextsEx** | 释放给定 FLT_RELATED_CONTEXTS_EX 结构中的每个上下文。 |
| **FltReleaseFileNameInformation** | 释放文件名信息结构。 |
| **FltReleasePushLock** | 释放由当前线程拥有的指定推送锁。 |
| **FltReleaseResource** | 释放当前线程拥有的指定资源。 |
| **FltRemoveExtraCreateParameter** | 在 ECP 列表中搜索 ECP 上下文结构，如果找到，则将其从 ECP 列表中分离。 |
| **FltRequestOperationStatusCallback** | 返回给定 i/o 操作的状态信息。 |
| **FltRetainSwappedBufferMdlAddress** | 防止筛选器管理器释放由微筛选器驱动程序交换的缓冲区的内存描述符列表（MDL）。 |
| **FltRetrieveIoPriorityInfo** | 从线程中检索优先级信息。 |
| **FltReuseCallbackData** | 重新初始化回调数据结构，以便可以重复使用它。 |
| **FltRollbackComplete** | 确认 TRANSACTION_NOTIFY_ROLLBACK 通知。 |
| **FltRollbackEnlistment** | 代表微筛选器驱动程序回滚或中止事务。 |
| **FltSendMessage** | 代表微筛选器驱动程序或微筛选器驱动程序实例将消息发送到等待用户模式应用程序。 |
| **FltSetActivityIdCallbackData** | 设置微筛选器的回调数据中的 IRP 的活动 ID。 |
| **FltSetCallbackDataDirty** | 微筛选器驱动程序的 preoperation 或 postoperation 回调例程会调用**FltSetCallbackDataDirty** ，以指示它已修改回调数据结构的内容。 |
| **FltSetCancelCompletion** | 指定在取消给定 i/o 操作时要调用的取消例程。 |
| **FltSetEaFile** | 为文件设置扩展属性（EA）值。 |
| **FltSetEcpListIntoCallbackData** | 将额外的 create parameter context structure list 列表附加到 create operation 回拨-data 对象。 |
| **FltSetFileContext** | 设置文件的上下文。 |
| **FltSetInformationFile** | 设置给定文件的信息。 |
| **FltSetInstanceContext** | 设置微筛选器驱动程序实例的上下文。 |
| **FltSetIoPriorityHintIntoCallbackData** | 设置回调数据中的 i/o 优先级信息。 |
| **FltSetIoPriorityHintIntoFileObject** | 在文件对象中设置 i/o 优先级信息。 |
| **FltSetIoPriorityHintIntoThread** | 设置线程中的 IO 优先级信息。 |
| **FltSetQuotaInformationFile** | 修改文件对象的配额条目。 |
| **FltSetSecurityObject** | 设置对象的安全状态。 |
| **FltSetStreamContext** | 设置文件流的上下文。 |
| **FltSetStreamHandleContext** | 设置流句柄的上下文。 |
| **FltSetTransactionContext** | 设置事务的上下文。 |
| **FltSetVolumeContext** | 设置卷的上下文。 |
| **FltSetVolumeInformation** | 更改有关给定实例附加到的卷的各种信息。 |
| **FltStartFiltering** | 开始筛选已注册的微筛选器驱动程序。 |
| **FltSupportsFileContexts** | 确定文件系统是否支持给定文件的文件上下文。 |
| **FltSupportsFileContextsEx** | 确定文件系统或筛选器管理器是否支持给定文件的文件上下文。 |
| **FltSupportsStreamContexts** | 确定给定文件对象是否支持流上下文。 |
| **FltSupportsStreamHandleContexts** | 确定给定文件对象是否支持流处理上下文。 |
| **FltTagFile** | 对文件或目录设置重分析标记。 |
| **FltUninitializeFileLock** | 取消 FILE_LOCK 结构。 |
| **FltUninitializeOplock** | 取消机会锁（oplock）指针。 |
| **FltUnloadFilter** | 通过调用**FltLoadFilter**加载了支持微筛选器驱动程序的微筛选器驱动程序可以通过调用**FltUnloadFilter**来卸载微筛选器驱动程序。 |
| **FltUnregisterFilter** | 已注册的微筛选器驱动程序调用**FltUnregisterFilter**来注销自身，使筛选器管理器不再调用它来处理 i/o 操作。 |
| **FltUntagFile** | 删除文件或目录中的重新分析点。 |
| **FltWriteFile** | 向打开的文件、流或设备写入数据。 |
| **FltWriteFileEx** | 向打开的文件、流或设备写入数据。 此函数扩展**FltWriteFile** ，以允许将 MDL 的可选用法用于写入数据，而不是映射缓冲区地址。 |
| **IS_ALIGNED** | 确定第一个参数是否在指定的2次边界上对齐。
