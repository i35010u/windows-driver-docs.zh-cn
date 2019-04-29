---
title: 杂项网络微型重定向程序例程
description: 杂项网络微型重定向程序例程
ms.assetid: bad5847c-8ac5-4e63-a0a5-3bbf13424928
keywords:
- 最小重定向程序 WDK，杂项例程
- 连接 Id WDK 网络重定向程序
- 缓冲状态 WDK 网络重定向程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7346b3d17626d2cafd02c458e1c7f34ea949474
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384283"
---
# <a name="miscellaneous-network-mini-redirector-routines"></a>杂项网络微型重定向程序例程


少数其他例程由网络微型重定向处理缓冲状态管理和连接 Id。 缓冲状态管理例程可以使用网络微型重定向来处理各种缓冲方案中重定向程序和服务器实现以及通信中缓冲状态的任何更改。 例如， [ **MRxCompleteBufferingStateChangeRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff549850)例程由 SMB 重定向程序用作的机制的一部分来向服务器发送破坏 oplock。

连接 Id 可以用于多路复用多个连接。 网络微型-重定向程序以支持连接 Id，因此，不必[ **MRxGetConnectionId** ](https://msdn.microsoft.com/library/windows/hardware/ff550687)是可选的。

下表列出了可以由网络微型-重定向程序用于执行其他操作的例程。

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
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549850" data-raw-source="[&lt;strong&gt;MRxCompleteBufferingStateChangeRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549850)"><strong>MRxCompleteBufferingStateChangeRequest</strong></a></td>
<td align="left"><p>RDBSS 调用以通知网络微型重定向缓冲的状态更改请求已完成此例程。 例如，SMB 重定向程序使用此例程来发送 oplock 中断响应或关闭上破坏 oplock 句柄，如果该文件不再使用。 需要刷新到服务器的字节范围锁传递给网络微型-重定向程序中<strong>LowIoContext.ParamsFor.Locks.LockList</strong> RX_CONTEXT 的成员。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549856" data-raw-source="[&lt;strong&gt;MRxComputeNewBufferingState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549856)"><strong>MRxComputeNewBufferingState</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向计算新的缓冲状态更改。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550687" data-raw-source="[&lt;strong&gt;MRxGetConnectionId&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550687)"><strong>MRxGetConnectionId</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向返回可用于处理多个会话的连接的连接 ID。 如果网络微型重定向支持连接 Id，则返回的连接 ID 追加到名称表中存储的连接结构。 RDBSS 认为形式的不透明 blob 的连接 ID，并查找具有给定名称的 net 名称表时没有按字节进行比较的连接 ID 的 blob。</p></td>
</tr>
</tbody>
</table>

 

 

 




