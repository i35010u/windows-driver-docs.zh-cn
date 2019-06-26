---
title: 队列状态和操作
description: 队列状态和操作
ms.assetid: 892f8f19-b94e-4950-af88-334c9a8b8c0d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 319895ff2ab273ff66d185e922d2d9355183a75c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382194"
---
# <a name="queue-states-and-operations"></a>队列状态和操作





对于每个队列，网络适配器必须支持以下一组操作状态：

<a href="" id="undefined"></a>未定义  
不会分配给队列。 若要分配一个队列，基础驱动程序将发送[OID\_接收\_筛选器\_分配\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)OID 请求。

<a href="" id="allocated"></a>分配  
*已分配*状态是队列的初始状态。 已分配状态队列时，基础驱动程序通常设置为筛选器上的队列[OID\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)OID 或完成队列与分配[OID\_接收\_筛选器\_队列\_分配\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)OID 请求。

<a href="" id="set"></a>设置  
在中*设置*状态时，队列都具有分配至少一个筛选器，但是基础驱动程序的发送了不[OID\_接收\_筛选器\_队列\_分配\_完整](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)OID。

<a href="" id="running"></a>运行  
在中*运行*状态中时，队列具有筛选器设置，队列分配已完成和微型端口适配器指示接收数据包的队列。

<a href="" id="paused"></a>已暂停  
在中*已暂停*状态，则网络适配器并不表示队列的接收的网络数据。 要么已设置队列之前的任何筛选器[OID\_接收\_筛选器\_队列\_分配\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)OID 请求或所有筛选器的已队列上的设置与已清除[OID\_接收\_筛选器\_清除\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)OID 请求。

<a href="" id="dma-stopped"></a>DMA 已停止  
在中*DMA 停止*状态时，收到的微型端口驱动程序[OID\_接收\_筛选器\_免费\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)OID 请求。 当停止 DMA 和驱动程序已发出的 DMA 停止状态指示 (与[ **NDIS\_状态\_接收\_队列\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-queue-state))，该驱动程序将进入释放状态。

<a href="" id="freeing"></a>释放  
在中*释放*状态时，微型端口驱动程序中完成操作所需停止发送和接收操作对于队列，并释放关联的资源。 所有未处理的接收后指示已完成、 删除队列和队列是未定义。

下表中的标题是队列状态。 第一列中列出了主要的事件。 表中的条目的其余部分指定下一个状态队列进入后处于状态发生的事件。 为空白条目表示无效的事件状态组合。

<table>
<colgroup>
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">事件 \ 状态</th>
<th align="left">未定义</th>
<th align="left">分配</th>
<th align="left">设置</th>
<th align="left">正在运行</th>
<th align="left">已暂停</th>
<th align="left">停止 DMA</th>
<th align="left">释放</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>OID_RECEIVE_FILTER_ALLOCATE_QUEUE-方法 (set)</p></td>
<td align="left"><p>分配</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>OID_RECEIVE_FILTER_QUEUE_PARAMETERS-方法 （查询） 请求</p></td>
<td align="left"></td>
<td align="left"><p>分配</p></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"><p>已暂停</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>OID_RECEIVE_FILTER_QUEUE_PARAMETERS 的集请求</p></td>
<td align="left"></td>
<td align="left"><p>分配</p></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"><p>已暂停</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>OID_RECEIVE_FILTER_SET_FILTER-方法 (set) 请求</p></td>
<td align="left"></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>OID_RECEIVE_FILTER_CLEAR_FILTER 的集请求 （最后一个筛选器）</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>分配</p></td>
<td align="left"><p>已暂停</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>OID_RECEIVE_FILTER_CLEAR_FILTER 的集请求 （不最后一个筛选器）</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>OID_RECEIVE_FILTER_ENUM_FILTERS-方法 （查询请求）</p></td>
<td align="left"></td>
<td align="left"><p>分配</p></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"><p>已暂停</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>OID_RECEIVE_FILTER_PARAMETERS-方法 （查询） 请求</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>OID_RECEIVE_FILTER_QUEUE_ALLOCATION_COMPLETE-方法 (set) 请求</p></td>
<td align="left"></td>
<td align="left"><p>已暂停</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>接收数据包</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>正在运行</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>OID_RECEIVE_FILTER_FREE_QUEUE 设置请求</p></td>
<td align="left"></td>
<td align="left"><p>停止 DMA</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>停止 DMA</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>停止 DMA 和 NDIS_STATUS_RECEIVE_QUEUE_STATE 状态指示已发送 (注意：DMA 中已分配可能已停止或暂停状态）</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>释放</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>所有接收指示释放是完整和队列资源</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>未定义</p></td>
</tr>
</tbody>
</table>

 

**请注意**  上表中列出的事件包括状态更改不会产生一些辅助事件。 若要指定这些事件是有效的状态表中包含这些辅助的事件。

 

主队列事件定义，如下所示：

<a href="" id="oid-receive-filter-allocate-queue---method--set--request"></a>OID\_接收\_筛选器\_分配\_队列的方法 (set) 请求  
基础驱动程序分配一个队列。 有关分配队列的详细信息，请参阅[Allocating 和释放虚拟机队列](allocating-and-freeing-vm-queues.md)。

<a href="" id="oid-receive-filter-set-filter---method--set--request"></a>OID\_接收\_筛选器\_设置\_筛选器-方法 (set) 请求  
基础驱动程序在队列上设置筛选器。 如果基础驱动程序内未发送[OID\_接收\_筛选器\_队列\_分配\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)OID，队列是在设置状态。 否则，队列是处于运行状态。 在队列上设置筛选器的详细信息，请参阅[设置和清除 VMQ 筛选器](setting-and-clearing-vmq-filters.md)。

<a href="" id="oid-receive-filter-clear-filter---set-request"></a>OID\_接收\_筛选器\_清除\_筛选器-set 请求  
基础驱动程序清除队列中的筛选器。 如果正在运行的队列已清除的最后一个筛选器，可以停止 DMA;接收指示都将停止且应接收数据的清除队列，如果有的话。 有关清除队列的筛选器的详细信息，请参阅[设置和清除 VMQ 筛选器](setting-and-clearing-vmq-filters.md)。

<a href="" id="oid-receive-filter-queue-allocation-complete---method--set--request"></a>OID\_接收\_筛选器\_队列\_分配\_完成的方法 (set) 请求  
基础驱动程序完成队列分配。 如果没有设置队列的筛选器，将在运行状态，并接收指示可以启动。 有关如何完成队列分配的详细信息，请参阅[Allocating 和释放虚拟机队列](allocating-and-freeing-vm-queues.md)。

<a href="" id="receive-packet"></a>接收数据包  
微型端口驱动程序可以仅指示接收队列处于运行状态的数据包。 对于队列，该值指示接收到的数据有关的详细信息，请参阅[VMQ 发送和接收操作](vmq-send-and-receive-operations.md)。

<a href="" id="oid-receive-filter-free-queue-set-request-"></a>OID\_接收\_筛选器\_免费\_设置队列的请求。  
基础驱动程序释放队列。 驱动程序将发出 DMA 停止状态指示 (与[ **NDIS\_状态\_接收\_队列\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-queue-state))，该驱动程序将进入释放状态。 当所有未处理的接收指示已完成和队列资源也将释放，队列是未定义。

 

 





