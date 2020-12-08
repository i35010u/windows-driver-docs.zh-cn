---
title: REMOTE_NDIS_SET_CMPLT
description: 远程 NDIS 设备将使用 REMOTE_NDIS_SET_CMPLT 消息响应 REMOTE_NDIS_SET_MSG 消息。
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 898998cb8a9b8cff96641e265f84fe4f46fcfa42
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792625"
---
# <a name="remote_ndis_set_cmplt"></a>远程 \_ NDIS \_ 设置 \_ CMPLT


远程 ndis 设备将使用远程 ndis set CMPLT 消息对 [**远程 \_ ndis \_ set \_ MSG**](remote-ndis-set-msg.md) 消息做出响应 \_ \_ \_ 。 此消息用于中继将设备操作参数的值设置为主机的结果。

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
<td><p>指定要发送的消息的类型。 设置为0x80000005。</p></td>
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
<td><p>指定远程 NDIS 消息 ID 值。 此值从要响应的 REMOTE_NDIS_SET_MSG 复制。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>状态</p></td>
<td><p>指定处理 OID 集请求的状态。</p></td>
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

 

 




