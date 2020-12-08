---
title: REMOTE_NDIS_INDICATE_STATUS_MSG
description: 此消息将从远程 NDIS 设备发送到主机，以指示设备的状态发生更改。
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4369f64ce976bf245aff600a5669e320d1001a5b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818341"
---
# <a name="remote_ndis_indicate_status_msg"></a>远程 \_ NDIS \_ 指示 \_ 状态 \_ 消息


此消息将从远程 NDIS 设备发送到主机，以指示设备的状态发生更改。 远程 \_ NDIS \_ 指示 \_ 状态 \_ 消息消息还可用于指示错误事件，例如无法识别的消息。 远程 NDIS 设备可以在任何时候发送此消息，因为它处于由远程 NDIS 初始化的状态。 此消息没有响应。

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
<td><p>指定要发送的消息的类型。 设置为0x00000007。</p></td>
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
<td><p>状态</p></td>
<td><p>指定主机请求的当前状态。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>StatusBufferLength</p></td>
<td><p>指定状态数据的长度（以字节为单位）。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>StatusBufferOffset</p></td>
<td><p>指定设备指示 Rndis_Diagnostic_Info 状态数据位于此消息开头的字节偏移量。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

远程 NDIS 最常见的用途 \_ \_ 是指示 \_ 状态 \_ 消息，指示802.3 设备的链接的状态。 Status 值 RNDIS \_ status \_ MEDIA \_ CONNECT 指示从断开连接 (（例如，无 802.3 link 脉冲) 连接状态） (802.3 link 脉冲检测到) 。 "RNDIS \_ 状态 \_ 媒体断开连接" 状态值 \_ 指示从连接到断开状态的转换。 \_ \_ \_ \_ 每次802.3 链接状态发生更改时，设备必须发送远程 NDIS 指示状态消息，并显示其中一个值。 不需要状态缓冲区即可返回这两个常见的指示。

在为响应设备无法处理的主机消息而发送此消息的特定情况下，" *状态* " 字段必须设置为 "RNDIS \_ 状态 \_ 无效 \_ 数据"，并且 RNDIS \_ 诊断 \_ 信息状态缓冲区的格式如下所示。

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
<td><p>DiagStatus</p></td>
<td><p>包含有关错误本身的状态信息 (例如，RNDIS_STATUS_NOT_SUPPORTED) </p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>ErrorOffset</p></td>
<td><p>指定原始消息中检测到错误的位置的从零开始的字节偏移量。</p></td>
</tr>
</tbody>
</table>

 

如果错误条件是由远程 NDIS 消息引起的 (例如，设备无法识别特定的 RNDIS 消息) ，则设备应在上面定义的状态消息末尾追加原始消息。

此消息仅用于在设备无法生成具有适当状态的响应消息时报告错误条件。 适当用法的示例如下：

-   接收到消息类型不受支持的消息。

-   接收到带有不可接受内容的 [**远程 \_ NDIS \_ 数据包 \_ 消息**](remote-ndis-packet-msg.md) 时。

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

 

 




