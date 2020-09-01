---
title: 队列状态和操作
description: 队列状态和操作
ms.assetid: 892f8f19-b94e-4950-af88-334c9a8b8c0d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ccd0504896538435e1691c34048a2378786fb7e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206283"
---
# <a name="queue-states-and-operations"></a>队列状态和操作





对于每个队列，网络适配器必须支持以下操作状态集：

<a href="" id="undefined"></a>Undefined  
队列未分配。 为了分配队列，过量驱动程序将发送 [OID \_ 接收 \_ 筛选器 \_ 分配 \_ 队列](./oid-receive-filter-allocate-queue.md) OID 请求。

<a href="" id="allocated"></a>已分配  
*分配*状态是队列的初始状态。 当队列处于分配状态时，过量驱动程序通常使用 [oid \_ 接收 \_ 筛选器 \_ 设置 \_ 筛选器](./oid-receive-filter-set-filter.md) OID 在队列上设置筛选器，或使用 [oid \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 \_ 完成](./oid-receive-filter-queue-allocation-complete.md) oid 请求完成队列分配。

<a href="" id="set"></a>字符集  
在 *设置* 状态下，队列至少分配了一个筛选器，但过量驱动程序尚未发送 [OID \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 \_ 完成](./oid-receive-filter-queue-allocation-complete.md) oid。

<a href="" id="running"></a>耗尽  
在 " *正在运行* " 状态下，队列设置了筛选器，队列分配已完成，微型端口适配器指示队列的接收数据包。

<a href="" id="paused"></a>悬停  
在 *暂停* 状态下，网络适配器不指示接收的网络数据。 在 [oid \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 \_ 完成](./oid-receive-filter-queue-allocation-complete.md) oid 请求之前，在队列中未设置任何筛选器，或者在队列中设置的所有筛选器都已清除并带有 [OID \_ 接收筛选器 \_ \_ 清除 \_ 筛选器](./oid-receive-filter-clear-filter.md) OID 请求。

<a href="" id="dma-stopped"></a>已停止 DMA  
在 *DMA 停止* 状态下，微型端口驱动程序收到 [OID \_ 接收 \_ 筛选器 \_ 释放 \_ 队列](./oid-receive-filter-free-queue.md) OID 请求。 当 DMA 停止并且驱动程序已将 "DMA 停止" 状态指示 (为 [**NDIS \_ 状态 \_ 接收 \_ 队列 \_ 状态**](./ndis-status-receive-queue-state.md) ") 时，驱动程序将进入" 正在释放 "状态。

<a href="" id="freeing"></a>减轻  
在 "正在 *释放* " 状态下，微型端口驱动程序完成停止发送队列和接收操作所需的操作，并释放关联的资源。 完成所有未完成的接收指示后，队列将被删除，并且不会定义队列。

在下表中，标题是队列状态。 主要事件在第一列中列出。 表中的其余条目指定事件发生在状态中之后队列所进入的下一个状态。 空白条目表示无效的事件/状态组合。

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
<th align="left">Undefined</th>
<th align="left">已分配</th>
<th align="left">设置</th>
<th align="left">正在运行</th>
<th align="left">已暂停</th>
<th align="left">停止 DMA</th>
<th align="left">减轻</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>OID_RECEIVE_FILTER_ALLOCATE_QUEUE 方法 (集) </p></td>
<td align="left"><p>已分配</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>OID_RECEIVE_FILTER_QUEUE_PARAMETERS) 请求 (查询</p></td>
<td align="left"></td>
<td align="left"><p>已分配</p></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"><p>已暂停</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>OID_RECEIVE_FILTER_QUEUE_PARAMETERS 设置请求</p></td>
<td align="left"></td>
<td align="left"><p>已分配</p></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"><p>已暂停</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>OID_RECEIVE_FILTER_SET_FILTER) 请求 (集</p></td>
<td align="left"></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>OID_RECEIVE_FILTER_CLEAR_FILTER 设置 (上一个筛选器的请求) </p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>已分配</p></td>
<td align="left"><p>已暂停</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>OID_RECEIVE_FILTER_CLEAR_FILTER 设置 (不是上一个筛选器的请求) </p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>查询请求 (OID_RECEIVE_FILTER_ENUM_FILTERS 方法) </p></td>
<td align="left"></td>
<td align="left"><p>已分配</p></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"><p>已暂停</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>OID_RECEIVE_FILTER_PARAMETERS) 请求 (查询</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>OID_RECEIVE_FILTER_QUEUE_ALLOCATION_COMPLETE) 请求 (集</p></td>
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
<td align="left"><p>DMA 已停止并 NDIS_STATUS_RECEIVE_QUEUE_STATE 状态指示已发送 (注意： DMA 可能已在 "已分配" 或 "已暂停" 状态下停止) </p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>减轻</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>所有接收指示都已完成，并且队列资源已释放</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>Undefined</p></td>
</tr>
</tbody>
</table>

 

**注意**   上表中列出的事件包括一些不会导致状态更改的辅助事件。 这些辅助事件包括在表中，用于指定这些事件的有效状态。

 

主要队列事件定义如下：

<a href="" id="oid-receive-filter-allocate-queue---method--set--request"></a>OID \_ 接收 \_ 筛选器 \_ 分配 \_ 队列-方法 (集) 请求  
过量驱动程序已分配队列。 有关分配队列的详细信息，请参阅 [分配和释放 VM 队列](allocating-and-freeing-vm-queues.md)。

<a href="" id="oid-receive-filter-set-filter---method--set--request"></a>OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器-方法 (设置) 请求  
过量驱动程序在队列上设置筛选器。 如果过量驱动程序未发送 [OID \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 \_ 完成](./oid-receive-filter-queue-allocation-complete.md) oid，则队列处于设置状态。 否则，队列将处于 "正在运行" 状态。 有关在队列上设置筛选器的详细信息，请参阅 [设置和清除 VMQ 筛选器](setting-and-clearing-vmq-filters.md)。

<a href="" id="oid-receive-filter-clear-filter---set-request"></a>OID \_ 接收 \_ 筛选器 \_ 清除 \_ 筛选器-设置请求  
过量驱动程序在队列中清除了筛选器。 如果在正在运行的队列中清除了最后一个筛选器，则可以停止 DMA;接收指示将停止，并且应清除收到的数据（如果有）。 有关清除队列筛选器的详细信息，请参阅 [设置和清除 VMQ 筛选器](setting-and-clearing-vmq-filters.md)。

<a href="" id="oid-receive-filter-queue-allocation-complete---method--set--request"></a>OID \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 \_ 完成-方法 (设置) 请求  
过量驱动程序已完成队列分配。 如果在队列上设置了筛选器，则它处于 "正在运行" 状态并且接收指示可以启动。 有关完成队列分配的详细信息，请参阅 [分配和释放 VM 队列](allocating-and-freeing-vm-queues.md)。

<a href="" id="receive-packet"></a>接收数据包  
微型端口驱动程序只能指示处于运行状态的队列的接收数据包。 有关指示队列接收的数据的详细信息，请参阅 [VMQ 发送和接收操作](vmq-send-and-receive-operations.md)。

<a href="" id="oid-receive-filter-free-queue-set-request-"></a>OID \_ 接收 \_ 筛选器 \_ 无 \_ 队列设置请求。  
过量驱动程序释放了队列。 驱动程序发出 DMA 停止状态指示 (，其中 [**NDIS \_ 状态 \_ 接收 \_ 队列 \_ 状态**](./ndis-status-receive-queue-state.md) 为) ，驱动程序进入释放状态。 当所有未完成的接收指示都完成并且队列资源被释放时，队列不确定。

 

