---
title: REMOTE_NDIS_QUERY_CMPLT
description: 远程 NDIS 设备将使用 REMOTE_NDIS_QUERY_CMPLT 消息响应 REMOTE_NDIS_QUERY_MSG 消息。
ms.assetid: 357e2ade-0b67-42c3-b1e1-dcc4b7ec5cda
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b761422a965a98f47af23e2c6bb96e5660f6330
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968638"
---
# <a name="remote_ndis_query_cmplt"></a>远程 \_ NDIS \_ 查询 \_ CMPLT


远程 ndis 设备将使用远程 ndis 查询消息 CMPLT 消息响应 [**远程 \_ ndis \_ 查询 \_ **](remote-ndis-query-msg.md) 消息 \_ \_ \_ 。 此消息用于将设备参数或统计信息计数器查询的结果中继到主机。 远程 NDIS 设备还会在此消息中将所请求的信息返回给主机。

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
<td><p>指定要发送的消息的类型。 设置为0x80000004。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>MessageLength</p></td>
<td><p>指定从消息开头开始的此消息的总长度（以字节为单位）。</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>4</p></td>
<td><p>RequestId</p></td>
<td><p>指定远程 NDIS 消息 ID 值。 此值从要响应的 REMOTE_NDIS_QUERY_MSG 复制。</p></td>
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
<td><p>指定查询的响应数据的长度（以字节为单位）。 如果没有 OID 结果缓冲区，则设置为零。</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>4</p></td>
<td><p>InformationBufferOffset</p></td>
<td><p>指定来自 <em>RequestId</em> 字段开头的字节偏移量，查询的响应数据位于该位置。 如果没有响应数据，则设置为零。</p></td>
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

 

 




