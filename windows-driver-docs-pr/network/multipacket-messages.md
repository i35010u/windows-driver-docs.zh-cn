---
title: 多数据包消息
description: 多数据包消息
ms.assetid: 58979799-4618-43b9-a6dc-0635f6ade9b3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f17eb1fe0b9a6a21a65ae425f317f4c8d24fdf9
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107000"
---
# <a name="multipacket-messages"></a>多数据包消息





在任一方向，都可以通过单个传输发送多个 [**远程 \_ NDIS \_ 数据包 \_ **](/previous-versions/ff570635(v=vs.85)) 消息消息。 Multipacket 消息通过连接多个 **远程 \_ NDIS \_ 数据包 \_ 消息** 元素形成。 此类传输的最大长度由[**远程 \_ NDIS \_ INITIALIZE \_ **](/previous-versions/ff570624(v=vs.85))消息和响应消息中传递的*MaxTransferSize*参数控制。 宿主还会将其捆绑的消息数限制为单一传输到设备在[**远程 \_ NDIS \_ INITIALIZE \_ CMPLT**](/previous-versions/ff570621(v=vs.85))响应消息中返回的*MaxPacketsPerMessage*参数。

与单数据包消息的不同之处在于，每个[**远程 \_ NDIS \_ 数据包 \_ **](/previous-versions/ff570635(v=vs.85))消息标头中的*MessageLength*字段都包含一些额外的填充字节。 这些填充字节将添加到除最后一个 **远程 \_ ndis \_ 数据包 \_ 消息** 以外的所有字符，以使后续远程 \_ ndis \_ 数据包 \_ 消息在适当的字节边界处启动。 对于从设备发送到主机的消息，这种填充应该会导致每个远程 \_ NDIS \_ 数据包消息从 \_ multipacket 消息开头开始的字节偏移量开始的字节偏移量。 当主机向设备发送 multipacket 消息时，它将遵循[**远程 \_ NDIS \_ INITIALIZE \_ CMPLT**](/previous-versions/ff570621(v=vs.85))响应消息中设备指定的*PacketAlignmentFactor* 。

请注意，不会在任何远程 NDIS 定义的字段中显式指定组合消息中的 multipacket 消息和 [**远程 \_ ndis \_ 数据包 \_ 消息**](/previous-versions/ff570635(v=vs.85)) 元素数的组合长度。 组合长度在特定于总线的传输机制中是隐式的，主机或设备必须遍历组合消息的 *MessageLength* 字段，以确定组合消息的数量。

下表是 multipacket 消息的一个示例，它由两个 \_ \_ \_ 从主机发送到设备的远程 NDIS 数据包消息组成。 在 [**远程 \_ NDIS \_ 初始化 \_ 消息**](/previous-versions/ff570624(v=vs.85)) 交换期间，设备请求的 *PacketAlignmentFactor* 为 3 (沿8字节边界) 对齐。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">偏移量</th>
<th align="left">大小</th>
<th align="left">字段</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>MessageType</p></td>
<td align="left"><p>0x1</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>MessageLength</p></td>
<td align="left"><p>72 (包括2个填充字节;请参阅下面的) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>数据偏移量</p></td>
<td align="left"><p>36</p></td>
</tr>
<tr class="even">
<td align="left"><p>12</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>DataLength</p></td>
<td align="left"><p>26</p></td>
</tr>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>OOBDataOffset</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>20</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>OOBDataLength</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>24</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>NumOOBDataElements</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>28</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>PerPacketInfoOffset</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>32</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>PerPacketInfoLength</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>36</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>VcHandle</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>40</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>44</p></td>
<td align="left"><p>26</p></td>
<td align="left"><p>负载 (数据) </p></td>
<td align="left"><p>某些网络数据的长度为26个字节</p></td>
</tr>
<tr class="odd">
<td align="left"><p>70</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>填充</p></td>
<td align="left"><p>不重要-未使用</p></td>
</tr>
<tr class="even">
<td align="left"><p>72</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>MessageType (第二个 <a href="/previous-versions/ff570635(v=vs.85)" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_PACKET_MSG&lt;/strong&gt;](/previous-versions/ff570635(v=vs.85))"><strong>REMOTE_NDIS_PACKET_MSG</strong></a> 的开头) </p></td>
<td align="left"><p>0x1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>76</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>MessageLength</p></td>
<td align="left"><p>60</p></td>
</tr>
<tr class="even">
<td align="left"><p>80</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>数据偏移量</p></td>
<td align="left"><p>36</p></td>
</tr>
<tr class="odd">
<td align="left"><p>84</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>DataLength</p></td>
<td align="left"><p>16</p></td>
</tr>
<tr class="even">
<td align="left"><p>88</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>OOBDataOffset</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>92</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>OOBDataLength</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>96</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>NumOOBDataElements</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>100</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>PerPacketInfoOffset</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>104</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>PerPacketInfoLength</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>108</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>VcHandle</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>112</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>116</p></td>
<td align="left"><p>16</p></td>
<td align="left"><p>负载 (数据) </p></td>
<td align="left"><p>长度为16个字节的网络数据</p></td>
</tr>
</tbody>
</table>

 

