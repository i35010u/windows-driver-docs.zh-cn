---
title: 控制通道特征
description: 控制通道特征
ms.assetid: b289f21c-a53e-424c-be31-b7a869e335c4
keywords:
- 控制通道特征
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a0dba41cb510802285d5a1b5ecc3d9f181af33f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357416"
---
# <a name="control-channel-characteristics"></a>控制通道特征





设备控制通道是其 USB 控制终结点。 作为发送发送控制消息从主机到设备\_封装\_命令传输。 下表中定义此传输。

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
<td align="left"><p><em>bInterfaceNumber</em>通信类接口描述符字段</p></td>
<td align="left"><p>控制消息块的字节长度</p></td>
<td align="left"><p>控制消息块</p></td>
</tr>
</tbody>
</table>

 

主机不会持续轮询输入的控制消息的 USB 控制终结点。 后将控制消息放置在其控制终结点，设备必须轮询由主机一次时，设备可以将控制消息返回的通信类接口的中断在端点上返回通知。 从设备的中断 IN 终结点传输到该主机是标准的 USB 中断中传输。 仅定义的设备通知是响应\_可用通知下, 表中定义。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">偏移量 （字节）</th>
<th align="left">长度 （字节）</th>
<th align="left">字段</th>
<th align="left">数据</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>通知</p></td>
<td align="left"><p>RESPONSE_AVAILABLE (0x00000001)</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

在收到响应后\_可用通知主机读取控制消息从控制终结点使用 GET\_封装\_响应传输下, 表中定义。

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
<td align="left"><p><em>bInterfaceNumber</em>通信类接口描述符字段</p></td>
<td align="left"><p>0x0400 （这是由主机发送的缓冲区的最小字节长度）</p></td>
<td align="left"><p>控制消息块</p></td>
</tr>
</tbody>
</table>

 

如果由于某种原因，设备收到 GET\_封装\_响应并且不能使用在控制终结点，有效的数据进行响应，则应返回一个字节的数据包将设置为 0x00，而不停止控制终结点。

 

 





