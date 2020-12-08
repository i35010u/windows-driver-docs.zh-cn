---
title: REMOTE_NDIS_QUERY_MSG
description: 如果需要在设备上查询设备的特性、统计信息或状态，则会将此消息从主机发送到远程 NDIS 设备。
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4e21e19cafdcad3f006c46b1675e2badc78e1a3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833311"
---
# <a name="remote_ndis_query_msg"></a>远程 \_ NDIS \_ 查询 \_ 消息


如果需要在设备上查询设备的特性、统计信息或状态，则会将此消息从主机发送到远程 NDIS 设备。 正在查询的参数或统计信息计数器由 (OID) 的 NDIS 对象标识符标识。 当设备处于远程 NDIS 初始化的状态时，主机可能会 \_ \_ 通过控制通道向设备发送远程 ndis 查询 \_ 消息。 远程 NDIS 设备将通过 \_ 向主机发送远程 ndis 查询 CMPLT 来响应此消息 \_ \_ 。

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
<td><p>指定要发送的消息的类型。 设置为0x00000004。</p></td>
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
<td><p>Oid</p></td>
<td><p>指定标识正在查询的参数的 NDIS OID。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>InformationBufferLength</p></td>
<td><p>指定查询的输入数据的长度（以字节为单位）。 如果没有 OID 输入缓冲区，则设置为零。</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>4</p></td>
<td><p>InformationBufferOffset</p></td>
<td><p>指定查询的输入数据位于 <em>RequestId</em> 字段开头的字节偏移量。 如果没有 OID 输入缓冲区，则设置为零。</p></td>
</tr>
<tr class="odd">
<td><p>24</p></td>
<td><p>4</p></td>
<td><p>DeviceVcHandle</p></td>
<td><p>为面向连接的设备保留。 设置为零。</p></td>
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
<td><p>在 Microsoft Windows XP 和更高版本的 Windows 操作系统中可用。 在 Windows 2000 中也可以作为可再发行二进制文件。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Rndis (包含 Rndis) </td>
</tr>
</tbody>
</table>

 

 




