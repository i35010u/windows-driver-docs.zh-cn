---
title: USB 设备描述符
description: USB 设备描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0d8d96ec85a5b44a48d0a7726d745cf6a21023f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837899"
---
# <a name="usb-device-descriptor"></a>USB 设备描述符





设备返回 USB 规范中定义的 USB 设备描述符。 下表定义了 USB 设备描述符的醒目字段。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">偏移量 (字节) </th>
<th align="left">字段</th>
<th align="left">大小（字节）</th>
<th align="left">“值”</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>bDeviceClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>02h</p></td>
<td align="left"><p>通信设备类代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p>bDeviceSubClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>指</p></td>
<td align="left"><p>通信设备子类代码，此时未使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>bDeviceProtocol</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>指</p></td>
<td align="left"><p>目前未使用通信设备协议代码。</p></td>
</tr>
</tbody>
</table>

 

 

 





