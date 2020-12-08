---
title: 数据类接口
description: 数据类接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9188481819f3f35c37a2dac2daa5334f69190bc1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799409"
---
# <a name="data-class-interface"></a>数据类接口





数据类接口由标准 USB 接口描述符（后跟两个终结点描述符）描述。 数据类接口中的两个终结点描述符定义标准 USB 大容量类型终结点：一个批量输入终结点和一个大容量输出终结点。 下表定义了数据类接口描述符的突出字段。

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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>5</p></td>
<td align="left"><p>bInterfaceClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0Ah</p></td>
<td align="left"><p>数据接口类代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>bInterfaceSubClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>指</p></td>
<td align="left"><p>数据类子类代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7</p></td>
<td align="left"><p>bInterfaceProtocol</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>指</p></td>
<td align="left"><p>数据类协议代码。</p></td>
</tr>
</tbody>
</table>

 

 

 





