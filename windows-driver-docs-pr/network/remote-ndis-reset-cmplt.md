---
title: REMOTE_NDIS_RESET_CMPLT
description: 远程 NDIS 设备将通过重置设备并返回 REMOTE_NDIS_RESET_CMPLT 消息中请求的状态来响应来自主机的 REMOTE_NDIS_RESET_MSG 消息。
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64a1be4af84d37774b2a041c53e5cc8c0cb94245
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789644"
---
# <a name="remote_ndis_reset_cmplt"></a>远程 \_ NDIS \_ 重置 \_ CMPLT


远程 NDIS 设备将通过重置设备并返回远程 ndis 重置 CMPLT 消息中的请求状态来响应来自主机的 [**远程 \_ ndis \_ 重置 \_**](remote-ndis-reset-msg.md) 消息 \_ 消息 \_ \_ 。

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
<td><p>指定要发送的消息的类型。 设置为0x80000006。</p></td>
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
<td><p>状态</p></td>
<td><p>指定处理重置请求的状态。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>AddressingReset</p></td>
<td><p>指示在执行 "重置" 操作期间是否丢失了寻址信息 (多播地址列表、数据包筛选器) 。 如果设备要求主机重新发送寻址信息，请将此字段设置为 1;否则将其设置为零。</p></td>
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

 

 




