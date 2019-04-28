---
title: REMOTE_NDIS_QUERY_CMPLT
Description: 远程 NDIS 设备将响应将 REMOTE_NDIS_QUERY_MSG 消息 REMOTE_NDIS_QUERY_CMPLT 消息。
ms.assetid: 357e2ade-0b67-42c3-b1e1-dcc4b7ec5cda
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 618860ecf39a5660b7a3bc3cf8f4fc9e66b0bf37
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350827"
---
# <a name="remotendisquerycmplt"></a>远程\_NDIS\_查询\_CMPLT


远程 NDIS 设备将响应[**远程\_NDIS\_查询\_MSG** ](remote-ndis-query-msg.md)带有远程邮件\_NDIS\_查询\_CMPLT 消息。 此消息用于中继到主机的设备参数或统计信息计数器的查询的结果。 远程 NDIS 设备还将恢复此消息中的主机所需的信息。

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
<td><p>指定发送消息的类型。 将设置为 0x80000004。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>MessageLength</p></td>
<td><p>以字节为单位，指定该消息的开始的这封邮件的总长度。</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>4</p></td>
<td><p>RequestId</p></td>
<td><p>指定远程 NDIS 消息 ID 值。 从响应 REMOTE_NDIS_QUERY_MSG 复制此值。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>状态</p></td>
<td><p>指定处理 OID 查询请求的状态。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>InformationBufferLength</p></td>
<td><p>以字节为单位，指定的查询的响应数据的长度。 设置为零，此时没有 OID 结果缓冲区。</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>4</p></td>
<td><p>InformationBufferOffset</p></td>
<td><p>指定的字节偏移量，从开头<em>RequestId</em>字段中，查询的数据所在位置的响应。 设置为零，如果没有响应的数据。</p></td>
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

 

 




