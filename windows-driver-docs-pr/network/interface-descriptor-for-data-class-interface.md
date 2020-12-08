---
title: 数据类接口的接口描述符
description: 数据类接口的接口描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cc5e1cf184ce463c43114bfcee69f87bb0c6be8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840641"
---
# <a name="interface-descriptor-for-data-class-interface"></a>数据类接口的接口描述符





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
<td align="left"><p>0x09</p></td>
<td align="left"><p>此描述符的大小（以字节为单位）</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>bDescriptorType</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x04</p></td>
<td align="left"><p>接口描述符</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>bInterfaceNumber</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x01</p></td>
<td align="left"><p>此接口的索引</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>bAlternateSetting</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>此设置的索引</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>bNumEndpoints</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x02</p></td>
<td align="left"><p>2个终结点</p></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p>bInterfaceClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x0A</p></td>
<td align="left"><p>数据类</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>bInterfaceSubclass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>未使用</p></td>
</tr>
<tr class="even">
<td align="left"><p>7</p></td>
<td align="left"><p>bInterfaceProtocol</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>未使用</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"><p>iInterface</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>未使用</p></td>
</tr>
</tbody>
</table>

 

 

 





