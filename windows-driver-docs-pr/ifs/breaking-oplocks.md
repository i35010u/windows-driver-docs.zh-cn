---
title: 破坏 Oplock
description: 破坏 Oplock
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc53fd163f8f4d9671e0bf1150de157cf366609f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831841"
---
# <a name="breaking-oplocks"></a>破坏 Oplock


## <span id="ddk_network_redirector_design_and_performance_if"></span><span id="DDK_NETWORK_REDIRECTOR_DESIGN_AND_PERFORMANCE_IF"></span>


授权 oplock 后，该 oplock 的所有者就可以根据请求的操作类型 () 来访问该流。 如果收到的操作与当前 oplock 不兼容，则 oplock 会断开。

当向 oplock 授予时，请求的 IRP 将挂起。 Oplock 中断后，挂起的 oplock 请求 IRP 已完成，状态为 " \_ 成功"。 对于级别1、批处理和筛选器 oplock，IRP 的 **IoStatus** 成员设置为指示 oplock 要中断的级别。 这些级别包括：

-   文件 \_ oplock \_ 断开 \_ 为 \_ "无"-操作中断，并且流上没有当前 oplock。 Oplock 被称为 "无"。

-   文件 \_ OPLOCK \_ 分解 \_ 为 \_ 级别 \_ 2-当前 Oplock (级别1或批处理) 转换为第2级 oplock。 请注意，Filter oplock 从不分解为级别2，它们始终中断到 "无"。

对于读取句柄、读写和读写句柄 oplock，oplock 要中断的级别被描述为作为 \_ \_ \_ \_ \_ \_ \_ \_ \_ **NewOplockLevel** \_ \_ \_ [DeviceIoControl](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)的 *lpOutBuffer* 参数传递的请求 oplock 输出缓冲区结构的 NewOplockLevel 成员中的零个或多个标志 oplock 级别缓存读取、oplock 级别缓存句柄或 oplock 级别缓存写入的组合。 同样， [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 和 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 可用于请求内核模式下的 Windows 7 oplock。 有关详细信息，请参阅 [**FSCTL \_ 请求 \_ OPLOCK**](./fsctl-request-oplock.md)。

在中断级别1、批处理、筛选器、读写和读写句柄，或在某些情况下 (参阅注意) ，Read-Handle oplock，挂起的 oplock 请求 IRP 由 oplock 包完成，导致 oplock 中断的操作本身处于挂起 (注意，如果在同步句柄上发出操作，它也是一个 IRP \_ MJ \_ CREATE，它始终是同步的，i/o 管理器会导致操作被阻止，而不是返回状态 " \_ 挂起) "，等待 oplock 的所有者确认其已完成其处理，并且挂起的操作可以安全地继续。 此延迟的目的是允许操作者的所有者将流置于一致状态，然后再继续执行当前操作。 系统永远不会等待接收确认，因为没有超时。 因此，对 oplock 的所有者，要及时确认中断。 挂起操作的 IRP 设置为可取消状态。 如果执行等待的应用程序或驱动程序终止，oploack 包会立即完成 IRP，状态为 "已 \_ 取消"。

\_ \_ \_ \_ 如果 \_ OPLOCKED 创建选项避免在 oplock 中断确认过程中被阻止，irp MJ CREATE irp 可能会指定文件完成。 此选项告知 oplock 包不阻止 create IRP，直到收到 oplock 中断确认。 但允许创建操作。 如果成功的 create 导致 oplock 中断，返回代码为状态 \_ oplock \_ 中断 \_ \_ ，而不是 \_ 成功状态。 \_ \_ 如果 \_ OPLOCKED 标志通常用于避免死锁，则文件完成。 例如，如果客户端拥有对流上的 oplock，并且同一客户端随后打开相同的流，则客户端会阻止其自身确认 oplock 中断。 在这种情况下， \_ \_ 如果 \_ OPLOCKED 标志避免死锁，则使用文件 COMPLETE。

由于 NTFS 文件系统会在检查共享冲突之前为批处理和筛选器 oplock 启动 oplock 中断，因此，如果 OPLOCKED 失败并发生状态共享冲突，则创建指定的文件可能已 \_ 完成， \_ \_ \_ \_ 但仍会导致批处理或筛选器 oplock 中断。 在这种情况下， [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构的信息成员设置为 FILE \_ OPBATCH \_ BREAK， \_ 以允许调用方检测到这种情况。

对于 Read-Handle 和读写句柄 oplock，在 NTFS 检查并检测到共享冲突后，将启动 oplock 中断。 这为这些 oplock 的持有者提供关闭句柄并使其停止的机会，从而允许不向用户返回共享冲突。 它还可以避免在 oplock 缓存的句柄不会与新的 create 冲突的情况下无条件中断 oplock。

当级别为2时，请在某些情况下读取，并在某些情况下 (查看) Read-Handle oplock 中断，系统不等待确认。 这是因为在允许其他客户端访问该文件之前，需要将该流上的缓存状态还原到该文件。

某些文件系统操作会检查当前 oplock 状态，以确定 oplock 是否需要中断。 以下各部分列出了每个操作，并说明了 oplock 中断的触发因素，确定 oplock 中断的级别以及是否需要确认是否需要中断：

- [IRP_MJ_CREATE](irp-mj-create2.md)

- [IRP_MJ_READ](irp-mj-read2.md)

- [IRP_MJ_WRITE](irp-mj-write2.md)

- [IRP_MJ_CLEANUP](irp-mj-cleanup2.md)

- [IRP_MJ_LOCK_CONTROL](irp-mj-lock-control2.md)

- [IRP_MJ_SET_INFORMATION](irp-mj-set-information2.md)

- [IRP_MJ_FILE_SYSTEM_CONTROL](irp-mj-file-system-control2.md)

Windows 7 oplock 的中断要求确认：请求 oplock 输出 \_ \_ \_ 标志 \_ 确认请求 \_ 标记是在 **Flags** \_ \_ \_ 作为 [DeviceIoControl](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) (*lpOutBuffer*) 、 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) (*OutBuffer*) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) (*OutBuffer*) 的 output 参数传递的请求 oplock 输出缓冲区结构中设置的。 有关详细信息，请参阅 [**FSCTL \_ 请求 \_ OPLOCK**](./fsctl-request-oplock.md)。

**注意**  上面列出的每个操作主题描述了当 Read-Handle oplock 的中断导致断开 oplock 的操作挂起时的详细信息。 例如， [IRP \_ MJ \_ CREATE](irp-mj-create2.md) 主题包含关联的 Read-Handle 详细信息。

 

