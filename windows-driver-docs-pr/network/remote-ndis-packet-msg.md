---
title: REMOTE_NDIS_PACKET_MSG
description: REMOTE_NDIS_PACKET_MSG 封装 NDIS 数据包以构成单个数据消息。
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01e728339898e20f0fbd3aefe5291fc8da06d2b9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829173"
---
# <a name="remote_ndis_packet_msg"></a>远程 \_ NDIS \_ 数据包 \_ 消息


远程 \_ NDIS \_ 数据包 \_ 消息封装 NDIS 数据包，以形成单个数据消息。

串联多个远程 \_ NDIS \_ 数据包 \_ 消息元素将形成一个 multipacket 消息。 \_按如下所述构造每个单独的远程 NDIS \_ 数据包 \_ 消息组件。 与单数据包消息不同的是，每个远程 NDIS 数据包消息标头中的 *MessageLength* 字段都 \_ \_ \_ 包含一些额外的填充字节。 这些填充字节将追加到除最后一个远程 ndis 数据包消息以外的所有字符， \_ \_ \_ 以使后续远程 \_ ndis \_ 数据包 \_ 消息在适当的字节边界处启动。 对于从设备发送到主机的消息，这种填充应该会导致每个远程 \_ NDIS \_ 数据包消息从 \_ multipacket 消息开头开始的字节偏移量开始的字节偏移量。 当主机向设备发送 multipacket 消息时，它将遵循设备指定的 *PacketAlignmentFactor* 。

远程 \_ NDIS \_ 数据包 \_ 消息格式在下表中定义。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Offset</th>
<th>大小</th>
<th>字段</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>4</p></td>
<td><p>MessageType</p></td>
<td><p>指定要发送的消息的类型。 设置为0x1。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>MessageLength</p></td>
<td><p>消息长度（以字节为单位），包括追加的数据包数据、OOB 数据、每个数据包的信息数据以及内部和外部空白。</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>4</p></td>
<td><p>数据偏移量</p></td>
<td><p>指定从此消息的数据偏移量字段开头到数据开始处的偏移量（以字节为单位）。 这是4的整数倍。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>DataLength</p></td>
<td><p>指定此消息的数据内容中的字节数。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>OOBDataOffset</p></td>
<td><p>指定从此消息的 <em>数据偏移量</em> 字段开头开始的第一个 OOB 数据记录的偏移量（以字节为单位）。 如果没有 OOB 数据，则设置为零。 否则，这是4的整数倍。</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>4</p></td>
<td><p>OOBDataLength</p></td>
<td><p>指定 OOB 数据的总长度（以字节为单位）。</p></td>
</tr>
<tr class="odd">
<td><p>24</p></td>
<td><p>4</p></td>
<td><p>NumOOBDataElements</p></td>
<td><p>指定此消息中的 OOB 记录数。</p></td>
</tr>
<tr class="even">
<td><p>28</p></td>
<td><p>4</p></td>
<td><p>PerPacketInfoOffset</p></td>
<td><p>指定从 REMOTE_NDIS_PACKET_MSG 数据消息中的 <em>数据偏移量</em> 字段开始到第一个每个数据包信息数据记录开始的偏移量（以字节为单位）。 如果没有每个数据包数据，则设置为零。 否则，这是4的整数倍。</p></td>
</tr>
<tr class="odd">
<td><p>32</p></td>
<td><p>4</p></td>
<td><p>PerPacketInfoLength</p></td>
<td><p>指定此消息中包含的每个数据包的总长度（以字节为单位）。</p></td>
</tr>
<tr class="even">
<td><p>36</p></td>
<td><p>4</p></td>
<td><p>VcHandle</p></td>
<td><p>为面向连接的设备保留。 设置为零。</p></td>
</tr>
<tr class="odd">
<td><p>40</p></td>
<td><p>4</p></td>
<td><p>预留</p></td>
<td><p>保留。 设置为零。</p></td>
</tr>
</tbody>
</table>

 

下表指示了单个 OOB 数据记录的格式。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Offset</th>
<th>大小</th>
<th>字段</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>4</p></td>
<td><p>大小</p></td>
<td><p>此 OOB 标头的长度（以字节为单位），并追加了 OOB 数据和填充。 这是4的整数倍。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>类型</p></td>
<td><p>无为802.3 设备定义。</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>4</p></td>
<td><p>ClassInformationOffset</p></td>
<td><p>从此 OOB 数据记录的开始到 OOB 数据开头的字节偏移量。</p></td>
</tr>
<tr class="even">
<td><p> (N) </p></td>
<td><p>...</p></td>
<td><p>OOB 数据</p></td>
<td><p>OOB 数据;有关详细信息，请参阅 Microsoft Windows 驱动程序开发工具包 (DDK) 文档。</p></td>
</tr>
</tbody>
</table>

 

**注意**  
 (N) 等于 *ClassInformationOffset* 的值。

 

下表定义了每个数据包的信息数据记录的格式。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Offset</th>
<th>大小</th>
<th>字段</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>4</p></td>
<td><p>大小</p></td>
<td><p>此每个数据包标头的长度（以字节为单位），并追加每个数据包的数据和填充。 此值为4的整数倍。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>类型</p></td>
<td><p>设置为 NDIS_PER_PACKET_INFO_FROM_PACKET 的合法值之一，如 Windows 2000 驱动程序开发工具包 (的 DDK) 中所述。</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>4</p></td>
<td><p>PerPacketInformationOffset</p></td>
<td><p>从每个数据包的信息数据记录开始到每个数据包信息数据的开头的字节偏移量。</p></td>
</tr>
<tr class="even">
<td><p> (N) </p></td>
<td><p>...</p></td>
<td><p>Per-Packet 数据</p></td>
<td><p>Per-Packet 的数据;有关详细信息，请参阅 Windows 2000 DDK 文档。</p></td>
</tr>
</tbody>
</table>

 

**注意**  
 (N) 等于 *PerPacketInformationOffset* 的值。

 

<a name="remarks"></a>备注
-------

每个远程 \_ NDIS \_ 数据包 \_ 消息可能包含一个或多个 OOB 数据记录。 *NumOOBDataElements* 指示此消息中的 OOB 数据记录数。 OOB 数据记录必须按顺序显示。 *OOBDataLength* 字段指示整个 OOB 数据块的长度（以字节为单位）。 *OOBDataOffset* 字段指示从 *数据偏移量* 字段开头到 OOB 数据块开始的字节偏移量。 有关 OOB 数据包数据的详细信息，请参阅 Windows 2000 DDK 中的 NDIS 规范。

如果将多个 OOB 数据块附加到远程 \_ NDIS \_ 数据包消息 \_ 消息，则每个后续 oob 数据记录必须紧跟上一个 oob 记录的数据。

当前没有为802.3 设备定义 OOB 信息。

每个远程 \_ NDIS \_ 数据包 \_ 消息可能包含一个或多个每个数据包信息的数据记录。 每个数据包的信息用于传递包元数据，例如 TCP 校验和。 *PerPacketInfoOffset* 字段指示从 *数据偏移量* 字段开头到每个数据包信息数据记录开始的字节偏移量。 *OOBDataLength* 字段指示每个数据包的信息数据记录的字节长度。 有关每个数据包的信息数据的详细信息，请参阅 Windows 2000 DDK。

如果有多个每个数据包的信息数据块，则每个数据包的后续信息数据记录必须紧跟在上一个每个数据包信息记录的数据中。

远程 NDIS 设备必须通过 NDIS 数据包发送和接收数据。 设备使用的总线确定如何将这些数据包从主机传递到设备和设备到主机。 它可以是共享内存，也可以是 USB、Isoch 和大容量管道。 NDIS 数据包也可能包含带外 (OOB) 数据以及跨网络的数据。

远程 NDIS 设备传输 NDIS 数据包，这些数据包封装为数据通道中的 **远程 \_ NDIS \_ 数据包 \_ 消息** 。 无连接 (（例如 802.3) 和面向连接的 (，例如 ATM) 设备）使用相同的数据包消息结构来简化包处理的通用代码。 每个 **远程 \_ NDIS \_ 数据包 \_** 消息消息都包含一个网络数据单元的相关信息 (例如，) 以太网802.3 帧。

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
<td><p>在 Microsoft Windows XP 和更高版本的 Windows 操作系统中可用。 在 Windows 2000 中也可以作为可再发行二进制文件。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Rndis (包含 Rndis) </td>
</tr>
</tbody>
</table>

 

 




