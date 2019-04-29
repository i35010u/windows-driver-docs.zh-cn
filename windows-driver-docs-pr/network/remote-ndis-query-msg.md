---
title: REMOTE_NDIS_QUERY_MSG
Description: 此消息是发送给远程 NDIS 设备的主机时它需要查询其特征、 统计信息或状态的设备。
ms.assetid: 9cf79495-a115-49ce-a0cf-fa4fa2183a8a
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c8e89f517f7992b2c4ca9c28835678531ec018e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385485"
---
# <a name="remotendisquerymsg"></a>远程\_NDIS\_查询\_消息


此消息是发送给远程 NDIS 设备的主机时它需要查询其特征、 统计信息或状态的设备。 对其进行查询的参数或统计信息计数器被标识通过 NDIS 对象标识符 (OID)。 主机可能会发送远程\_NDIS\_查询\_通过在任何设备已由远程 NDIS 初始化状态的时间控制通道向设备的消息。 远程 NDIS 设备将通过发送一个远程来响应此消息\_NDIS\_查询\_CMPLT 到主机。

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
<td><p>指定发送消息的类型。 将设置为 0x00000004。</p></td>
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
<td><p>Oid</p></td>
<td><p>指定 NDIS OID，标识正在查询的参数。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>InformationBufferLength</p></td>
<td><p>以字节为单位指定查询的输入数据的长度。 设置为零，此时没有 OID 输入缓冲区。</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>4</p></td>
<td><p>InformationBufferOffset</p></td>
<td><p>指定的字节偏移量，从开头<em>RequestId</em>字段中，查询的输入的数据所在位置。 设置为零，如果没有 OID 输入缓冲区。</p></td>
</tr>
<tr class="odd">
<td><p>24</p></td>
<td><p>4</p></td>
<td><p>DeviceVcHandle</p></td>
<td><p>保留的面向连接的设备。 设置为零。</p></td>
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
<td><p>在 Microsoft Windows XP 和更高版本的 Windows 操作系统中可用。 也可在 Windows 2000 中作为可再发行组件的二进制文件。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Rndis.h （包括 Rndis.h）</td>
</tr>
</tbody>
</table>

 

 




