---
title: REMOTE_NDIS_SET_CMPLT
Description: A Remote NDIS device will respond to a REMOTE_NDIS_SET_MSG message with a REMOTE_NDIS_SET_CMPLT message.
ms.assetid: 97436a5f-7516-46cf-b789-a6b1c8c067a2
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3664bd100a640d6ece3441b68a3f1242c60e595
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575195"
---
# <a name="remotendissetcmplt"></a>远程\_NDIS\_设置\_CMPLT


远程 NDIS 设备将响应[**远程\_NDIS\_设置\_MSG** ](remote-ndis-set-msg.md)带有远程邮件\_NDIS\_集\_CMPLT 消息。 此消息用于中继到主机设置设备的操作参数的值的结果。

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
<td><p>指定发送消息的类型。 将设置为 0x80000005。</p></td>
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
<td><p>指定远程 NDIS 消息 ID 值。 从响应 REMOTE_NDIS_SET_MSG 复制此值。</p></td>
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
<td><p>在 Microsoft Windows XP 和更高版本的 Windows 操作系统中可用。 也可在 Windows 2000 中作为可再发行组件的二进制文件。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Rndis.h （包括 Rndis.h）</td>
</tr>
</tbody>
</table>

 

 




