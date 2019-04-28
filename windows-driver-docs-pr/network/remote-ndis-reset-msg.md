---
title: REMOTE_NDIS_RESET_MSG
Description: 此消息发送给远程 NDIS 设备的主机以将设备重置并返回状态。
ms.assetid: b5938b0d-75bf-497f-afeb-9950b383af5e
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: beed2ca885a5d76af4f43c1efc58411b215e3bc9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351259"
---
# <a name="remotendisresetmsg"></a>远程\_NDIS\_重置\_消息


此消息发送给远程 NDIS 设备的主机以将设备重置并返回状态。 主机可能会发送远程\_NDIS\_重置\_通过在设备处于状态由远程 NDIS 初始化任何时间控制通道向设备的消息。 远程 NDIS 设备将通过发送一个远程来响应此消息\_NDIS\_重置\_CMPLT 到主机。

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
<td><p>指定发送消息的类型。 将设置为 0x00000006。</p></td>
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
<td><p>保留</p></td>
<td><p>保留。 设置为零。</p></td>
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

 

 




