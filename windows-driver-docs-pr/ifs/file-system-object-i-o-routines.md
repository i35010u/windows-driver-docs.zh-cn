---
title: 文件系统对象 I/O 例程
description: 文件系统对象 I/O 例程
keywords:
- 小型重定向程序 WDK，对象 i/o 例程
- I/o WDK 网络重定向器
- 低 i/o 例程 WDK 网络重定向程序
- 文件系统对象 i/o WDK
- 文件对象 WDK 微型重定向程序
- 对象 WDK 微型重定向器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb88bf1b5a020aa01d306085128f633a574e1521
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786839"
---
# <a name="file-system-object-io-routines"></a>文件系统对象 I/O 例程


文件系统对象 i/o 例程表示用于读取、写入和其他文件操作的传统文件 i/o 调用。 这些例程在网络小型重定向程序中通常称为 "低 i/o 例程"。 RDBSS 调用这些例程来响应接收特定 IRP

低 i/o 例程作为一系列例程指针传入，作为将 MINIRDR \_ 调度结构传递到 [**RxRegisterMinirdr**](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr) 例程的一部分，该构造用于在 **DriverEntry** 例程) 中的 (启动时注册网络小型重定向程序。 数组项的值是要执行的低 i/o 操作。

通常由 RDBSS 异步调用这些低 i/o 或文件系统对象 i/o 例程。 因此，网络小型重定向程序必须确保可以安全地以异步方式调用任何实现的低 i/o 例程。 网络小型重定向器还可以忽略异步调用请求，并实现仅同步操作的例程。 但是，对于某些可能需要花费时间才能完成 (读取和写入的调用，例如) ，将它们作为同步操作实现可显著降低整个操作系统的 i/o 性能。

所有文件系统对象 i/o 例程都需要一个指向要 \_ 作为参数传入的 RX 上下文结构的指针。 在调用这些例程之前，RDBSS 设置 RX 上下文的 **LowIoContext** 结构中的多个成员的值 \_ 。 **LowIoContext** 结构中的某些成员是为所有例程设置的，而某些成员只是针对特定例程设置的。 RX \_ 上下文数据结构包含正在处理的 IRP，并具有 **LowIoContext** 成员，该成员指定要执行的低 i/o 操作。 由于可以使用此 **LowIoContext** 成员来区分请求的低 i/o 操作，因此几个低 i/o 例程可能会指向网络小型重定向程序中的同一例程。 例如，所有与文件锁相关的 i/o 调用都可以调用网络小型重定向程序中的相同低 i/o 例程，该例程使用 **LowIoContext** 成员来区分请求的锁定或解锁操作。

除低 i/o 例程以外的其他文件 i/o 例程都基于同步调用，但在将来的 Windows 操作系统版本中可能会有所更改。

在 LowIo 路径中，可保证 RX 上下文的 **LowIoContext ResourceThreadId** 成员 \_ 指示在 RDBSS 中启动操作的拥有线程。 **LowIoContext. ResourceThreadId** 成员可用于代表其他线程发布 FCB 资源。 异步例程完成后，可以释放从初始线程获取的 FCB 资源。

如果 **MrxLowIoSubmit \[ LOWIO \_ OP \_ XXX \]** 例程可能需要很长时间才能完成，则网络小型重定向程序驱动程序应在启动网络通信之前释放 FCB 资源。 可以通过调用 [**RxReleaseFcbResourceForThreadInMRx**](/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)释放 FCB 资源。

下表列出了可由用于文件系统对象 i/o 的网络微重定向器 (低 i/o) 操作实现的例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程所返回的值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-exclusivelock-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_EXCLUSIVELOCK]&lt;/strong&gt;](./mrxlowiosubmit-lowio-op-exclusivelock-.md)"><strong>MRxLowIOSubmit [LOWIO_OP_EXCLUSIVELOCK]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序打开文件对象上的排他锁。 RDBSS 发出此调用，以响应使用次要代码 IRP_MN_LOCK 和 IrpSp &gt; 设置 SL_EXCLUSIVE_LOCK 的 IRP_MJ_LOCK_CONTROL。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-fsctl-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_FSCTL]&lt;/strong&gt;](./mrxlowiosubmit-lowio-op-fsctl-.md)"><strong>MRxLowIOSubmit [LOWIO_OP_FSCTL]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以将文件系统控制请求传递到网络小型重定向程序。 RDBSS 发出此调用以响应接收 IRP_MJ_FILE_SYSTEM_CONTROL。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-ioctl-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_IOCTL]&lt;/strong&gt;](./mrxlowiosubmit-lowio-op-ioctl-.md)"><strong>MRxLowIOSubmit [LOWIO_OP_IOCTL]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程将 i/o 系统控制请求传递到网络小型重定向程序。 RDBSS 发出此调用以响应接收 IRP_MJ_DEVICE_CONTROL 或 IRP_MJ_INTERNAL_DEVICE_CONTROL。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-notify-change-directory-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY]&lt;/strong&gt;](./mrxlowiosubmit-lowio-op-notify-change-directory-.md)"><strong>MRxLowIOSubmit [LOWIO_OP_NOTIFY_CHANGE_DIRECTORY]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程向网络小型重定向程序发出请求，以执行目录更改通知操作。 RDBSS 发出此调用以响应接收 IRP_MJ_DIRECTORY_CONTROL。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-read-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_READ]&lt;/strong&gt;](./mrxlowiosubmit-lowio-op-read-.md)"><strong>MRxLowIOSubmit [LOWIO_OP_READ]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程向网络小型重定向程序发出读取请求。 RDBSS 发出此调用以响应接收 IRP_MJ_READ。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-sharedlock-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_SHAREDLOCK]&lt;/strong&gt;](./mrxlowiosubmit-lowio-op-sharedlock-.md)"><strong>MRxLowIOSubmit [LOWIO_OP_SHAREDLOCK]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络重定向程序打开文件对象上的共享锁。 RDBSS 发出此调用以响应接收 IRP_MN_LOCK 次要代码为和 IrpSp 的 IRP_MJ_LOCK_CONTROL，但 &gt; 未设置 SL_EXCLUSIVE_LOCK 位。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-unlock-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_UNLOCK]&lt;/strong&gt;](./mrxlowiosubmit-lowio-op-unlock-.md)"><strong>MRxLowIOSubmit [LOWIO_OP_UNLOCK]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序删除文件对象上的单个锁。 RDBSS 发出此调用以响应 IRP_MN_UNLOCK_SINGLE 的次要代码接收 IRP_MJ_LOCK_CONTROL。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-unlock-multiple-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_UNLOCK_MULTIPLE]&lt;/strong&gt;](./mrxlowiosubmit-lowio-op-unlock-multiple-.md)"><strong>MRxLowIOSubmit [LOWIO_OP_UNLOCK_MULTIPLE]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络小型重定向程序删除对某个文件对象持有的多个锁。 RDBSS 发出此调用以响应 IRP_MN_UNLOCK_ALL 或 IRP_MN_UNLOCK_ALL_BY_KEY 的次要代码接收 IRP_MJ_LOCK_CONTROL。 要解锁的字节范围是在 RX_CONTEXT 的 <strong>LockList</strong> 成员中指定的。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-write-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_WRITE]&lt;/strong&gt;](./mrxlowiosubmit-lowio-op-write-.md)"><strong>MRxLowIOSubmit [LOWIO_OP_WRITE]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程向网络小型重定向程序发出写入请求。 RDBSS 发出此调用以响应接收 IRP_MJ_WRITE。</p></td>
</tr>
</tbody>
</table>

 

