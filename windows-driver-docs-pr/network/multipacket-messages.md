---
title: Multipacket 消息
description: Multipacket 消息
ms.assetid: 58979799-4618-43b9-a6dc-0635f6ade9b3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a301713e217006da4955015bb7345474b44dd00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522369"
---
# <a name="multipacket-messages"></a>Multipacket 消息





多个[**远程\_NDIS\_数据包\_MSG** ](https://msdn.microsoft.com/library/windows/hardware/ff570635)可能在单个传输，在任一方向发送消息。 通过串联多个构成 multipacket 消息**远程\_NDIS\_数据包\_MSG**元素。 此类传输的最大长度受到*MaxTransferSize*参数中传递[**远程\_NDIS\_初始化\_MSG**](https://msdn.microsoft.com/library/windows/hardware/ff570624)和响应消息。 主机还会限制它捆绑到单次转让到的消息数*MaxPacketsPerMessage*中的设备返回参数[**远程\_NDIS\_初始化\_CMPLT** ](https://msdn.microsoft.com/library/windows/hardware/ff570621)响应消息。

从单个数据包消息用例的区别在于*MessageLength*字段中每个[**远程\_NDIS\_数据包\_MSG** ](https://msdn.microsoft.com/library/windows/hardware/ff570635)标头包括某些附加的填充字节。 这些填充字节添加到所有除最后一个**远程\_NDIS\_数据包\_MSG**这样的后续远程\_NDIS\_数据包\_消息从相应字节边界处开始。 对于从设备发送到主机的消息，此填充应该产生的每个远程\_NDIS\_数据包\_消息开始的字节偏移量，它是从 multipacket 消息开始的 8 字节的倍数。 当主机将 multipacket 消息发送到设备时，将遵守*PacketAlignmentFactor*中的设备指定[**远程\_NDIS\_初始化\_CMPLT** ](https://msdn.microsoft.com/library/windows/hardware/ff570621)响应消息。

请注意，既不组合 multipacket 消息，也不数的长度[**远程\_NDIS\_数据包\_MSG** ](https://msdn.microsoft.com/library/windows/hardware/ff570635)给定组合消息中的元素显式任何远程 NDIS 中定义的字段。 合并后的长度是隐式总线特定于传输机制中，主机或设备必须遍历*MessageLength*组合的消息，以确定的数的字段结合使用的消息。

下表是由组成的两个远程 multipacket 消息的示例\_NDIS\_数据包\_消息数，从主机到设备发送。 期间[**远程\_NDIS\_初始化\_MSG** ](https://msdn.microsoft.com/library/windows/hardware/ff570624)交换设备请求*PacketAlignmentFactor*为 3 (沿一个 8 字节边界对齐）。

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
<th align="left">尺寸</th>
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
<td align="left"><p>72 （包括 2 个填充字节; 请参阅下文）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>DataOffset</p></td>
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
<td align="left"><p>有效负载 （数据）</p></td>
<td align="left"><p>某些网络 26 个字节的长度的数据</p></td>
</tr>
<tr class="odd">
<td align="left"><p>70</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>填充</p></td>
<td align="left"><p>此&#39;t 问题-未使用</p></td>
</tr>
<tr class="even">
<td align="left"><p>72</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>MessageType (开始的第二个<a href="https://msdn.microsoft.com/library/windows/hardware/ff570635" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_PACKET_MSG&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570635)"> <strong>REMOTE_NDIS_PACKET_MSG</strong></a>)</p></td>
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
<td align="left"><p>DataOffset</p></td>
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
<td align="left"><p>有效负载 （数据）</p></td>
<td align="left"><p>某些网络 16 个字节的长度的数据</p></td>
</tr>
</tbody>
</table>

 

 

 





