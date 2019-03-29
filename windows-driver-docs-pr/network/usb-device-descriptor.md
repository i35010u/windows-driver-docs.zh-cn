---
title: USB 设备描述符
description: USB 设备描述符
ms.assetid: ef2a3e43-0e55-4e8e-ad86-efcbe153c847
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c260bfbac83c4beea5f77ccbab097255a0a0b15
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577328"
---
# <a name="usb-device-descriptor"></a>USB 设备描述符





设备返回 USB 设备描述符 USB 规范中定义。 下表定义重要的 USB 设备描述符字段。

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
<th align="left">偏移量 （字节）</th>
<th align="left">字段</th>
<th align="left">大小 （字节）</th>
<th align="left">ReplTest1</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>bDeviceClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>02 h</p></td>
<td align="left"><p>通信设备类代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p>bDeviceSubClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>00 h</p></td>
<td align="left"><p>通信设备子类代码，在这一次未使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>bDeviceProtocol</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>00 h</p></td>
<td align="left"><p>通信设备协议代码，在这一次未使用。</p></td>
</tr>
</tbody>
</table>

 

 

 





