---
title: 数据类接口
description: 数据类接口
ms.assetid: d7bf9ec3-8bf3-45a9-84a2-c507953d1ad4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b16b280d233c3e4142db334d16e853ba3e3361e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387390"
---
# <a name="data-class-interface"></a>数据类接口





通过标准 USB 接口描述符后, 跟两个终结点描述符详细介绍了数据类接口。 在数据类接口中的两个终结点描述符定义标准 USB 大容量类型终结点： 一个大容量-IN 和一个向外大容量。 下表定义数据类接口描述符的重要字段。

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
<td align="left"><p>00 h</p></td>
<td align="left"><p>数据类子类代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7</p></td>
<td align="left"><p>bInterfaceProtocol</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>00 h</p></td>
<td align="left"><p>数据类协议代码。</p></td>
</tr>
</tbody>
</table>

 

 

 





