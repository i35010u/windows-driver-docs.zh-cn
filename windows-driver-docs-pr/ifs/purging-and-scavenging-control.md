---
title: 清除和清理控件
description: 清除和清理控件
ms.assetid: 103b05e6-333a-441a-a4f8-784ae43df59e
keywords:
- RDBSS WDK 文件系统中，清除和清理结构
- 重定向驱动器缓冲子系统 WDK 文件系统中，清除和清理结构
- 清除 WDK 网络重定向程序
- 清理 WDK 网络重定向程序
- FOBX 结构
- 清理 FOBX 结构 WDK 网络重定向程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 094cf479eaccb91396a07df19ac4be4d7122389a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385144"
---
# <a name="purging-and-scavenging-control"></a>清除和清理控件


## <span id="ddk_purging_and_scavenging_control_if"></span><span id="DDK_PURGING_AND_SCAVENGING_CONTROL_IF"></span>


RDBSS 提供例程来清除和在不再需要时清理 FOBX 结构的数。

在清理，没有更多用户句柄与文件对象相关联。 在这种情况下，关闭并清理之间的时间窗口根据由内存管理器和缓存管理器维护的其他引用来确定。 RDBSS 使用清理并清除不需要的 FOBX 和其他结构的单独线程运行的清理程序进程。

目前，清理已实现为 SRV\_调用时，NET\_根和 V\_NET\_根结构。 FCB 清理是单独处理。 FOBX 可以并始终应以同步方式完成。 将需要清理终止可能启用的唯一数据结构是 SRV\_打开结构。

清理程序进程是在 RDBSS 中当前实现不会使用任何系统资源之前需要进行清理终结。 第一项以将标记为清理终止会导致为清理程序要发布的计时器请求。 在当前实现中，计时器请求都以单步计时器请求发布。 这意味着没有任何保证将在其中完成条目的时间间隔。 清理程序激活机制是在后面的阶段进行细微调整的潜在候选。

RDBSS 清除和清理例程包括：

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxpurgeallfobxs" data-raw-source="[&lt;strong&gt;RxPurgeAllFobxs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxpurgeallfobxs)"><strong>RxPurgeAllFobxs</strong></a></p></td>
<td align="left"><p>此例程会清除所有与网络微型重定向相关联的 FOBX 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scavengr/nf-scavengr-rxpurgerelatedfobxs" data-raw-source="[&lt;strong&gt;RxPurgeRelatedFobxs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scavengr/nf-scavengr-rxpurgerelatedfobxs)"><strong>RxPurgeRelatedFobxs</strong></a></p></td>
<td align="left"><p>此例程会清除所有与 NET_ROOT 结构相关联的 FOBX 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxscavengeallfobxs" data-raw-source="[&lt;strong&gt;RxScavengeAllFobxs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxscavengeallfobxs)"><strong>RxScavengeAllFobxs</strong></a></p></td>
<td align="left"><p>此例程清理所有与给定的网络微型重定向设备对象相关联的 FOBX 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scavengr/nf-scavengr-rxscavengefobxsfornetroot" data-raw-source="[&lt;strong&gt;RxScavengeFobxsForNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scavengr/nf-scavengr-rxscavengefobxsfornetroot)"><strong>RxScavengeFobxsForNetRoot</strong></a></p></td>
<td align="left"><p>此例程清理所有与给定 NET_ROOT 结构相关联的 FOBX 结构。</p></td>
</tr>
</tbody>
</table>

 

 

 




