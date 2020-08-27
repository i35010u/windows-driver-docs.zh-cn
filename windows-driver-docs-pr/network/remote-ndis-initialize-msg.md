---
title: REMOTE_NDIS_INITIALIZE_MSG
description: 此消息由主机发送到远程 NDIS 设备，以便初始化网络连接。
ms.assetid: 08735ee8-7a4c-4a3d-9082-27c61cfd15e8
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 703865ff32108dfb78e8067ae506bdcf6496b803
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968714"
---
# <a name="remote_ndis_initialize_msg"></a>远程 \_ NDIS \_ 初始化 \_ 消息


此消息由主机发送到远程 NDIS 设备，以便初始化网络连接。 它是通过控制通道发送的，并且仅在设备未处于通过远程 NDIS 初始化的状态时发送。

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
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>4</p></td>
<td><p>MessageType</p></td>
<td><p>指定要发送的消息的类型。 设置为0x00000002。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>MessageLength</p></td>
<td><p>从消息的开头指定此消息的总长度（以字节为单位）。</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>4</p></td>
<td><p>RequestId</p></td>
<td><p>指定远程 NDIS 消息 ID 值。 此值用于匹配主机发送的包含设备响应的消息。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>MajorVersion</p></td>
<td><p>指定由主机实现的远程 NDIS 协议版本。 当前规范使用 RNDIS_MAJOR_VERSION = 1。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>MinorVersion</p></td>
<td><p>指定由主机实现的远程 NDIS 协议版本。 当前规范使用 RNDIS_MINOR_VERSION = 0。</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>4</p></td>
<td><p>MaxTransferSize</p></td>
<td><p>指定主机预期从设备接收的任何单个总线数据传输的最大大小（以字节为单位）。 通常，每个总线数据传输都容纳单个远程 NDIS 消息。 但是，设备可能会将包含数据包的多个远程 NDIS 消息捆绑到单个传输 (请参阅 <a href="remote-ndis-packet-msg.md" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_PACKET_MSG&lt;/strong&gt;](remote-ndis-packet-msg.md)"><strong>REMOTE_NDIS_PACKET_MSG</strong></a>) 。</p></td>
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
<td><p>Version</p></td>
<td><p>在 Microsoft Windows XP 和更高版本的 Windows 操作系统中可用。 在 Windows 2000 中也可以作为可再发行二进制文件。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Rndis (包含 Rndis) </td>
</tr>
</tbody>
</table>

 

 




