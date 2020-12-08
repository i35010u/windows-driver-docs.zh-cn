---
title: 通信类接口
description: 通信类接口
keywords:
- communication
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 702c81f0e7256259bd2f19ea5039652c9c44e720
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817623"
---
# <a name="communication-class-interface"></a>通信类接口





通信类接口由 USB 接口描述符、三个类特定描述符和通知终结点的终结点描述符描述。 通知终结点描述符是终结点描述符中的标准 USB 中断类型，其 **wMaxPacketSize** 字段为8个字节。 下表定义通信类接口描述符的突出字段。

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
<td align="left"><p>02h</p></td>
<td align="left"><p>通信接口类代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>bInterfaceSubClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>02h</p></td>
<td align="left"><p>抽象控件模型的通信接口类子类代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7</p></td>
<td align="left"><p>bInterfaceProtocol</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>FFh</p></td>
<td align="left"><p>供应商特定协议的通信接口类协议代码。</p></td>
</tr>
</tbody>
</table>

 

 

 





