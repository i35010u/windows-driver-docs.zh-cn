---
title: REMOTE_NDIS_KEEPALIVE_MSG
description: 当没有任何其他控制或数据流量从设备发送到总线定义的 KeepAliveTimeoutPeriod 的主机时，主机会定期发送此消息。
ms.assetid: 7e0b329f-8ba7-488d-b99d-63e6b9bbc171
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: db2f2e58ea28be672a6cb620a81aa9a3471127c3
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969402"
---
# <a name="remote_ndis_keepalive_msg"></a>远程 \_ NDIS \_ KEEPALIVE \_ 消息


当没有任何其他控制或数据流量从设备发送到总线定义的 *KeepAliveTimeoutPeriod*的主机时，主机会定期发送此消息。 在没有其他消息流量的情况下，主机至少会发送此消息， \_ \_ 以检测远程设备的状态。 远程设备可能会在反向方向上使用相同的消息，但这不是必需的。

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
<td><p>指定要发送的消息的类型。 设置为0x00000008。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>MessageLength</p></td>
<td><p>从消息的开头指定此消息的总长度（以字节为单位）。</p></td>
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

在 \_ \_ \_ \_ \_ 从远程设备收到最后一条消息后，主机将不会发送远程 NDIS KEEPALIVE 消息消息，直到 RNDIS KEEPALIVE 超时秒数。 这可以避免在通信通道处于活动状态时不必要地交换 keep-alive 消息。

设备还可以选择将此消息发送到主机。 例如，设备可能使用此消息来触发主机的响应，以便计算往返延迟时间。 如果实现了此项，则设备 \_ 必须 \_ 通过控制通道发送远程 ndis KEEPALIVE \_ 消息，且仅当设备处于通过远程 ndis 初始化的状态时。

主机通过控制通道向设备发送 **远程 \_ NDIS \_ KEEPALIVE \_ ** 消息消息，以检查设备的运行状况。 当设备处于远程 NDIS 初始化的状态时，主机会在没有任何其他控制或数据流量从设备到 *KeepAliveTimeoutPeriod*的主机上定期发送此消息。 *KeepAliveTimeoutPeriod* 依赖于总线，并在相应的总线映射规范中定义。

收到此消息后，远程设备必须返回响应，该响应的 " *状态* " 字段指示设备是否从主机 jenni [**远程 \_ NDIS \_ RESET \_ **](remote-ndis-reset-msg.md) 消息消息。

如果设备阻止从主机查看 **远程 \_ NDIS \_ KEEPALIVE \_ ** 消息消息，则不需要执行任何特定操作。

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

 

 




