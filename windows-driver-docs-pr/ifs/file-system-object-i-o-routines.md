---
title: 文件系统对象 I/O 例程
description: 文件系统对象 I/O 例程
ms.assetid: 0514e396-76b9-458b-9a98-e539d7e90274
keywords:
- 最小重定向程序 WDK，对象 I/O 例程
- I/O WDK 网络重定向程序
- 低-/ O 例程 WDK 网络重定向程序
- 文件系统对象 I/O WDK
- 文件对象 WDK 微型-重定向程序
- 对象 WDK 微型-重定向程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fa0c5092cb7bf27ad4ba384bbdfe2bff4976960
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369263"
---
# <a name="file-system-object-io-routines"></a>文件系统对象 I/O 例程


文件系统对象 I/O 例程表示传统的文件 I/O 调用的读取、 写入和其他文件操作。 这些例程通常称为"低 I/O 例程"在网络微型重定向。 RDBSS 响应接收特定 IRP 调用这些例程

较低的 I/O 例程中作为传递的例程的指针的数组作为一部分 MINIRDR\_调度结构传递给[ **RxRegisterMinirdr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxregisterminirdr)用于注册网络的例程最小重定向程序在启动时 (在**DriverEntry**例程)。 数组项的值是要执行的较低的 I/O 操作。

这些较低的 I/O 或文件系统对象 I/O 例程是通常情况下以异步方式由调用 RDBSS。 因此网络微型重定向必须确保实现任何低 I/O 例程可以安全地调用以异步方式。 还有可能为网络微型-重定向器要忽略的异步调用的请求，并实现例程，以仅同步运行。 但是，对于某些需要时间才能完成 （读取和写入，例如） 的调用，实现这些为同步操作可以显著减少整个操作系统的 I/O 性能。

所有文件系统对象 I/O 例程都预期指向 RX\_上下文结构中作为参数进行传递。 调用这些例程之前, RDBSS 设置的值中的成员数目**LowIoContext** RX 结构\_上下文。 中的成员的一些**LowIoContext**结构设置对于所有例程，而某些成员仅设置为特定的例程。 RX\_上下文数据结构包含正在处理并具有 IRP **LowIoContext.Operation**成员，指定要执行的较低的 I/O 操作。 可以为多个较低的 I/O 例程，使其指向网络微型重定向中的相同例程，因为这**LowIoContext.Operation**成员可用于区分请求的较低的 I/O 操作。 例如，所有与文件锁相关的 I/O 调用可以调用相同的低 I/O 例程网络微型-重定向程序中使用**LowIoContext.Operation**成员区分锁定或解锁请求的操作。

其他文件 I/O 例程而不是较低的 I/O 例程根据同步调用时，虽然这是受将来版本中更改的 Windows 操作系统。

在 LowIo 路径**LowIoContext.ResourceThreadId** RX 成员\_上下文保证以指示启动了该操作在 RDBSS 拥有线程。 **LowIoContext.ResourceThreadId**成员可用于代表另一个线程释放 FCB 资源。 完成异步例程后，可以释放已获取从初始线程的 FCB 资源。

如果**MrxLowIoSubmit\[LOWIO\_OP\_XXX\]** 例程是很可能需要很长时间才能完成，网络微型重定向程序驱动程序应释放之前 FCB 资源启动网络通信。 可以通过调用释放 FCB 资源[ **RxReleaseFcbResourceForThreadInMRx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)。

下表列出了可以由网络微型重定向的文件系统对象 I/O (低 I/O) 操作的例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-exclusivelock-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_EXCLUSIVELOCK]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-exclusivelock-)"><strong>MRxLowIOSubmit[LOWIO_OP_EXCLUSIVELOCK]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向，打开文件对象的排他锁。 RDBSS 发出此调用以响应接收 IRP_MN_LOCK 和 IrpSp-细微的代码与 IRP_MJ_LOCK_CONTROL&gt;标志有 SL_EXCLUSIVE_LOCK 位组。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-fsctl-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_FSCTL]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-fsctl-)"><strong>MRxLowIOSubmit[LOWIO_OP_FSCTL]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程将传递给网络微型重定向的文件系统控制请求。 RDBSS 发出响应接收 IRP_MJ_FILE_SYSTEM_CONTROL 此调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-ioctl-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_IOCTL]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-ioctl-)"><strong>MRxLowIOSubmit[LOWIO_OP_IOCTL]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程将传递给网络微型重定向 I/O 系统控制请求。 RDBSS 发出响应 IRP_MJ_DEVICE_CONTROL 或 IRP_MJ_INTERNAL_DEVICE_CONTROL 接收此调用...</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-notify-change-directory-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-notify-change-directory-)"><strong>MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，以向网络微型重定向目录更改通知操作发出请求。 RDBSS 发出响应接收 IRP_MJ_DIRECTORY_CONTROL 此调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-read-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_READ]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-read-)"><strong>MRxLowIOSubmit[LOWIO_OP_READ]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程网络微型重定向到发出读取的请求。 RDBSS 发出响应接收 IRP_MJ_READ 此调用。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-sharedlock-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_SHAREDLOCK]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-sharedlock-)"><strong>MRxLowIOSubmit[LOWIO_OP_SHAREDLOCK]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络重定向程序打开文件对象上的共享的锁。 RDBSS 发出此调用以响应接收 IRP_MN_LOCK 和 IrpSp-细微的代码与 IRP_MJ_LOCK_CONTROL&gt;标志不具有 SL_EXCLUSIVE_LOCK 位组。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-unlock-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_UNLOCK]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-unlock-)"><strong>MRxLowIOSubmit[LOWIO_OP_UNLOCK]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向移除对文件对象的单个锁。 RDBSS 发出响应接收的 IRP_MN_UNLOCK_SINGLE 细微的代码与 IRP_MJ_LOCK_CONTROL 此调用。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-unlock-multiple-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_UNLOCK_MULTIPLE]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-unlock-multiple-)"><strong>MRxLowIOSubmit[LOWIO_OP_UNLOCK_MULTIPLE]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向删除多个文件对象持有的锁。 RDBSS 发出响应接收 IRP_MJ_LOCK_CONTROL IRP_MN_UNLOCK_ALL 或 IRP_MN_UNLOCK_ALL_BY_KEY 的细微的代码使用此调用。 中指定的字节范围，以便能够解锁<strong>LowIoContext.ParamsFor.Locks.LockList</strong> RX_CONTEXT 的成员。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-write-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_WRITE]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-write-)"><strong>MRxLowIOSubmit[LOWIO_OP_WRITE]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程网络微型重定向到发出写入请求。 RDBSS 发出响应接收 IRP_MJ_WRITE 此调用。</p></td>
</tr>
</tbody>
</table>

 

 

 




