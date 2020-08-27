---
title: REMOTE_NDIS_HALT_MSG
description: 此消息由主机发送以终止网络连接。
ms.assetid: ad7802ff-20ee-4228-b236-a2ca39e8c478
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7386f199e3301b327be0fdd160f1c1c7ce4ca0de
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968830"
---
# <a name="remote_ndis_halt_msg"></a>远程 \_ NDIS \_ 停止 \_ 消息


此消息由主机发送以终止网络连接。 与其他主机启动的控制消息不同，设备不响应远程 \_ NDIS \_ 停止 \_ 消息。

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
<td><p>指定要发送的消息的类型。 设置为0x00000003。</p></td>
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
<td><p>指定远程 NDIS 消息 ID 值。 此值用于匹配主机发送的包含设备响应的消息。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

对于设备，实现远程 \_ NDIS 暂停消息是可选 \_ 的 \_ 。 如果实现了此项，则仅当设备处于远程 NDIS 初始化的状态时，设备才会通过控制通道将此消息发送给主机。 发送此消息后，设备必须立即终止所有通信。 发送此消息会导致设备进入不是由远程 NDIS 初始化的状态。

收到此消息时，所有未完成的请求和数据包都应丢弃。

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

 

 




