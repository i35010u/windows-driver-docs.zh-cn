---
title: 清除和清理控件
description: 清除和清理控件
ms.assetid: 103b05e6-333a-441a-a4f8-784ae43df59e
keywords:
- RDBSS WDK 文件系统，清除和清理结构
- 重定向的驱动器缓冲子系统 WDK 文件系统、清除和清理结构
- 清除 WDK 网络重定向器
- 清理 WDK 网络重定向器
- FOBX 结构
- 清理 FOBX 结构 WDK 网络重定向器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a6e000438e8ba80b7055b44994bd60e78aeda4c
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063258"
---
# <a name="purging-and-scavenging-control"></a>清除和清理控件


## <span id="ddk_purging_and_scavenging_control_if"></span><span id="DDK_PURGING_AND_SCAVENGING_CONTROL_IF"></span>


RDBSS 提供了许多例程，用于在不再需要 FOBX 结构时清除和清除这些结构。

清除时，没有与该文件对象关联的其他用户句柄。 在这种情况下，"关闭" 和 "清理" 之间的时间范围由内存管理器和缓存管理器维护的其他引用决定。 RDBSS 使用在单独的线程上运行的 scavenger 进程来清理和清除不需要的 FOBX 和其他结构。

目前，已实现 SRV \_ 调用、net \_ root 和 net \_ \_ root 结构的清理。 FCB 清理单独处理。 FOBX 可以并且应始终同步完成。 只有启用了 SRV 开放式结构，才有可能启用的唯一数据结构 \_ 。

在 RDBSS 中实现的 scavenger 过程目前不会消耗任何系统资源，除非需要进行清理。 第一项将标记为清理的终止将导致为清除程序发布计时器请求。 在当前实现中，计时器请求以一次拍摄计时器请求的形式发布。 这意味着，不能保证在时间间隔内完成项的时间间隔。 清除程序激活机制是一种可能的候选项，用于在以后进行微调。

RDBSS 清除和清理例程包括：

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxpurgeallfobxs" data-raw-source="[&lt;strong&gt;RxPurgeAllFobxs&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxpurgeallfobxs)"><strong>RxPurgeAllFobxs</strong></a></p></td>
<td align="left"><p>此例程将清除与网络小型重定向程序关联的所有 FOBX 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/scavengr/nf-scavengr-rxpurgerelatedfobxs" data-raw-source="[&lt;strong&gt;RxPurgeRelatedFobxs&lt;/strong&gt;](/windows-hardware/drivers/ddi/scavengr/nf-scavengr-rxpurgerelatedfobxs)"><strong>RxPurgeRelatedFobxs</strong></a></p></td>
<td align="left"><p>此例程将清除与 NET_ROOT 结构关联的所有 FOBX 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxscavengeallfobxs" data-raw-source="[&lt;strong&gt;RxScavengeAllFobxs&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxscavengeallfobxs)"><strong>RxScavengeAllFobxs</strong></a></p></td>
<td align="left"><p>此例程将清除与给定的网络微重定向程序设备对象相关联的所有 FOBX 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/scavengr/nf-scavengr-rxscavengefobxsfornetroot" data-raw-source="[&lt;strong&gt;RxScavengeFobxsForNetRoot&lt;/strong&gt;](/windows-hardware/drivers/ddi/scavengr/nf-scavengr-rxscavengefobxsfornetroot)"><strong>RxScavengeFobxsForNetRoot</strong></a></p></td>
<td align="left"><p>此例程将清除与给定 NET_ROOT 结构相关联的所有 FOBX 结构。</p></td>
</tr>
</tbody>
</table>

 

 

