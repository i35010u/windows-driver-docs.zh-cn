---
title: 杂项网络微型重定向程序例程
description: 杂项网络微型重定向程序例程
ms.assetid: bad5847c-8ac5-4e63-a0a5-3bbf13424928
keywords:
- 小型重定向程序 WDK，其他例程
- 连接 Id WDK 网络重定向器
- 缓冲状态 WDK 网络重定向器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6a1f917eb16b016cf8839b5989ba50dbf3728e3
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067388"
---
# <a name="miscellaneous-network-mini-redirector-routines"></a>杂项网络微型重定向程序例程


网络小型重定向程序实现的一些其他例程处理缓冲状态管理和连接 Id。 缓冲状态管理例程可由网络小型重定向器用于处理在重定向程序和服务器中实现的各种缓冲方案，并传达缓冲状态中的任何更改。 例如，SMB 重定向程序使用 [**MRxCompleteBufferingStateChangeRequest**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_change_buffering_state_calldown) 例程将 oplock 中断发送到服务器的机制中。

连接 Id 可用于多路复用多个连接。 网络小型重定向器不需要支持连接 Id，因此 [**MRxGetConnectionId**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_get_connection_id) 是可选的。

下表列出了可由网络小型重定向程序为其他操作实现的例程。

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
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_change_buffering_state_calldown" data-raw-source="[&lt;strong&gt;MRxCompleteBufferingStateChangeRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_change_buffering_state_calldown)"><strong>MRxCompleteBufferingStateChangeRequest</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，通知网络小型重定向器已完成缓冲状态更改请求。 例如，当文件不再使用时，SMB 重定向程序使用此例程来发送 oplock 中断响应或关闭 oplock 中断的句柄。 需要在服务器上刷新的字节范围锁会传递到 RX_CONTEXT 的 <strong>LockList</strong> 成员中的网络微重定向程序。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_compute_new_buffering_state" data-raw-source="[&lt;strong&gt;MRxComputeNewBufferingState&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_compute_new_buffering_state)"><strong>MRxComputeNewBufferingState</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络最小化重定向器计算新的缓冲状态更改。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_get_connection_id" data-raw-source="[&lt;strong&gt;MRxGetConnectionId&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_get_connection_id)"><strong>MRxGetConnectionId</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序为连接返回一个连接 ID，该 ID 可用于处理多个会话。 如果网络微型重定向程序支持连接 Id，则返回的连接 ID 将追加到存储在名称表中的连接结构。 RDBSS 将连接 ID 视为不透明的 blob，并在查找具有给定名称的网络名称表时对连接 ID blob 进行逐字节的比较。</p></td>
</tr>
</tbody>
</table>

 

 

