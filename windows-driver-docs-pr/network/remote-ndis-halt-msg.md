---
title: REMOTE_NDIS_HALT_MSG
Description: 主机发送此消息以终止网络连接。
ms.assetid: ad7802ff-20ee-4228-b236-a2ca39e8c478
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c12ac1133475961bc85d0431338698187dc39cb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350916"
---
# <a name="remotendishaltmsg"></a>远程\_NDIS\_暂停\_消息


主机发送此消息以终止网络连接。 与不同的其他主机启动的控制消息，设备不响应远程\_NDIS\_暂停\_消息。

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
<td><p>指定发送消息的类型。 将设置为 0x00000003。</p></td>
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
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

是可选的设备来实现远程\_NDIS\_暂停\_消息。 如果实现，该设备发送控制通道通过主机到此消息，仅当设备处于由远程 NDIS 初始化状态时。 设备必须终止后立即发送此消息的所有通信。 发送此消息会导致设备进入远程 NDIS 未初始化状态。

应在收到此消息丢弃所有未完成的请求和数据包。

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

 

 




