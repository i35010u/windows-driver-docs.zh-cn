---
title: 数据输入终结点描述符
description: 数据输入终结点描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52cb90110156d96cfc3fbc3964f601c91024fa61
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815003"
---
# <a name="data-in-endpoint-descriptor"></a>数据输入终结点描述符





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
<th align="left">Offset</th>
<th align="left">字段</th>
<th align="left">大小</th>
<th align="left">值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>bLength</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x07</p></td>
<td align="left"><p>此描述符的大小（以字节为单位）</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>bDescriptorType</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x05</p></td>
<td align="left"><p>终结点描述符</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>bEndpointAddress</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x82</p></td>
<td align="left"><p>中的终结点2</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>bmAttributes</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x02</p></td>
<td align="left"><p>批量终结点</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>wMaxPacketSize</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>0x0040</p></td>
<td align="left"><p>64字节最大数据包大小</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>bInterval</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>未使用</p></td>
</tr>
</tbody>
</table>

 

 

 





