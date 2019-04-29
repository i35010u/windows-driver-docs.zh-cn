---
title: REMOTE_NDIS_KEEPALIVE_MSG
Description: 主机已没有其他控件或数据从设备到通信的主机总线定义 KeepAliveTimeoutPeriod 时定期发送此消息。
ms.assetid: 7e0b329f-8ba7-488d-b99d-63e6b9bbc171
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f9415e36ec305b1fb0df2e30106d8f4398d051f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350856"
---
# <a name="remotendiskeepalivemsg"></a>远程\_NDIS\_KEEPALIVE\_消息


主机发送此消息已没有其他控件或数据流量从设备到总线定义的主机时定期*KeepAliveTimeoutPeriod*。 此消息由主机发送至少每隔 RNDIS\_KEEPALIVE\_超时 （秒)，如果没有其他消息流量，以检测远程设备的状态。 远程设备可以使用相同的消息按反向执行，但不需要。

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
<td><p>指定发送消息的类型。 将设置为 0x00000008。</p></td>
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

主机将不会发送远程\_NDIS\_KEEPALIVE\_MSG 消息直到 RNDIS\_KEEPALIVE\_后从远程设备收到的最后一个消息经过超时 （秒）。 这样可以避免不必要的保持活动状态的消息交换的通信通道处于活动状态时。

设备 （可选） 可以向主机也发送此消息。 例如，设备可能会使用此消息可用于计算往返延迟时间触发从主机的响应。 如果实现，设备必须发送远程\_NDIS\_KEEPALIVE\_通过控制通道和仅当设备处于由远程 NDIS 初始化的状态消息。

主机发送**远程\_NDIS\_KEEPALIVE\_MSG**控制通道通过向设备的消息，以检查设备的运行状况。 状态初始化远程 NDIS 设备时，主机将此消息发送已没有其他控件或数据从设备到通信的主机时定期*KeepAliveTimeoutPeriod*。 *KeepAliveTimeoutPeriod*总线取决于和相应的总线映射规范中定义。

远程设备必须将响应返回收到此消息时，其*状态*字段指示设备是否请求提供[**远程\_NDIS\_重置\_MSG** ](remote-ndis-reset-msg.md)从主机的消息。

设备不需要执行任何特定操作，停止时看到**远程\_NDIS\_KEEPALIVE\_MSG**来自主机的消息。

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

 

 




