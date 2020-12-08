---
title: 控制通道特征
description: 控制通道特征
keywords:
- 控制通道特征
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcd36f797a58b5626e8a895523fe26db21fb14fa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822221"
---
# <a name="control-channel-characteristics"></a>控制通道特征





设备的控制通道是其 USB 控制终结点。 从主机到设备的控制消息以发送封装的命令传输的形式发送 \_ \_ 。 下表中定义了此传输。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">BmRequestType</th>
<th align="left">bRequest</th>
<th align="left">wValue</th>
<th align="left">wIndex</th>
<th align="left">wLength</th>
<th align="left">数据</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x21</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>0x0000</p></td>
<td align="left"><p>通信类接口描述符的<em>bInterfaceNumber</em>字段</p></td>
<td align="left"><p>控制消息块的字节长度</p></td>
<td align="left"><p>控制消息块</p></td>
</tr>
</tbody>
</table>

 

主机不会持续轮询输入控制消息的 USB 控制终结点。 将控制消息放置在其控制终结点上后，设备必须返回终结点中通信类接口中断的通知，该通知将在每次设备可以返回控制消息时由主机轮询。 从设备在终结点到主机的中断之间传输是传输的标准 USB 中断。 唯一定义的设备通知是 \_ 下表中定义的响应可用通知。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">偏移量 (字节) </th>
<th align="left">长度 (字节) </th>
<th align="left">字段</th>
<th align="left">数据</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>通知</p></td>
<td align="left"><p> (0x00000001) RESPONSE_AVAILABLE</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

收到响应 \_ 可用通知后，主机将使用 \_ \_ 下表中定义的 "获取封装的响应传输" 从控件终结点读取控制消息。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bmRequestType</th>
<th align="left">bRequest</th>
<th align="left">wValue</th>
<th align="left">wIndex</th>
<th align="left">wLength</th>
<th align="left">数据</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0xA1</p></td>
<td align="left"><p>0x01</p></td>
<td align="left"><p>0x0000</p></td>
<td align="left"><p>通信类接口描述符的<em>bInterfaceNumber</em>字段</p></td>
<td align="left"><p>0x0400 (这是主机发布的缓冲的最小字节长度) </p></td>
<td align="left"><p>控制消息块</p></td>
</tr>
</tbody>
</table>

 

如果由于某种原因，设备收到一个 \_ 封装的 \_ 响应，并且无法使用控制终结点上的有效数据进行响应，则它应将单字节数据包集返回到0x00，而不是停止控制终结点。

 

 





