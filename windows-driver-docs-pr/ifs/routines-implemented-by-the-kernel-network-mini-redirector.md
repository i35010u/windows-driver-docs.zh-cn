---
title: 由内核网络微型重定向程序实现的例程
description: 由内核网络微型重定向程序实现的例程
ms.assetid: bd1a8989-100d-4b7b-9a61-521af6433b00
keywords:
- 小型重定向程序 WDK，实现的例程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 394462afd702b29624cda3733bb8058fa52967e3
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063008"
---
# <a name="routines-implemented-by-the-kernel-network-mini-redirector"></a>由内核网络微型重定向程序实现的例程


以下例程可由网络微型重定向程序实现：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程所返回的值</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkfcb_calldown" data-raw-source="[&lt;strong&gt;MRxAreFilesAliased&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkfcb_calldown)"><strong>MRxAreFilesAliased</strong></a></td>
<td align="left"><p>如果两个文件控制块 (FCB) 结构表示同一个文件，则 RDBSS 将调用此例程来查询网络微型重定向程序。 RDBSS 在处理两个看起来相同但名称不同 (MS-DOS 短名称和长名称的文件时，将调用此例程，例如) 。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85)" data-raw-source="[&lt;strong&gt;MRxCleanupFobx&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff549841(v=vs.85))"><strong>MRxCleanupFobx</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序关闭文件系统对象扩展结构。 RDBSS 发出此调用以响应接收文件对象上的 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-cleanup" data-raw-source="[&lt;strong&gt;IRP_MJ_CLEANUP&lt;/strong&gt;](./irp-mj-cleanup.md)"><strong>IRP_MJ_CLEANUP</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown" data-raw-source="[&lt;strong&gt;MRxCloseSrvOpen&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown)"><strong>MRxCloseSrvOpen</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向器关闭 SRV_OPEN 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcollapseopen" data-raw-source="[&lt;strong&gt;MRxCollapseOpen&lt;/strong&gt;](./mrxcollapseopen.md)"><strong>MRxCollapseOpen</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络微重定向程序将打开的文件系统请求折叠到现有 SRV_OPEN。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_change_buffering_state_calldown" data-raw-source="[&lt;strong&gt;MRxCompleteBufferingStateChangeRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_change_buffering_state_calldown)"><strong>MRxCompleteBufferingStateChangeRequest</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，通知网络小型重定向器已完成缓冲状态更改请求。 例如，当文件不再使用时，SMB 重定向程序使用此例程来发送 oplock 中断响应或关闭 oplock 中断的句柄。 需要在服务器上刷新的字节范围锁会传递到 RX_CONTEXT 结构的 <strong>LockList</strong> 成员中的网络微重定向程序。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_compute_new_buffering_state" data-raw-source="[&lt;strong&gt;MRxComputeNewBufferingState&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_compute_new_buffering_state)"><strong>MRxComputeNewBufferingState</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络最小化重定向器计算新的缓冲状态更改。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcreate" data-raw-source="[&lt;strong&gt;MRxCreate&lt;/strong&gt;](./mrxcreate.md)"><strong>MRxCreate</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序创建文件系统对象。 RDBSS 发出此调用以响应接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create" data-raw-source="[&lt;strong&gt;IRP_MJ_CREATE&lt;/strong&gt;](./irp-mj-create.md)"><strong>IRP_MJ_CREATE</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_srvcall" data-raw-source="[&lt;strong&gt;MRxCreateSrvCall&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_srvcall)"><strong>MRxCreateSrvCall</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序创建 SRV_CALL 结构并建立与服务器的连接。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_v_net_root" data-raw-source="[&lt;strong&gt;MRxCreateVNetRoot&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_v_net_root)"><strong>MRxCreateVNetRoot</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序创建 V_NET_ROOT 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fcb" data-raw-source="[&lt;strong&gt;MRxDeallocateForFcb&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fcb)"><strong>MRxDeallocateForFcb</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序释放 FCB。 此调用用于响应关闭文件系统对象的请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fobx" data-raw-source="[&lt;strong&gt;MRxDeallocateForFobx&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fobx)"><strong>MRxDeallocateForFobx</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序释放 FOBX 结构。 此调用用于响应关闭文件系统对象的请求。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxdevfcbxxxcontrolfile" data-raw-source="[&lt;strong&gt;MRxDevFcbXXXControlFile&lt;/strong&gt;](./mrxdevfcbxxxcontrolfile.md)"><strong>MRxDevFcbXXXControlFile</strong></a></td>
<td align="left"><p>RDBSS 调用此例程将设备 FCB 控制请求传递到网络小型重定向程序。 RDBSS 发出此调用以响应在设备 FCB 上接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](./irp-mj-device-control.md)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control" data-raw-source="[&lt;strong&gt;IRP_MJ_FILE_SYSTEM_CONTROL&lt;/strong&gt;](./irp-mj-file-system-control.md)"><strong>IRP_MJ_FILE_SYSTEM_CONTROL</strong></a>或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-internal-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](./irp-mj-internal-device-control.md)"><strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extendfile_calldown" data-raw-source="[&lt;strong&gt;MRxExtendForCache&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extendfile_calldown)"><strong>MRxExtendForCache</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络小型重定向程序在缓存管理器缓存文件时扩展文件。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxextendfornoncache" data-raw-source="[&lt;strong&gt;MRxExtendForNonCache&lt;/strong&gt;](./mrxextendfornoncache.md)"><strong>MRxExtendForNonCache</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络小型重定向程序在缓存管理器未缓存文件时扩展文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extract_netroot_name" data-raw-source="[&lt;strong&gt;MRxExtractNetRootName&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extract_netroot_name)"><strong>MRxExtractNetRootName</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络小型重定向程序从给定的路径名中提取 NET_ROOT 的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_net_root_calldown" data-raw-source="[&lt;strong&gt;MRxFinalizeNetRoot&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_net_root_calldown)"><strong>MRxFinalizeNetRoot</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络最小化重定向器完成一个 NET_ROOT 对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_srvcall_calldown" data-raw-source="[&lt;strong&gt;MRxFinalizeSrvCall&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_srvcall_calldown)"><strong>MRxFinalizeSrvCall</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络最小化重定向器完成用于与服务器建立连接的 SRV_CALL 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_v_net_root_calldown" data-raw-source="[&lt;strong&gt;MRxFinalizeVNetRoot&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_finalize_v_net_root_calldown)"><strong>MRxFinalizeVNetRoot</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络最小化重定向器完成一个 V_NET_ROOT 对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxflush" data-raw-source="[&lt;strong&gt;MRxFlush&lt;/strong&gt;](./mrxflush.md)"><strong>MRxFlush</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序刷新文件系统对象。 RDBSS 发出此调用以响应接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-flush-buffers" data-raw-source="[&lt;strong&gt;IRP_MJ_FLUSH_BUFFERS&lt;/strong&gt;](./irp-mj-flush-buffers.md)"><strong>IRP_MJ_FLUSH_BUFFERS</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_forceclosed_calldown" data-raw-source="[&lt;strong&gt;MRxForceClosed&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_forceclosed_calldown)"><strong>MRxForceClosed</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序强制关闭。 当 SRV_OPEN 结构的条件不正确或 SRV_OPEN 结构标记为已关闭时，将调用此例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_get_connection_id" data-raw-source="[&lt;strong&gt;MRxGetConnectionId&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_get_connection_id)"><strong>MRxGetConnectionId</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序为连接返回一个连接 ID，该 ID 可用于处理多个会话。 如果网络微型重定向程序支持连接 Id，则返回的连接 ID 将追加到存储在名称表中的连接结构。 RDBSS 会将连接 ID 视为不透明的 blob，并在查找具有给定名称的网络名称表时对连接 ID blob 进行逐字节的比较。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_is_lock_realizable" data-raw-source="[&lt;strong&gt;MRxIsLockRealizable&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_is_lock_realizable)"><strong>MRxIsLockRealizable</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络小型重定向器指示特定 NET_ROOT 结构是否支持字节范围锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkdir_calldown" data-raw-source="[&lt;strong&gt;MRxIsValidDirectory&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkdir_calldown)"><strong>MRxIsValidDirectory</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络小型重定向程序指出路径是否为有效的目录。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-exclusivelock-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_EXCLUSIVELOCK]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-exclusivelock-)"><strong>MRxLowIOSubmit [LOWIO_OP_EXCLUSIVELOCK]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序打开文件对象上的排他锁。 RDBSS 会发出此调用，以响应使用 IRP_MN_LOCK 次要代码接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-lock-control" data-raw-source="[&lt;strong&gt;IRP_MJ_LOCK_CONTROL&lt;/strong&gt;](./irp-mj-lock-control.md)"><strong>IRP_MJ_LOCK_CONTROL</strong></a> ，以及 <strong>IrpSp &gt; 标记</strong> 设置 SL_EXCLUSIVE_LOCK 位。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-fsctl-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_FSCTL]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-fsctl-)"><strong>MRxLowIOSubmit [LOWIO_OP_FSCTL]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以将文件系统控制请求传递到网络小型重定向程序。 RDBSS 发出此调用以响应接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control" data-raw-source="[&lt;strong&gt;IRP_MJ_FILE_SYSTEM_CONTROL&lt;/strong&gt;](./irp-mj-file-system-control.md)"><strong>IRP_MJ_FILE_SYSTEM_CONTROL</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-ioctl-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_IOCTL]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-ioctl-)"><strong>MRxLowIOSubmit [LOWIO_OP_IOCTL]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程将 i/o 系统控制请求传递到网络小型重定向程序。 RDBSS 发出此调用以响应接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](./irp-mj-device-control.md)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a> 或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-internal-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](./irp-mj-internal-device-control.md)"><strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-notify-change-directory-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-notify-change-directory-)"><strong>MRxLowIOSubmit [LOWIO_OP_NOTIFY_CHANGE_DIRECTORY]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程向网络小型重定向程序发出请求，以执行目录更改通知操作。 RDBSS 发出此调用以响应接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-directory-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DIRECTORY_CONTROL&lt;/strong&gt;](./irp-mj-directory-control.md)"><strong>IRP_MJ_DIRECTORY_CONTROL</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-read-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_READ]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-read-)"><strong>MRxLowIOSubmit [LOWIO_OP_READ]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程向网络小型重定向程序发出读取请求。 RDBSS 发出此调用以响应接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-read" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](./irp-mj-read.md)"><strong>IRP_MJ_READ</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-sharedlock-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_SHAREDLOCK]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-sharedlock-)"><strong>MRxLowIOSubmit [LOWIO_OP_SHAREDLOCK]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络重定向程序打开文件对象上的共享锁。 RDBSS 会发出此调用，以响应使用 IRP_MN_LOCK 次要代码接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-lock-control" data-raw-source="[&lt;strong&gt;IRP_MJ_LOCK_CONTROL&lt;/strong&gt;](./irp-mj-lock-control.md)"><strong>IRP_MJ_LOCK_CONTROL</strong></a> ，以及 <strong>IrpSp &gt; 标记</strong> 设置 SL_EXCLUSIVE_LOCK 位。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-unlock-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_UNLOCK]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-unlock-)"><strong>MRxLowIOSubmit [LOWIO_OP_UNLOCK]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序删除文件对象上的单个锁。 RDBSS 发出此调用以响应 IRP_MN_UNLOCK_SINGLE 的次要代码接收 IRP_MJ_LOCK_CONTROL。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-unlock-multiple-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_UNLOCK_MULTIPLE]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-unlock-multiple-)"><strong>MRxLowIOSubmit [LOWIO_OP_UNLOCK_MULTIPLE]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络小型重定向程序删除对某个文件对象持有的多个锁。 RDBSS 发出此调用以响应 IRP_MN_UNLOCK_ALL 或 IRP_MN_UNLOCK_ALL_BY_KEY 的次要代码接收 IRP_MJ_LOCK_CONTROL。 要解锁的范围是在 RX_CONTEXT 的 <strong>LockList</strong> 成员中指定的。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-write-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_WRITE]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-write-)"><strong>MRxLowIOSubmit [LOWIO_OP_WRITE]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程向网络小型重定向程序发出写入请求。 RDBSS 发出此调用以响应接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-write" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](./irp-mj-write.md)"><strong>IRP_MJ_WRITE</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_preparse_name" data-raw-source="[&lt;strong&gt;MRxPreparseName&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_preparse_name)"><strong>MRxPreparseName</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，为网络微重定向程序指定 preparse 名称的机会。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxquerydirectory" data-raw-source="[&lt;strong&gt;MRxQueryDirectory&lt;/strong&gt;](./mrxquerydirectory.md)"><strong>MRxQueryDirectory</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求一个有关文件目录系统对象的网络微重定向程序查询信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryeainfo" data-raw-source="[&lt;strong&gt;MRxQueryEaInfo&lt;/strong&gt;](./mrxqueryeainfo.md)"><strong>MRxQueryEaInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向器查询文件系统对象上的扩展属性信息。 RDBSS 发出此调用以响应接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-ea" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_EA&lt;/strong&gt;](./irp-mj-query-ea.md)"><strong>IRP_MJ_QUERY_EA</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryfileinfo" data-raw-source="[&lt;strong&gt;MRxQueryFileInfo&lt;/strong&gt;](./mrxqueryfileinfo.md)"><strong>MRxQueryFileInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求一个有关文件系统对象的网络微型重定向程序查询文件信息。 RDBSS 发出此调用以响应接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-information" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_INFORMATION&lt;/strong&gt;](./irp-mj-query-information.md)"><strong>IRP_MJ_QUERY_INFORMATION</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryquotainfo" data-raw-source="[&lt;strong&gt;MRxQueryQuotaInfo&lt;/strong&gt;](./mrxqueryquotainfo.md)"><strong>MRxQueryQuotaInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序查询有关文件系统对象的配额信息。 RDBSS 发出此调用以响应接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-quota" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_QUOTA&lt;/strong&gt;](./irp-mj-query-quota.md)"><strong>IRP_MJ_QUERY_QUOTA</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxquerysdinfo" data-raw-source="[&lt;strong&gt;MRxQuerySdInfo&lt;/strong&gt;](./mrxquerysdinfo.md)"><strong>MRxQuerySdInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序查询有关文件系统对象的安全描述符信息。 RDBSS 发出此调用以响应接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-security" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_SECURITY&lt;/strong&gt;](./irp-mj-query-security.md)"><strong>IRP_MJ_QUERY_SECURITY</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryvolumeinfo" data-raw-source="[&lt;strong&gt;MRxQueryVolumeInfo&lt;/strong&gt;](./mrxqueryvolumeinfo.md)"><strong>MRxQueryVolumeInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络最小化重定向器查询卷信息。 RDBSS 发出此调用以响应接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-volume-information" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_VOLUME_INFORMATION&lt;/strong&gt;](./irp-mj-query-volume-information.md)"><strong>IRP_MJ_QUERY_VOLUME_INFORMATION</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxseteainfo" data-raw-source="[&lt;strong&gt;MRxSetEaInfo&lt;/strong&gt;](./mrxseteainfo.md)"><strong>MRxSetEaInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序设置文件系统对象的扩展属性信息。 RDBSS 发出此调用以响应接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-ea" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_EA&lt;/strong&gt;](./irp-mj-set-ea.md)"><strong>IRP_MJ_SET_EA</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetfileinfo" data-raw-source="[&lt;strong&gt;MRxSetFileInfo&lt;/strong&gt;](./mrxsetfileinfo.md)"><strong>MRxSetFileInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序在文件系统对象上设置文件信息。 RDBSS 发出此调用以响应接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-information" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_INFORMATION&lt;/strong&gt;](./irp-mj-set-information.md)"><strong>IRP_MJ_SET_INFORMATION</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetfileinfoatcleanup" data-raw-source="[&lt;strong&gt;MRxSetFileInfoAtCleanup&lt;/strong&gt;](./mrxsetfileinfoatcleanup.md)"><strong>MRxSetFileInfoAtCleanup</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序在清理时在文件系统对象上设置文件信息。 当应用程序关闭句柄，但在 i/o 管理器关闭文件对象之前，RDBSS 将在清理过程中发出此调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetquotainfo" data-raw-source="[&lt;strong&gt;MRxSetQuotaInfo&lt;/strong&gt;](./mrxsetquotainfo.md)"><strong>MRxSetQuotaInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络最小化重定向器在文件系统对象上设置配额信息。 RDBSS 发出此调用以响应接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-quota" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_QUOTA&lt;/strong&gt;](./irp-mj-set-quota.md)"><strong>IRP_MJ_SET_QUOTA</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetsdinfo" data-raw-source="[&lt;strong&gt;MRxSetSdInfo&lt;/strong&gt;](./mrxsetsdinfo.md)"><strong>MRxSetSdInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序设置文件系统对象的安全描述符信息。 RDBSS 发出此调用以响应接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-security" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_SECURITY&lt;/strong&gt;](./irp-mj-set-security.md)"><strong>IRP_MJ_SET_SECURITY</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetvolumeinfo" data-raw-source="[&lt;strong&gt;MRxSetVolumeInfo&lt;/strong&gt;](./mrxsetvolumeinfo.md)"><strong>MRxSetVolumeInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序设置卷信息。 RDBSS 发出此调用以响应接收 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-volume-information" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_VOLUME_INFORMATION&lt;/strong&gt;](./irp-mj-set-volume-information.md)"><strong>IRP_MJ_SET_VOLUME_INFORMATION</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxshouldtrytocollapsethisopen" data-raw-source="[&lt;strong&gt;MRxShouldTryToCollapseThisOpen&lt;/strong&gt;](./mrxshouldtrytocollapsethisopen.md)"><strong>MRxShouldTryToCollapseThisOpen</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络小型重定向程序指示 RDBSS 是否应尝试并将打开的请求折叠到现有的文件系统对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_srvcall_winner_notify" data-raw-source="[&lt;strong&gt;MRxSrvCallWinnerNotify&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_srvcall_winner_notify)"><strong>MRxSrvCallWinnerNotify</strong></a></td>
<td align="left"><p>此例程最初设计为由 RDBSS 调用，以便在多个重定向程序可能满足请求时通知网络小型重定向器它是 "入选方"。 预期的网络微重定向器应创建 SRV_CALL 结构并建立与服务器的连接。</p>
<p>在 RDBSS 的当前实现下，每个网络微型重定向程序都有其自己的 RDBSS 副本，因此在 RDBSS 层没有争用的网络重定向程序。 此例程在每次请求创建 SRV_CALL 结构后调用。</p>
<p>如果安装了多个重定向程序来处理相同的通用命名约定 (UNC) 命名空间，则多 UNC 提供程序将根据注册表中指定的重定向程序的顺序， (MUP) 选择用于处理请求的重定向程序。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx" data-raw-source="[&lt;strong&gt;MRxStart&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx)"><strong>MRxStart</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来启动网络小型重定向程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxstop" data-raw-source="[&lt;strong&gt;MRxStop&lt;/strong&gt;](./mrxstop.md)"><strong>MRxStop</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来停止网络微型重定向程序。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxtruncate" data-raw-source="[&lt;strong&gt;MRxTruncate&lt;/strong&gt;](./mrxtruncate.md)"><strong>MRxTruncate</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络最小化重定向器截断文件系统对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxzeroextend" data-raw-source="[&lt;strong&gt;MRxZeroExtend&lt;/strong&gt;](./mrxzeroextend.md)"><strong>MRxZeroExtend</strong></a></td>
<td align="left"><p>如果文件大小大于 FCB 的有效数据长度，RDBSS 将调用此例程来请求网络最小化重定向程序扩展文件系统对象（清除时使用零）来填充文件。</p></td>
</tr>
</tbody>
</table>

 

 

