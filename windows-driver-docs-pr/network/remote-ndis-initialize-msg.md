---
title: REMOTE_NDIS_INITIALIZE_MSG
Description: This message is sent by the host to a Remote NDIS device to initialize the network connection.
ms.assetid: 08735ee8-7a4c-4a3d-9082-27c61cfd15e8
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74da17faed5fa28822ff5098414175bb27f1990c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544188"
---
# <a name="remotendisinitializemsg"></a>远程\_NDIS\_初始化\_消息


远程 NDIS 设备向主机发送此消息来初始化网络连接。 发送控制通道通过且仅当设备不由远程 NDIS 初始化的状态。

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
<td><p>指定发送消息的类型。 将设置为 0x00000002。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>MessageLength</p></td>
<td><p>以字节为单位指定的消息的开始，这封邮件的总长度。</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>4</p></td>
<td><p>RequestId</p></td>
<td><p>指定远程 NDIS 消息 ID 值。 此值用于匹配的设备响应主机发送的消息。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>主要版本</p></td>
<td><p>指定由宿主实现的远程 NDIS 协议版本。 当前规范使用 RNDIS_MAJOR_VERSION = 1。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>MinorVersion</p></td>
<td><p>指定由宿主实现的远程 NDIS 协议版本。 当前规范使用 RNDIS_MINOR_VERSION = 0。</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>4</p></td>
<td><p>MaxTransferSize</p></td>
<td><p>以字节为单位的主机需要从设备接收任何单个总线数据传输指定的最大大小。 通常情况下，每次总线数据传输适合于在单个远程 NDIS 消息。 但是，设备可能捆绑到单一传输包含数据的数据包的多个远程 NDIS 消息 (请参阅<a href="remote-ndis-packet-msg.md" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_PACKET_MSG&lt;/strong&gt;](remote-ndis-packet-msg.md)"> <strong>REMOTE_NDIS_PACKET_MSG</strong></a>)。</p></td>
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
<td><p>版本</p></td>
<td><p>在 Microsoft Windows XP 和更高版本的 Windows 操作系统中可用。 也可在 Windows 2000 中作为可再发行组件的二进制文件。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Rndis.h （包括 Rndis.h）</td>
</tr>
</tbody>
</table>

 

 




