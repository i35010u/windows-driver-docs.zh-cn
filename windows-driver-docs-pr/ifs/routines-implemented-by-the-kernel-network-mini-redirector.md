---
title: 由内核网络微型重定向程序实现的例程
description: 由内核网络微型重定向程序实现的例程
ms.assetid: bd1a8989-100d-4b7b-9a61-521af6433b00
keywords:
- 最小-重定向程序 WDK，实现的例程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d839ef5d02349f4a3729cfa2213d4e413d5b046e
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464095"
---
# <a name="routines-implemented-by-the-kernel-network-mini-redirector"></a>由内核网络微型重定向程序实现的例程


下面的例程可由网络微型重定向实现：

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
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549838" data-raw-source="[&lt;strong&gt;MRxAreFilesAliased&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549838)"><strong>MRxAreFilesAliased</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来查询网络微型重定向，如果两个文件控制块 (FCB) 结构表示同一个文件。 RDBSS 调用此例程时处理两个文件看上去相同但具有不同的名称 （MS-DOS 短名称和长名称，例如）。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549841" data-raw-source="[&lt;strong&gt;MRxCleanupFobx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549841)"><strong>MRxCleanupFobx</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向，关闭文件系统对象扩展结构。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff548608" data-raw-source="[&lt;strong&gt;IRP_MJ_CLEANUP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548608)"> <strong>IRP_MJ_CLEANUP</strong> </a>对文件对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549845" data-raw-source="[&lt;strong&gt;MRxCloseSrvOpen&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549845)"><strong>MRxCloseSrvOpen</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向关闭 SRV_OPEN 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549847" data-raw-source="[&lt;strong&gt;MRxCollapseOpen&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549847)"><strong>MRxCollapseOpen</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向折叠到现有 SRV_OPEN 上打开的文件系统的请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549850" data-raw-source="[&lt;strong&gt;MRxCompleteBufferingStateChangeRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549850)"><strong>MRxCompleteBufferingStateChangeRequest</strong></a></td>
<td align="left"><p>RDBSS 调用以通知网络微型重定向缓冲的状态更改请求已完成此例程。 例如，SMB 重定向程序使用此例程来发送 oplock 中断响应或关闭上破坏 oplock 句柄，如果该文件不再使用。 需要刷新到服务器的字节范围锁传递给网络微型-重定向程序中<strong>LowIoContext.ParamsFor.Locks.LockList</strong> RX_CONTEXT 结构中的成员。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549856" data-raw-source="[&lt;strong&gt;MRxComputeNewBufferingState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549856)"><strong>MRxComputeNewBufferingState</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向计算新的缓冲状态更改。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549862" data-raw-source="[&lt;strong&gt;MRxCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549862)"><strong>MRxCreate</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向创建文件系统对象。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff548630" data-raw-source="[&lt;strong&gt;IRP_MJ_CREATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548630)"> <strong>IRP_MJ_CREATE</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549864" data-raw-source="[&lt;strong&gt;MRxCreateSrvCall&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549864)"><strong>MRxCreateSrvCall</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向创建 SRV_CALL 结构并建立与服务器的连接。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549869" data-raw-source="[&lt;strong&gt;MRxCreateVNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549869)"><strong>MRxCreateVNetRoot</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向创建 V_NET_ROOT 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549871" data-raw-source="[&lt;strong&gt;MRxDeallocateForFcb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549871)"><strong>MRxDeallocateForFcb</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向解除分配 FCB。 此调用是对关闭文件系统对象的请求的响应中。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549872" data-raw-source="[&lt;strong&gt;MRxDeallocateForFobx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549872)"><strong>MRxDeallocateForFobx</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向解除分配 FOBX 结构。 此调用是对关闭文件系统对象的请求的响应中。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549876" data-raw-source="[&lt;strong&gt;MRxDevFcbXXXControlFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549876)"><strong>MRxDevFcbXXXControlFile</strong></a></td>
<td align="left"><p>RDBSS 调用此例程将传递给网络微型重定向的设备 FCB 控制请求。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff548649" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548649)"> <strong>IRP_MJ_DEVICE_CONTROL</strong></a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff548670" data-raw-source="[&lt;strong&gt;IRP_MJ_FILE_SYSTEM_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548670)"> <strong>IRP_MJ_FILE_SYSTEM_CONTROL</strong></a>，或<a href="https://msdn.microsoft.com/library/windows/hardware/ff549241" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549241)"> <strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong> </a> FCB 的设备上。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549878" data-raw-source="[&lt;strong&gt;MRxExtendForCache&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549878)"><strong>MRxExtendForCache</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向扩展一个文件，则将文件缓存的缓存管理器时。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549879" data-raw-source="[&lt;strong&gt;MRxExtendForNonCache&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549879)"><strong>MRxExtendForNonCache</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向扩展一个文件，当缓存管理器不缓存该文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550649" data-raw-source="[&lt;strong&gt;MRxExtractNetRootName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550649)"><strong>MRxExtractNetRootName</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向从给定的路径名称中提取 NET_ROOT 的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550653" data-raw-source="[&lt;strong&gt;MRxFinalizeNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550653)"><strong>MRxFinalizeNetRoot</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向完成 NET_ROOT 对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550656" data-raw-source="[&lt;strong&gt;MRxFinalizeSrvCall&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550656)"><strong>MRxFinalizeSrvCall</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向完成用于建立与服务器连接的 SRV_CALL 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550663" data-raw-source="[&lt;strong&gt;MRxFinalizeVNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550663)"><strong>MRxFinalizeVNetRoot</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向完成 V_NET_ROOT 对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550669" data-raw-source="[&lt;strong&gt;MRxFlush&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550669)"><strong>MRxFlush</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向刷新文件系统对象。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff549235" data-raw-source="[&lt;strong&gt;IRP_MJ_FLUSH_BUFFERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549235)"> <strong>IRP_MJ_FLUSH_BUFFERS</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550677" data-raw-source="[&lt;strong&gt;MRxForceClosed&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550677)"><strong>MRxForceClosed</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向强制关闭。 此例程称为 SRV_OPEN 结构的条件是错误或 SRV_OPEN 结构标记为已关闭时。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550687" data-raw-source="[&lt;strong&gt;MRxGetConnectionId&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550687)"><strong>MRxGetConnectionId</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向返回可用于处理多个会话的连接的连接 ID。 如果网络微型重定向支持连接 Id，则返回的连接 ID 追加到名称表中存储的连接结构。 RDBSS 认为连接 ID 的不透明 blob，并查找具有给定名称的 net 名称表时没有按字节进行比较的连接 ID 的 blob。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550691" data-raw-source="[&lt;strong&gt;MRxIsLockRealizable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550691)"><strong>MRxIsLockRealizable</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向，指示是否对特定 NET_ROOT 结构支持字节范围锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550696" data-raw-source="[&lt;strong&gt;MRxIsValidDirectory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550696)"><strong>MRxIsValidDirectory</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向指示路径是否是有效的目录。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550703" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_EXCLUSIVELOCK]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550703)"><strong>MRxLowIOSubmit[LOWIO_OP_EXCLUSIVELOCK]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向，打开文件对象的排他锁。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff549251" data-raw-source="[&lt;strong&gt;IRP_MJ_LOCK_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549251)"> <strong>IRP_MJ_LOCK_CONTROL</strong> </a> IRP_MN_LOCK 次要代码以及何时<strong>IrpSp-&gt;标志</strong>具有 SL_EXCLUSIVE_LOCK 位集。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550709" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_FSCTL]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550709)"><strong>MRxLowIOSubmit[LOWIO_OP_FSCTL]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程将传递给网络微型重定向的文件系统控制请求。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff548670" data-raw-source="[&lt;strong&gt;IRP_MJ_FILE_SYSTEM_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548670)"> <strong>IRP_MJ_FILE_SYSTEM_CONTROL</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550715" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_IOCTL]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550715)"><strong>MRxLowIOSubmit[LOWIO_OP_IOCTL]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程将传递给网络微型重定向 I/O 系统控制请求。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff548649" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548649)"> <strong>IRP_MJ_DEVICE_CONTROL</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff549241" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549241)"> <strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550721" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550721)"><strong>MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，以向网络微型重定向目录更改通知操作发出请求。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff548658" data-raw-source="[&lt;strong&gt;IRP_MJ_DIRECTORY_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548658)"> <strong>IRP_MJ_DIRECTORY_CONTROL</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550724" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_READ]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550724)"><strong>MRxLowIOSubmit[LOWIO_OP_READ]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程网络微型重定向到发出读取的请求。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff549327" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549327)"> <strong>IRP_MJ_READ</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550734" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_SHAREDLOCK]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550734)"><strong>MRxLowIOSubmit[LOWIO_OP_SHAREDLOCK]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络重定向程序打开文件对象上的共享的锁。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff549251" data-raw-source="[&lt;strong&gt;IRP_MJ_LOCK_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549251)"> <strong>IRP_MJ_LOCK_CONTROL</strong> </a> IRP_MN_LOCK 次要代码以及何时<strong>IrpSp-&gt;标志</strong>具有 SL_EXCLUSIVE_LOCK 位集。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550740" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_UNLOCK]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550740)"><strong>MRxLowIOSubmit[LOWIO_OP_UNLOCK]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向移除对文件对象的单个锁。 RDBSS 发出响应接收的 IRP_MN_UNLOCK_SINGLE 细微的代码与 IRP_MJ_LOCK_CONTROL 此调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550745" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_UNLOCK_MULTIPLE]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550745)"><strong>MRxLowIOSubmit[LOWIO_OP_UNLOCK_MULTIPLE]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向删除多个文件对象持有的锁。 RDBSS 发出响应接收 IRP_MJ_LOCK_CONTROL IRP_MN_UNLOCK_ALL 或 IRP_MN_UNLOCK_ALL_BY_KEY 的细微的代码使用此调用。 中指定的范围，以便能够解锁<strong>LowIoContext.ParamsFor.Locks.LockList</strong> RX_CONTEXT 的成员。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550746" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_WRITE]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550746)"><strong>MRxLowIOSubmit[LOWIO_OP_WRITE]</strong></a></td>
<td align="left"><p>RDBSS 调用此例程网络微型重定向到发出写入请求。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff549427" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549427)"> <strong>IRP_MJ_WRITE</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550750" data-raw-source="[&lt;strong&gt;MRxPreparseName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550750)"><strong>MRxPreparseName</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，以使网络微型重定向有机会 preparse 一个名称。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550755" data-raw-source="[&lt;strong&gt;MRxQueryDirectory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550755)"><strong>MRxQueryDirectory</strong></a></td>
<td align="left"><p>RDBSS 文件目录系统对象上调用此例程以请求的网络微型重定向查询信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550759" data-raw-source="[&lt;strong&gt;MRxQueryEaInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550759)"><strong>MRxQueryEaInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向查询扩展文件系统对象的属性信息。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff549279" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_EA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549279)"> <strong>IRP_MJ_QUERY_EA</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550770" data-raw-source="[&lt;strong&gt;MRxQueryFileInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550770)"><strong>MRxQueryFileInfo</strong></a></td>
<td align="left"><p>RDBSS 对文件系统对象调用此例程以请求的网络微型重定向查询文件信息。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff549283" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549283)"> <strong>IRP_MJ_QUERY_INFORMATION</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550773" data-raw-source="[&lt;strong&gt;MRxQueryQuotaInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550773)"><strong>MRxQueryQuotaInfo</strong></a></td>
<td align="left"><p>RDBSS 对文件系统对象调用此例程以请求的网络微型重定向查询配额信息。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff549293" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_QUOTA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549293)"> <strong>IRP_MJ_QUERY_QUOTA</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550776" data-raw-source="[&lt;strong&gt;MRxQuerySdInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550776)"><strong>MRxQuerySdInfo</strong></a></td>
<td align="left"><p>RDBSS 对文件系统对象调用此例程以请求的网络微型重定向查询安全描述符信息。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff549298" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_SECURITY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549298)"> <strong>IRP_MJ_QUERY_SECURITY</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550782" data-raw-source="[&lt;strong&gt;MRxQueryVolumeInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550782)"><strong>MRxQueryVolumeInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求的网络微型重定向查询卷信息。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff549318" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_VOLUME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549318)"> <strong>IRP_MJ_QUERY_VOLUME_INFORMATION</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550786" data-raw-source="[&lt;strong&gt;MRxSetEaInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550786)"><strong>MRxSetEaInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向程序集扩展文件系统对象的属性信息。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff549346" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_EA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549346)"> <strong>IRP_MJ_SET_EA</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550790" data-raw-source="[&lt;strong&gt;MRxSetFileInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550790)"><strong>MRxSetFileInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向设置文件系统对象上的文件信息。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff549366" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549366)"> <strong>IRP_MJ_SET_INFORMATION</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550796" data-raw-source="[&lt;strong&gt;MRxSetFileInfoAtCleanup&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550796)"><strong>MRxSetFileInfoAtCleanup</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向，在清理的文件系统对象上设置文件的信息。 当关闭句柄的应用程序，但文件之前，对象已关闭的 I/O 管理器，RDBSS 清理期间发出此调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550800" data-raw-source="[&lt;strong&gt;MRxSetQuotaInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550800)"><strong>MRxSetQuotaInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向，在文件系统对象设置的配额信息。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff549401" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_QUOTA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549401)"> <strong>IRP_MJ_SET_QUOTA</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550805" data-raw-source="[&lt;strong&gt;MRxSetSdInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550805)"><strong>MRxSetSdInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向，在文件系统对象设置安全描述符信息。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff549407" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_SECURITY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549407)"> <strong>IRP_MJ_SET_SECURITY</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550810" data-raw-source="[&lt;strong&gt;MRxSetVolumeInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550810)"><strong>MRxSetVolumeInfo</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向设置卷信息。 RDBSS 发出此调用中接收响应<a href="https://msdn.microsoft.com/library/windows/hardware/ff549415" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_VOLUME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549415)"> <strong>IRP_MJ_SET_VOLUME_INFORMATION</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550817" data-raw-source="[&lt;strong&gt;MRxShouldTryToCollapseThisOpen&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550817)"><strong>MRxShouldTryToCollapseThisOpen</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向指示是否 RDBSS 应尝试并折叠了打开请求到现有的文件系统对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550824" data-raw-source="[&lt;strong&gt;MRxSrvCallWinnerNotify&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550824)"><strong>MRxSrvCallWinnerNotify</strong></a></td>
<td align="left"><p>此例程最初设计用于由 RDBSS 以通知网络微型重定向，它是"赢家"调用时多个重定向程序无法完成请求。 入选网络的微型重定向需要创建 SRV_CALL 结构并建立与服务器的连接。</p>
<p>下 RDBSS 当前实现中，每个网络微型重定向有其自己的 RDBSS，副本，因此在 RDBSS 层包含任何竞争的网络重定向程序。 此例程称为后创建 SRV_CALL 结构的每个请求。</p>
<p>当处理相同的通用命名约定 (UNC) 命名空间为安装了多个重定向程序时，重定向程序若要为请求提供服务选择的重定向程序在注册表中指定的顺序基于多个 UNC Provider (MUP)。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550829" data-raw-source="[&lt;strong&gt;MRxStart&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550829)"><strong>MRxStart</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，以启动网络微型重定向。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550833" data-raw-source="[&lt;strong&gt;MRxStop&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550833)"><strong>MRxStop</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，以停止网络微型重定向。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550839" data-raw-source="[&lt;strong&gt;MRxTruncate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550839)"><strong>MRxTruncate</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向截断文件系统对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550844" data-raw-source="[&lt;strong&gt;MRxZeroExtend&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550844)"><strong>MRxZeroExtend</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向扩展用清除零填充该文件，如果文件大小大于 FCB 的有效数据长度的文件系统对象。</p></td>
</tr>
</tbody>
</table>

 

 

 




