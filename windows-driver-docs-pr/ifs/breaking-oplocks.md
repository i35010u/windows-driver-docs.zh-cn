---
title: 破坏 Oplock
description: 破坏 Oplock
ms.assetid: 1f3c4a99-5ad2-4597-a1c9-a21f80c40291
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be10a1b3a47d9296b7e8937af665654246f778e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841483"
---
# <a name="breaking-oplocks"></a>破坏 Oplock


## <span id="ddk_network_redirector_design_and_performance_if"></span><span id="DDK_NETWORK_REDIRECTOR_DESIGN_AND_PERFORMANCE_IF"></span>


授权 oplock 后，该 oplock 的所有者有权访问该流（基于请求的操作类型）。 如果收到的操作与当前 oplock 不兼容，则 oplock 会断开。

当向 oplock 授予时，请求的 IRP 将挂起。 Oplock 中断后，挂起的 oplock 请求 IRP 将以状态\_成功完成。 对于级别1、批处理和筛选器 oplock，IRP 的**IoStatus**成员设置为指示 oplock 要中断的级别。 这些级别包括：

-   文件\_OPLOCK\_中断\_到\_无-操作中断，并且流上没有当前 oplock。 Oplock 被称为 "无"。

-   文件\_OPLOCK\_中断\_到\_级别\_2-当前 oplock （级别1或批）已转换为2级 oplock。 请注意，Filter oplock 从不分解为级别2，它们始终中断到 "无"。

对于读取句柄，读写和读/写-句柄 oplock，oplock 要中断的级别被描述为零个或多个标志 OPLOCK\_级别的组合\_缓存\_读取、OPLOCK\_级别\_缓存\_句柄，或 OPLOCK\_级别\_缓存\_在请求的**NewOplockLevel**成员中\_写入作为 DeviceIoControl 的*lpOutBuffer*参数传递\_缓冲结构[](https://go.microsoft.com/fwlink/p/?linkid=124239).\_ 同样， [**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)和[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)可用于请求内核模式下的 Windows 7 oplock。 有关详细信息，请参阅[**FSCTL\_REQUEST\_OPLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-request-oplock)。

如果在某些情况下中断级别1、批处理、筛选器、读写、读写句柄或，则在某些情况下（请参阅注意），读取句柄操作将由 oplock 包完成，而导致 oplock 中断的操作本身就是挂起（请注意，如果在同步句柄上发出操作，或者它是 IRP\_MJ\_CREATE （始终是同步的），则 i/o 管理器会导致阻止操作，而不是返回状态\_挂起），等待操作人员的所有者确认操作者通知 oplock 包已完成其处理，且挂起的操作可以安全地继续操作。 此延迟的目的是允许操作者的所有者将流置于一致状态，然后再继续执行当前操作。 系统永远不会等待接收确认，因为没有超时。 因此，对 oplock 的所有者，要及时确认中断。 挂起操作的 IRP 设置为可取消状态。 如果执行等待的应用程序或驱动程序终止，oploack 包会立即完成 IRP，状态\_已取消。

IRP\_MJ\_CREATE IRP 可以指定文件\_完成\_如果\_OPLOCKED CREATE 选项，以避免在 oplock 中断确认过程中被阻止。 此选项告知 oplock 包不阻止 create IRP，直到收到 oplock 中断确认。 但允许创建操作。 如果成功的 create 导致 oplock 中断，则返回代码为状态\_OPLOCK\_中断\_\_进度，而不是成功的\_状态。 如果\_OPLOCKED 标志通常用于避免死锁，则文件\_完成\_。 例如，如果客户端拥有对流上的 oplock，并且同一客户端随后打开相同的流，则客户端会阻止其自身确认 oplock 中断。 在这种情况下，如果\_OPLOCKED 标志避免死锁，则使用文件\_完成\_。

由于 NTFS 文件系统会在检查共享冲突之前为批处理和筛选器 oplock 启动 oplock 中断，因此创建该指定的文件可能\_完成\_如果\_OPLOCKED 失败，状态\_共享\_冲突，但仍会导致批处理或筛选器 oplock 中断。 在这种情况下， [**IO\_状态\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构的信息成员设置为 FILE\_OPBATCH\_中断\_以允许调用方检测到这种情况。

对于读取句柄和读写句柄 oplock，在 NTFS 检查并检测到共享冲突后，将启动 oplock 中断。 这为这些 oplock 的持有者提供关闭句柄并使其停止的机会，从而允许不向用户返回共享冲突。 它还可以避免在 oplock 缓存的句柄不会与新的 create 冲突的情况下无条件中断 oplock。

当级别为2时，请在某些情况下读取，并在某些情况下（请参阅注意），读取-处理 oplock 中断，系统不等待确认。 这是因为在允许其他客户端访问该文件之前，需要将该流上的缓存状态还原到该文件。

某些文件系统操作会检查当前 oplock 状态，以确定 oplock 是否需要中断。 以下各部分列出了每个操作，并说明了 oplock 中断的触发因素，确定 oplock 中断的级别以及是否需要确认是否需要中断：

- [IRP_MJ_CREATE](irp-mj-create2.md)

- [IRP_MJ_READ](irp-mj-read2.md)

- [IRP_MJ_WRITE](irp-mj-write2.md)

- [IRP_MJ_CLEANUP](irp-mj-cleanup2.md)

- [IRP_MJ_LOCK_CONTROL](irp-mj-lock-control2.md)

- [IRP_MJ_SET_INFORMATION](irp-mj-set-information2.md)

- [IRP_MJ_FILE_SYSTEM_CONTROL](irp-mj-file-system-control2.md)

如果请求\_OPLOCK\_OUTPUT\_标志\_ACK\_在请求的**Flags**成员\_输出\_缓冲区中设置，则 Windows 7 oplock 的中断需要确认作为[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)（*LpOutBuffer*）、 [**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)（*OutBuffer*）或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)（*OutBuffer*）的 output 参数传递的结构。\_ 有关详细信息，请参阅[**FSCTL\_REQUEST\_OPLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-request-oplock)。

**请注意**  以上列出的每个操作的主题描述了当读取句柄 oplock 中断导致断开 oplock 的操作挂起时的详细信息。 例如， [IRP\_MJ\_CREATE](irp-mj-create2.md)主题包含关联的读取句柄详细信息。

 

 

 




