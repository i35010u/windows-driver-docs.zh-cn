---
title: 无连接 (802.3) 初始化序列示例
description: 无连接 (802.3) 初始化序列示例
ms.assetid: 9625f717-81c3-460b-83e8-c7a86aa85f36
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e0320207ba01037fbb37a84a51f7e99c86c348d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391666"
---
# <a name="example-connectionless-8023-initialization-sequence"></a>无连接 (802.3) 初始化序列示例





本部分介绍了设备可以预期在启动时作为远程 NDIS 无连接设备时的事件的常规顺序。 远程 NDIS 的基本操作是相同的而不考虑基础总线，因为需要总线枚举和启动进程已离职示例。

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
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570624" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_INITIALIZE_MSG&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570624)"><strong>REMOTE_NDIS_INITIALIZE_MSG</strong></a></p></td>
<td align="left"></td>
<td align="left"><p>主机将远程 NDIS 初始化消息发送到设备。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570621" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_INITIALIZE_CMPLT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570621)"><strong>REMOTE_NDIS_INITIALIZE_CMPLT</strong></a></p></td>
<td align="left"><p>具有初始化完整的消息的设备响应。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>接收。 初始化成功</p></td>
<td align="left"></td>
<td align="left"><p>主机启动接受传入的数据通道上的数据。 (示例： 启动 USB 上的在管道中执行读取操作上)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570641" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_QUERY_MSG&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570641)"><strong>REMOTE_NDIS_QUERY_MSG</strong></a></p>
<p>和</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570654" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_SET_MSG&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570654)"><strong>REMOTE_NDIS_SET_MSG</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570638" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_QUERY_CMPLT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570638)"><strong>REMOTE_NDIS_QUERY_CMPLT</strong></a></p>
<p>或者</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570651" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_SET_CMPLT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570651)"><strong>REMOTE_NDIS_SET_CMPLT</strong></a></p></td>
<td align="left"><p>主机启动一的系列集和查询来确定设备的状态和设置初始参数。 设备响应适当地使用正确完成消息。 可以查询以下 NDIS Oid:<a href="https://msdn.microsoft.com/library/windows/hardware/ff569069" data-raw-source="[OID_802_3_CURRENT_ADDRESS](https://msdn.microsoft.com/library/windows/hardware/ff569069)">OID_802_3_CURRENT_ADDRESS</a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff569072" data-raw-source="[OID_802_3_MAXIMUM_LIST_SIZE](https://msdn.microsoft.com/library/windows/hardware/ff569072)">OID_802_3_MAXIMUM_LIST_SIZE</a>，依次类推。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570654" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_SET_MSG&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570654)"><strong>REMOTE_NDIS_SET_MSG</strong></a></p></td>
<td align="left"></td>
<td align="left"><p>承载发送<a href="https://msdn.microsoft.com/library/windows/hardware/ff569575" data-raw-source="[OID_GEN_CURRENT_PACKET_FILTER](https://msdn.microsoft.com/library/windows/hardware/ff569575)">OID_GEN_CURRENT_PACKET_FILTER</a> OID 到设备的非零值的筛选器值。 此时设备应开始在传入的数据通道上发送数据包。 主机还会在传出的数据通道上发送数据包。</p></td>
</tr>
</tbody>
</table>

 

 

 





