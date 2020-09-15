---
title: 无连接 (802.3) 初始化序列示例
description: 无连接 (802.3) 初始化序列示例
ms.assetid: 9625f717-81c3-460b-83e8-c7a86aa85f36
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9c2d7c98672d59c95af8743320c80955dea2472
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104276"
---
# <a name="example-connectionless-8023-initialization-sequence"></a>无连接 (802.3) 初始化序列示例





本部分描述了设备在启动时可以预期为远程 NDIS 无连接设备的一般事件顺序。 由于远程 NDIS 的基本操作是相同的，因此无论底层总线是什么，都需要在示例中省略总线枚举和启动进程。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主机</th>
<th align="left">设备</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/previous-versions/ff570624(v=vs.85)" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_INITIALIZE_MSG&lt;/strong&gt;](/previous-versions/ff570624(v=vs.85))"><strong>REMOTE_NDIS_INITIALIZE_MSG</strong></a></p></td>
<td align="left"></td>
<td align="left"><p>主机向设备发送远程 NDIS 初始化消息。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p><a href="/previous-versions/ff570621(v=vs.85)" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_INITIALIZE_CMPLT&lt;/strong&gt;](/previous-versions/ff570621(v=vs.85))"><strong>REMOTE_NDIS_INITIALIZE_CMPLT</strong></a></p></td>
<td align="left"><p>具有初始化完成消息的设备响应。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>接收。 初始化成功</p></td>
<td align="left"></td>
<td align="left"><p>主机开始接受传入数据通道上的数据。  (示例： USB 上的开始在管道) 中进行读取。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/previous-versions/ff570641(v=vs.85)" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_QUERY_MSG&lt;/strong&gt;](/previous-versions/ff570641(v=vs.85))"><strong>REMOTE_NDIS_QUERY_MSG</strong></a></p>
<p>AND</p>
<p><a href="/previous-versions/ff570654(v=vs.85)" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_SET_MSG&lt;/strong&gt;](/previous-versions/ff570654(v=vs.85))"><strong>REMOTE_NDIS_SET_MSG</strong></a></p></td>
<td align="left"><p><a href="/previous-versions/ff570638(v=vs.85)" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_QUERY_CMPLT&lt;/strong&gt;](/previous-versions/ff570638(v=vs.85))"><strong>REMOTE_NDIS_QUERY_CMPLT</strong></a></p>
<p>OR</p>
<p><a href="/previous-versions/ff570651(v=vs.85)" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_SET_CMPLT&lt;/strong&gt;](/previous-versions/ff570651(v=vs.85))"><strong>REMOTE_NDIS_SET_CMPLT</strong></a></p></td>
<td align="left"><p>主机启动一系列集和查询，确定设备的状态和设置初始参数。 设备响应正确的完整消息。 可以查询以下 NDIS Oid： <a href="/windows-hardware/drivers/network/oid-802-3-current-address" data-raw-source="[OID_802_3_CURRENT_ADDRESS](./oid-802-3-current-address.md)">OID_802_3_CURRENT_ADDRESS</a>、 <a href="/windows-hardware/drivers/network/oid-802-3-maximum-list-size" data-raw-source="[OID_802_3_MAXIMUM_LIST_SIZE](./oid-802-3-maximum-list-size.md)">OID_802_3_MAXIMUM_LIST_SIZE</a>等。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/previous-versions/ff570654(v=vs.85)" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_SET_MSG&lt;/strong&gt;](/previous-versions/ff570654(v=vs.85))"><strong>REMOTE_NDIS_SET_MSG</strong></a></p></td>
<td align="left"></td>
<td align="left"><p>主机将具有非零筛选器值的 <a href="/windows-hardware/drivers/network/oid-gen-current-packet-filter" data-raw-source="[OID_GEN_CURRENT_PACKET_FILTER](./oid-gen-current-packet-filter.md)">OID_GEN_CURRENT_PACKET_FILTER</a> OID 发送到设备。 此时，设备应该开始发送传入数据通道上的数据包。 主机还会开始发送传出数据通道上的数据包。</p></td>
</tr>
</tbody>
</table>

 

