---
title: 终结点描述符中的数据
description: 终结点描述符中的数据
ms.assetid: bf311754-3ef8-483b-8c34-419d2d9c7512
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b01a2967676e23b1353e25395029097863f6f583
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540678"
---
# <a name="data-in-endpoint-descriptor"></a>终结点描述符中的数据





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
<th align="left">偏移量</th>
<th align="left">字段</th>
<th align="left">尺寸</th>
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
<td align="left"><p>此说明符，以字节为单位的大小</p></td>
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
<td align="left"><p>中的终结点 2</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>bmAttributes</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x02</p></td>
<td align="left"><p>大容量终结点</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>wMaxPacketSize</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>0x0040</p></td>
<td align="left"><p>64 字节最大数据包大小</p></td>
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

 

 

 





