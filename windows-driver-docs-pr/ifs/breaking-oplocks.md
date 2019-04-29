---
title: 破坏 Oplock
description: 破坏 Oplock
ms.assetid: 1f3c4a99-5ad2-4597-a1c9-a21f80c40291
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79818cd997acc69e0b5ab5cc229faa9b59529ee9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391501"
---
# <a name="breaking-oplocks"></a>破坏 Oplock


## <span id="ddk_network_redirector_design_and_performance_if"></span><span id="DDK_NETWORK_REDIRECTOR_DESIGN_AND_PERFORMANCE_IF"></span>


授予 oplock 后，该机会锁的所有者有权访问 （基于请求的机会锁的类型） 的流。 如果接收到的操作不符合当前 oplock，oplock 已断开。

授予 oplock 时，发出请求的 IRP 是挂起。 破坏 oplock 时，将挂起 oplock 请求 IRP 完成，状态\_成功。 对于级别 1、 批处理和筛选器 oplocks **IoStatus.Information** IRP 的成员设置为指示向其破坏 oplock 的级别。 这些级别包括：

-   文件\_OPLOCK\_破坏\_TO\_NONE-oplock 已断开，并且在流上没有任何当前 oplock。 机会锁被认为已"为无拆分"。

-   文件\_OPLOCK\_破坏\_TO\_级别\_2-当前 oplock （级别 1 或批） 已转换为级别 2 oplock。 请注意，筛选器 oplocks 永远不会中断到级别 2，它们始终中断为无。

读取句柄，读写和读写句柄 oplock，向其破坏 oplock 的级别描述为组合的零个或多个标志 OPLOCK\_级别\_缓存\_读取、 OPLOCK\_级别\_缓存\_句柄或 OPLOCK\_级别\_缓存\_中编写**NewOplockLevel**成员请求\_OPLOCK\_输出\_作为传递的缓冲区结构*lpOutBuffer*参数[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)。 以类似方式[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)并[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)可以用于从内核模式下请求 Windows 7 oplock。 有关详细信息，请参阅[ **FSCTL\_请求\_OPLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff545530)。

将换行一级，批处理，筛选，读写、 读-写的句柄，或者在某些情况下 （请参阅备注）、 读取句柄 oplock、 挂起操作锁定请求由 oplock 包完成 IRP 和导致破坏 oplock 的操作是本身挂起 (请注意，如果该操作发出同步句柄，或者它是 IRP\_MJ\_创建，始终是同步的 I/O 管理器会导致操作阻止，而不返回状态\_PENDING)，等待机会锁的所有者，告知他们已完成其处理，并且是安全的挂起操作才能继续 oplock 包确认。 这种延迟的目的是允许放在流回到一致状态之前继续执行当前操作的机会锁所有者。 系统永远等待以接收确认，因为没有任何超时。 因此，是的机会锁的所有者负责及时地确认中断。 挂起的操作的 IRP 是设置为可取消状态。 如果应用程序或驱动程序执行等待终止，oploack 包立即完成，状态 IRP\_已取消。

IRP\_MJ\_IRP 创建可能指定的文件\_完成\_如果\_OPLOCKED 创建选项，以避免被阻止 oplock 中断确认的一部分。 此选项会告知 oplock 包不进行阻止创建 IRP，直到收到 oplock 中断确认。 相反，创建允许以继续。 如果成功创建导致破坏 oplock，返回代码是状态\_OPLOCK\_BREAK\_IN\_进度，而不是状态\_成功。 该文件\_完成\_如果\_OPLOCKED 标志通常用于避免死锁。 例如，如果客户端拥有流 oplock，同一个客户端随后将打开同一个流，客户端将阻止等待本身以确认破坏 oplock。 在此方案中，使用的文件\_完成\_如果\_OPLOCKED 标志可避免死锁。

由于 NTFS 文件系统共享冲突检查之前启动的批处理和筛选器 oplocks oplock 分隔线，很可能指定了文件创建\_完成\_如果\_OPLOCKED 状态而失败\_共享\_冲突但仍会导致批处理或筛选器的 oplock 中断。 在此情况下，信息隶属[ **IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)结构设置为文件\_OPBATCH\_中断\_正在以允许调用方来检测这种情况。

对于读取句柄和读写句柄 oplock，需要破坏 oplock 启动后检查 NTFS，并检测到发生共享冲突。 这样，持有人的这些 oplock 机会关闭其句柄并获取开，从而允许不向用户返回共享冲突的可能性。 它还避免了无条件地在其中 oplock 缓存的句柄不冲突的新创建的情况下破坏 oplock。

级别 2 读取时，并在某些情况下，（请参阅备注），读取句柄 oplock 中断，系统不会等待确认。 这是因为需要允许访问它的其他客户端之前还原到的文件的流上应为没有缓存的状态。

有检查当前的 oplock 状态，以确定是否需要被破坏 oplock 的某些文件系统操作。 以下各节列出的每个操作，并说明是什么触发了破坏 oplock，由什么决定 oplock 中断的级别以及是否需要中断的确认：

- [IRP_MJ_CREATE](irp-mj-create2.md)

- [IRP_MJ_READ](irp-mj-read2.md)

- [IRP_MJ_WRITE](irp-mj-write2.md)

- [IRP_MJ_CLEANUP](irp-mj-cleanup2.md)

- [IRP_MJ_LOCK_CONTROL](irp-mj-lock-control2.md)

- [IRP_MJ_SET_INFORMATION](irp-mj-set-information2.md)

- [IRP_MJ_FILE_SYSTEM_CONTROL](irp-mj-file-system-control2.md)

Windows 7 oplock 中断如果，则需要确认请求\_OPLOCK\_输出\_标志\_ACK\_中设置了必需标志**标志**的成员请求\_OPLOCK\_输出\_作为输出参数传递的缓冲区结构[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)(*lpOutBuffer*)， [ **FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)(*OutBuffer*) 或[ **ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)(*OutBuffer*)。 有关详细信息，请参阅[ **FSCTL\_请求\_OPLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff545530)。

**请注意**  上面列出的每个操作的主题介绍的读句柄 oplock 中断导致的详细信息挂起操作破坏 oplock 的操作。 例如， [IRP\_MJ\_创建](irp-mj-create2.md)主题包含关联的读句柄详细信息。

 

 

 




