---
title: REMOTE_NDIS_PACKET_MSG
Description: REMOTE_NDIS_PACKET_MSG encapsulates NDIS data packets to form a single data message.
ms.assetid: cc4efe94-6e2c-4201-b251-10e76cf5a553
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb6a990e578f3e14634bac684270755004e2afaa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545785"
---
# <a name="remotendispacketmsg"></a>远程\_NDIS\_数据包\_消息


远程\_NDIS\_数据包\_MSG 封装 NDIS 数据包，以形成单个数据消息。

串联多个远程\_NDIS\_数据包\_MSG 元素窗体 multipacket 消息。 每个单个远程\_NDIS\_数据包\_MSG 组件构造如下所述。 从单个数据包消息的区别在于*MessageLength*字段中每个远程\_NDIS\_数据包\_消息标头包括某些附加的填充字节。 这些填充字节追加到最后一个远程除\_NDIS\_数据包\_消息，以便后续远程\_NDIS\_数据包\_MSG 相应字节边界处开始。 对于从设备发送到主机的消息，此填充应该产生的每个远程\_NDIS\_数据包\_消息开始的字节偏移量，它是从 multipacket 消息开始的 8 字节的倍数。 当主机将 multipacket 消息发送到设备时，将遵守*PacketAlignmentFactor*设备指定。

在远程\_NDIS\_数据包\_MSG 格式定义如下表中。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>偏移量</th>
<th>尺寸</th>
<th>字段</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>4</p></td>
<td><p>MessageType</p></td>
<td><p>指定发送消息的类型。 设置为 0x1。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>MessageLength</p></td>
<td><p>消息长度以字节为单位，包括附加的数据包数据、 OOB 数据、 每个数据包信息数据和内部和外部填充。</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>4</p></td>
<td><p>DataOffset</p></td>
<td><p>此消息的 DataOffset 字段开头字节数据的开始到指定的偏移量。 这是一个整数 4 的倍数。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>DataLength</p></td>
<td><p>此消息的数据内容中指定字节的数。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>OOBDataOffset</p></td>
<td><p>以字节为单位的开始处的第一个 OOB 数据记录指定的偏移量<em>DataOffset</em>此消息的字段。 设置为零，如果没有 OOB 数据。 否则，这就是一个整数 4 的倍数。</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>4</p></td>
<td><p>OOBDataLength</p></td>
<td><p>以字节为单位指定的 OOB 数据的总长度。</p></td>
</tr>
<tr class="odd">
<td><p>24</p></td>
<td><p>4</p></td>
<td><p>NumOOBDataElements</p></td>
<td><p>此消息中指定 OOB 记录的数。</p></td>
</tr>
<tr class="even">
<td><p>28</p></td>
<td><p>4</p></td>
<td><p>PerPacketInfoOffset</p></td>
<td><p>以字节为单位指定从开头的偏移量<em>DataOffset</em>字段的每个数据包信息数据的第一个记录开始将 REMOTE_NDIS_PACKET_MSG 数据消息中。 如果没有每个数据包数据，则设置为零。 否则，这就是一个整数 4 的倍数。</p></td>
</tr>
<tr class="odd">
<td><p>32</p></td>
<td><p>4</p></td>
<td><p>PerPacketInfoLength</p></td>
<td><p>以字节为单位指定此消息中包含的每个数据包信息的总长度。</p></td>
</tr>
<tr class="even">
<td><p>36</p></td>
<td><p>4</p></td>
<td><p>VcHandle</p></td>
<td><p>保留的面向连接的设备。 设置为零。</p></td>
</tr>
<tr class="odd">
<td><p>40</p></td>
<td><p>4</p></td>
<td><p>保留</p></td>
<td><p>保留。 设置为零。</p></td>
</tr>
</tbody>
</table>

 

下表中指示的单个 OOB 数据记录的格式。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>偏移量</th>
<th>尺寸</th>
<th>字段</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>4</p></td>
<td><p>尺寸</p></td>
<td><p>以字节为单位的此 OOB 标头和追加 OOB 数据和填充的长度。 这是一个整数 4 的倍数。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>在任务栏的搜索框中键入</p></td>
<td><p>未定义适用于 802.3 设备。</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>4</p></td>
<td><p>ClassInformationOffset</p></td>
<td><p>字节偏移量从一开始此 OOB 数据记录到 OOB 数据的起始位置。</p></td>
</tr>
<tr class="even">
<td><p>(N)</p></td>
<td><p>...</p></td>
<td><p>OOB 数据</p></td>
<td><p>OOB 数据;有关详细信息，请参阅 Microsoft Windows 驱动程序开发工具包 (DDK) 文档。</p></td>
</tr>
</tbody>
</table>

 

**请注意**   (N) 等于的值*ClassInformationOffset*。

 

下表定义的每个数据包信息数据记录的格式。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>偏移量</th>
<th>尺寸</th>
<th>字段</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>4</p></td>
<td><p>尺寸</p></td>
<td><p>以字节为单位的此每个数据包标头和追加的每个数据包数据和填充的长度。 此值是一个整数 4 的倍数。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>在任务栏的搜索框中键入</p></td>
<td><p>设置为一个合法值 NDIS_PER_PACKET_INFO_FROM_PACKET，在 Windows 2000 驱动程序开发工具包 (DDK) 所述。</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>4</p></td>
<td><p>PerPacketInformationOffset</p></td>
<td><p>字节偏移量从一开始此每个数据包的信息的数据记录到每个数据包信息数据的开头。</p></td>
</tr>
<tr class="even">
<td><p>(N)</p></td>
<td><p>...</p></td>
<td><p>每个数据包数据</p></td>
<td><p>每个数据包数据;有关详细信息，请参阅 Windows 2000 DDK 文档。</p></td>
</tr>
</tbody>
</table>

 

**请注意**   (N) 等于的值*PerPacketInformationOffset*。

 

<a name="remarks"></a>备注
-------

每个远程\_NDIS\_数据包\_消息可能包含一个或多个 OOB 数据记录。 *NumOOBDataElements*指示此消息中的 OOB 数据记录数。 OOB 数据记录必须出现在序列中。 *OOBDataLength*字段指示整个 OOB 数据块的长度以字节为单位。 *OOBDataOffset*字段指示从开始处的字节偏移量*DataOffset*字段到 OOB 数据块的开头。 OOB 包的数据有关的详细信息，请参阅 Windows 2000 DDK 中的 NDIS 规范。

如果多个 OOB 数据块附加到远程\_NDIS\_数据包\_MSG 消息，每个后续的 OOB 数据记录必须紧跟以前 OOB 记录的数据。

当前为 802.3 设备定义没有 OOB 信息。

每个远程\_NDIS\_数据包\_消息可能包含一个或多个每个数据包信息数据记录。 每个数据包信息用于传达数据包元数据，例如 TCP 校验和。 *PerPacketInfoOffset*字段指示从开始处的字节偏移量*DataOffset*字段的每个数据包信息数据记录的开头。 *OOBDataLength*字段指示每个数据包信息数据记录的字节长度。 有关每个数据包信息数据的详细信息，请参阅 Windows 2000 DDK。

如果有多个每个数据包信息数据块，每个后续的每个数据包信息数据记录必须紧跟以前每个数据包的信息记录的数据。

远程 NDIS 设备必须发送和接收通过 NDIS 数据包数据。 设备使用的总线确定这些数据包如何从主机到设备和设备传递到主机。 可能是共享的内存，它或在 USB、 Isoch 和大容量的情况下通过管道传递。 NDIS 数据包还可能包含带外 (OOB) 数据，以及放在网络上的数据。

远程 NDIS 设备将传输封装与的 NDIS 数据包**远程\_NDIS\_数据包\_MSG**跨整个数据通道。 无连接 （例如，802.3) 和面向连接的网站 （如 ATM) 设备使用同一数据包消息结构，以便处理数据包的通用代码。 每个**远程\_NDIS\_数据包\_MSG**消息包含有关单个网络数据单元 （此类 s 以太网 802.3 帧） 的信息。

有关带外数据包数据或每个数据包信息数据的详细信息，请参阅 Windows 2000 DDK NDIS 部分。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Microsoft Windows XP 和更高版本的 Windows 操作系统中可用。 也可在 Windows 2000 中作为可再发行组件的二进制文件。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Rndis.h （包括 Rndis.h）</td>
</tr>
</tbody>
</table>

 

 




