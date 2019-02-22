---
title: REMOTE_NDIS_RESET_CMPLT
Description: A Remote NDIS device will respond to a REMOTE_NDIS_RESET_MSG message from the host by resetting the device and returning the status of the request in the REMOTE_NDIS_RESET_CMPLT message.
ms.assetid: 80ab998f-9690-49d3-bb47-1937c832d13e
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 853e8d4fc849662eeda2426c504b50e570b238c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547442"
---
# <a name="remotendisresetcmplt"></a>远程\_NDIS\_重置\_CMPLT


远程 NDIS 设备将响应[**远程\_NDIS\_重置\_MSG** ](remote-ndis-reset-msg.md)从主机通过将设备重置并返回请求的状态消息在远程\_NDIS\_重置\_CMPLT 消息。

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
<td><p>指定发送消息的类型。 将设置为 0x80000006。</p></td>
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
<td><p>状态</p></td>
<td><p>指定处理重置请求的状态。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>AddressingReset</p></td>
<td><p>指示是否寻址 （多路广播的地址列表，数据包筛选器） 的信息已丢失结束重置操作过程。 如果设备需要主机重新发送寻址信息，此字段设置为 1;否则将其设置为零。</p></td>
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

 

 




