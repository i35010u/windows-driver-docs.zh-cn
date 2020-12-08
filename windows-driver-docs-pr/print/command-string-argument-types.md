---
title: 命令字符串参数类型
description: 命令字符串参数类型
keywords:
- 打印机命令 WDK Unidrv，字符串
- 命令字符串 WDK Unidrv
- 字符串 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 366814d40a1ccfdaab93ac0df9e693a7585748d0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797645"
---
# <a name="command-string-argument-types"></a>命令字符串参数类型





如果在命令字符串中包含参数，则必须指定每个参数的类型。 每个参数类型规范均为一个字母，前面有一个百分号。

下表列出了所有参数类型说明符。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数类型说明符</th>
<th>结果值的说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>%&lt;<em>位数</em> &gt;2-d</p></td>
<td><p>表示十进制值的 ASCII 字符串，其中包括负号。 <em> &lt; 数字 &gt; </em>是指示字符串长度的可选数字。</p></td>
</tr>
<tr class="even">
<td><p>%&lt;<em>位数</em> &gt;2-d</p></td>
<td><p>表示十进制值的 ASCII 字符串，包括加号或减号。 <em> &lt; 数字 &gt; </em>是指示字符串长度的可选数字。</p></td>
</tr>
<tr class="odd">
<td><p>% c</p></td>
<td><p>二进制字节。</p></td>
</tr>
<tr class="even">
<td><p>% C</p></td>
<td><p>二进制字节已添加到 ASCII "0"。</p></td>
</tr>
<tr class="odd">
<td><p>% f</p></td>
<td><p>表示十进制值的无符号 ASCII 字符串，其中小数点作为第三个字符插入到右侧，如 "12.25"。</p></td>
</tr>
<tr class="even">
<td><p>% g</p></td>
<td><p>2 * ABS (<em>参数</em>) + IS_NEGATIVE (<em>参数</em>) 作为64的数字，最小的有效位数为最高有效位。 最有效的数字 (0-63) 由字节191到254表示。 所有其他数字用字节63到126表示。 如果<em>参数</em>为负，则 "IS_NEGATIVE (<em>参数</em>) " 为1，否则为零。</p></td>
</tr>
<tr class="odd">
<td><p>% l</p></td>
<td><p>二进制单词，首先是最小有效字节。</p></td>
</tr>
<tr class="even">
<td><p>% m</p></td>
<td><p>二进制单词，最高有效字节。</p></td>
</tr>
<tr class="odd">
<td><p>% n</p></td>
<td><p>Canon 整数编码。 从最高有效字节到最低有效字节编码的二进制值。 4个最小有效位编码为 001<em>sbbbb</em>，其中 <em>s</em> 表示符号 (0 为负数，1表示正负) ， <em>b</em> 表示整数的有效位。 接下来的最重要6位编码为 01<em>bbbbbb</em>。 例如，254 (11111110) 表示为 (01001111 00111110) 。</p></td>
</tr>
<tr class="even">
<td><p>% q</p></td>
<td><p>表示 QUME 十六进制数的 ASCII 字符串。 对于 Toshiba/Qume 设备。</p></td>
</tr>
<tr class="odd">
<td><p>% v</p></td>
<td><p>NEC VFU (垂直格式单位) 编码。 指定的变量的值除以1/6 英寸。 结果是向打印机发送 VFU 数据的次数。</p></td>
</tr>
</tbody>
</table>

 

可以为任何参数指定可接受值的范围。 为此，请将参数的最小值和最大值放在一组方括号中， ( \[ ， \] ) ，紧跟自变量类型说明符，然后用逗号分隔这些值。 例如，以下命令将0到255指定为 LinefeedSpacing/2 的值的可接受范围：

```cpp
*Command:CmdSetLineSpacing{*Cmd:"<1B>3"%c[0,255]{(LinefeedSpacing/2)}}
```

 

 




