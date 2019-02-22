---
title: REMOTE_NDIS_KEEPALIVE_CMPLT
Description: A Remote NDIS device will respond to a REMOTE_NDIS_KEEPALIVE_MSG message from the host by sending back a REMOTE_NDIS_KEEPALIVE_CMPLT response message.
ms.assetid: c090b781-73f1-4a7a-a0a2-60af366daa77
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69abf349b66b4307f62d00827d79829660822ae8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523223"
---
# <a name="remotendiskeepalivecmplt"></a>REMOTE\_NDIS\_KEEPALIVE\_CMPLT


远程 NDIS 设备将响应[**远程\_NDIS\_KEEPALIVE\_MSG** ](remote-ndis-keepalive-msg.md)消息从通过发回远程主机\_NDIS\_KEEPALIVE\_CMPLT 响应消息。 如果返回的状态不是 RNDIS\_状态\_成功后，将发送主机[**远程\_NDIS\_重置\_MSG** ](remote-ndis-reset-msg.md)重置设备。

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
<td><p>指定发送消息的类型。 将设置为 0x80000008。</p></td>
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
<td><p>指定远程 NDIS 消息 ID 值。 此值用于匹配的设备响应主机发送的消息。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>状态</p></td>
<td><p>指定设备的当前状态。 如果返回<em>状态</em>不是 RNDIS_STATUS_SUCCESS，主机将发送<a href="remote-ndis-reset-msg.md" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_RESET_MSG&lt;/strong&gt;](remote-ndis-reset-msg.md)"> <strong>REMOTE_NDIS_RESET_MSG</strong> </a>消息将设备重置。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果设备实现选择发送[**远程\_NDIS\_KEEPALIVE\_MSG**](remote-ndis-keepalive-msg.md)，主机将使用远程响应\_NDIS\_KEEPALIVE\_CMPLT 通过控制通道。

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

 

 




