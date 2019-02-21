---
title: REMOTE_NDIS_INDICATE_STATUS_MSG
Description: This message is sent from a Remote NDIS device to a host to indicate a change in the status of the device.
ms.assetid: 768aad13-3da6-436c-a7ba-d420af34643e
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26c27b3fb61aacdfc6e9463f47b8041e31a1731f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524918"
---
# <a name="remotendisindicatestatusmsg"></a>远程\_NDIS\_指示\_状态\_消息


此消息是从远程 NDIS 设备发送到主机以指示设备的状态中的更改。 远程\_NDIS\_指示\_状态\_MSG 消息还可以用来表示发生了错误事件，如无法识别的消息。 远程 NDIS 设备可能处于状态由远程 NDIS 初始化任何时候发送此消息。 为此邮件没有响应。

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
<td><p>指定发送消息的类型。 将设置为 0x00000007。</p></td>
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
<td><p>指定主机请求的当前状态。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>StatusBufferLength</p></td>
<td><p>以字节为单位指定的状态数据的长度。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>StatusBufferOffset</p></td>
<td><p>指定的字节偏移量，从一开始此消息，请为设备可能 Rndis_Diagnostic_Info 状态数据所在位置。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

最常用的远程\_NDIS\_指示\_状态\_消息是指示 802.3 设备的链接的状态。 将 status 值为 RNDIS\_状态\_媒体\_CONNECT 指示从过渡断开连接 （例如没有 802.3 链接脉冲） 到已连接的状态 (检测到 pulse 802.3 链接)。 将 status 值为 RNDIS\_状态\_媒体\_断开连接指示从连接到断开连接状态的转换。 设备必须发送远程\_NDIS\_指示\_状态\_消息与下列任一值每次 802.3 链接状态发生更改。 没有状态缓冲区需要返回这些两个常见的指示。

在其中为主机的设备无法处理的消息的响应中发送此消息的特定情况下*状态*字段必须设置为 RNDIS\_状态\_无效\_数据和 Rndis\_诊断\_信息状态缓冲区格式，如下所示。

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
<td><p>DiagStatus</p></td>
<td><p>包含有关与错误本身 (例如，RNDIS_STATUS_NOT_SUPPORTED) 的状态信息</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>ErrorOffset</p></td>
<td><p>在其中检测到错误的原始消息中指定的从零开始的字节偏移量。</p></td>
</tr>
</tbody>
</table>

 

如果由远程 NDIS 消息引起的错误条件 （例如，设备不能识别特定 RNDIS 消息），则设备应追加的原始消息，以上面定义的状态消息的末尾。

此消息用于报告错误条件仅在环境中的设备不能够生成包含相应的状态的响应消息。 相应的使用情况的示例包括：

-   在使用不受支持的消息类型接收一条消息。

-   在收到[**远程\_NDIS\_数据包\_MSG** ](remote-ndis-packet-msg.md)不可接受的内容。

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

 

 




