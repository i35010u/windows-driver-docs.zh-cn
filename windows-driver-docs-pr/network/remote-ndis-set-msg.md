---
title: REMOTE_NDIS_SET_MSG
Description: This message is sent to a Remote NDIS device from a host, when it requires to set the value of some operational parameter on the device.
ms.assetid: d39032e2-e3a5-415f-8bd6-b60b9049ce33
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: d730f462919a074f85f869d042480ccace052066
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566495"
---
# <a name="remotendissetmsg"></a>远程\_NDIS\_设置\_消息


此消息是发送给远程 NDIS 设备的主机时，需要在设备上设置某些操作的参数的值时。 要设置的特定参数标识通过对象标识符 (OID)，并且与消息一起发送信息缓冲区中包含的值，则设置为。 主机可能会发送远程\_NDIS\_设置\_通过在设备处于状态由远程 NDIS 初始化任何时间控制通道向设备的消息。 远程 NDIS 设备将通过发送一个远程来响应此消息\_NDIS\_设置\_CMPLT 到主机。

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
<td><p>指定发送消息的类型。 将设置为 0x00000005。</p></td>
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
<td><p>Oid</p></td>
<td><p>指定 NDIS OID，标识要设置的参数。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>InformationBufferLength</p></td>
<td><p>以字节为单位，指定请求的输入数据的长度。</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>4</p></td>
<td><p>InformationBufferOffset</p></td>
<td><p>指定的字节偏移量，从开头<em>RequestId</em>字段中，请求的输入的数据所在位置。</p></td>
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
<td><p>版本</p></td>
<td><p>在 Microsoft Windows XP 和更高版本的 Windows 操作系统中可用。 也可在 Windows 2000 中作为可再发行组件的二进制文件。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Rndis.h （包括 Rndis.h）</td>
</tr>
</tbody>
</table>

 

 




