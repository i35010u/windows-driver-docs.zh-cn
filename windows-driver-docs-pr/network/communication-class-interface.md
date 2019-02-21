---
title: 通信类接口
description: 通信类接口
ms.assetid: b0414d0e-6e1b-4d84-8ca4-40a59fb1b099
keywords:
- 通信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be9190ea105d99730974e2ad6140e5f96bad71a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546342"
---
# <a name="communication-class-interface"></a>通信类接口





通过 USB 接口描述符、 三个特定于类的描述符，并通知终结点的终结点描述符详细介绍了通信类接口。 通知终结点说明符是一个标准的 USB 中断类型在终结点说明符其**wMaxPacketSize**字段为 8 个字节。 下表定义通信类接口描述符的重要字段。

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
<th align="left">值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>5</p></td>
<td align="left"><p>bInterfaceClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>02 h</p></td>
<td align="left"><p>通信接口类代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>bInterfaceSubClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>02 h</p></td>
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

 

 

 





