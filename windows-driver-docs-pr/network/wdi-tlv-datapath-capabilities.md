---
title: WDI_TLV_DATAPATH_CAPABILITIES
description: WDI_TLV_DATAPATH_CAPABILITIES 是包含数据路径功能 TLV。
ms.assetid: 7B545858-56A2-4655-91D5-37CA4EB61E1E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_DATAPATH_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5a86ae49462f2f44206155d7985f2bc3f9ef7537
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520624"
---
# <a name="wditlvdatapathcapabilities"></a>WDI\_TLV\_数据路径\_功能


WDI\_TLV\_数据路径\_功能是包含数据路径功能 TLV。

## <a name="tlv-type"></a>TLV 类型


0xB9

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>在任务栏的搜索框中键入</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926068" data-raw-source="[&lt;strong&gt;WDI_INTERCONNECT_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926068)"><strong>WDI_INTERCONNECT_TYPE</strong></a> (UINT32)</td>
<td>互连类型。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>对等节点的最大数目。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指定传输功能：目标优先级队列。
<p>有效值为 0 和 1。 如果设置为 0，WDI 将分为两类通过对等方和 TID Tx 帧，并利用完整的计划程序来选择要传输的 TX 队列。 建议，此设置为 false 除非目标是能够分类和对等方 TID 排入队列。 如果设置为 1，WDI 将分为两类通过对等方和 TID Tx 帧，并且仅提供队列在端口级别。 WDI 计划使用全局 DRR 囤积的端口队列。</p></td>
</tr>
<tr class="even">
<td>UINT16</td>
<td>指定传输功能：最大的散点图收集帧中的元素数。
<p>WDI 将合并帧根据需要，IHV 微型端口不会接收需要更多的散点图收集元素指定的此功能的帧。 为了获得最佳性能，建议，此功能设置为高于典型的帧合并需要内存副本。 如果此功能不大于最大帧大小除以页面大小，WDI 可能无法成功 coalesce 帧，并可能会断开。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指定传输功能：所需的显式发送完成标志。
<p>有效值为 0 和 1。 如果设置为 0，目标/谈论生成 TX 发送完成的所有框架。 如果设置为 1，目标/谈论生成 TX 发送完成指示仅对具有帧的元数据中设置此标志的帧。</p></td>
</tr>
<tr class="even">
<td>UINT16</td>
<td>指定传输功能：最小的有效帧大小。
<p>当出列帧，TxMgr 将处理帧小于此值为具有此值的有效大小。</p></td>
</tr>
<tr class="odd">
<td>UINT16</td>
<td>指定传输功能：帧大小粒度。
<p>此值等于每个框架的内存分配的粒度。 为了取消排队，TxMgr 帧将视为具有等于帧大小加上填充量最少的有效大小，以便有效大小是一个整数，此值的倍数。 此值必须设置为 2 的幂。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定传输功能：Rx Tx 转发。
<p>有效值为 0 和 1。 如果设置为 1，目标是能够转发接收的帧。</p></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定传输功能：0.5 Mbps 为单位的最大吞吐量。
<p>此值用于描述符和缓冲区的分配。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




