---
title: 命令字符串自变量类型
description: 命令字符串自变量类型
ms.assetid: c7540c3f-265a-4fee-aca9-b8cc10b6be8f
keywords:
- 打印机命令 WDK Unidrv，字符串
- 命令字符串 WDK Unidrv
- 字符串 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1823c4ded01c59c03bbd92e3223b1756350b0da9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526654"
---
# <a name="command-string-argument-types"></a>命令字符串自变量类型





如果命令字符串中包含参数，必须指定每个自变量的类型。 每个自变量类型规范是一个字母，以百分比符号开头。

下表列出了所有参数的类型说明符。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数类型说明符</th>
<th>生成的值的说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>%&lt;<em>位数</em>&gt;d</p></td>
<td><p>ASCII 字符串，表示一个十进制值，包括一个减号，如果为负数。 <em>&lt;位数&gt;</em>是可选的数字，指示字符串长度。</p></td>
</tr>
<tr class="even">
<td><p>%&lt;<em>位数</em>&gt;D</p></td>
<td><p>ASCII 字符串表示十进制值，包括一个加号或减号。 <em>&lt;位数&gt;</em>是可选的数字，指示字符串长度。</p></td>
</tr>
<tr class="odd">
<td><p>%c</p></td>
<td><p>二进制字节。</p></td>
</tr>
<tr class="even">
<td><p>%C</p></td>
<td><p>添加到 ASCII 的二进制字节&quot;0&quot;。</p></td>
</tr>
<tr class="odd">
<td><p>%f</p></td>
<td><p>无符号的 ASCII 字符串，表示带插入为从右、 从第三个字符作为中的小数点的十进制值， &quot;12.25&quot;。</p></td>
</tr>
<tr class="even">
<td><p>%g</p></td>
<td><p>2 * ABS (<em>参数</em>) + IS_NEGATIVE (<em>参数</em>) 到最高有效位 base-64 number，最低有效位数字。 由字节到 254 191 表示最高有效位 （0 到 63 个）。 所有其他数字表示由字节 63 到 126。 &quot;IS_NEGATIVE (<em>参数</em>)&quot;为 1，如果<em>参数</em>是负数，否则不进行任何。</p></td>
</tr>
<tr class="odd">
<td><p>%l</p></td>
<td><p>二进制文件，word，最低有效字节第一次。</p></td>
</tr>
<tr class="even">
<td><p>%m</p></td>
<td><p>二进制文件，word，最高有效字节第一次。</p></td>
</tr>
<tr class="odd">
<td><p>%n</p></td>
<td><p>Canon 整数编码。 从最高有效字节编码为最低有效字节的二进制值。 4 的最低有效位编码为 001<em>sbbbb</em>，其中<em>s</em>表示符号 （0 为负，1 为正），并且<em>b</em>表示的整数的有效位。 下一步最重要的 6 位编码为 01<em>bbbbbb</em>。 例如，254 (11111110) 表示为 (01001111 00111110)。</p></td>
</tr>
<tr class="even">
<td><p>%q</p></td>
<td><p>表示 QUME 十六进制数的 ASCII 字符串。 对于 Toshiba/Qume 设备。</p></td>
</tr>
<tr class="odd">
<td><p>%v</p></td>
<td><p>NEC VFU （垂直格式单元） 编码。 指定的变量&#39;s 值除以 1/6 英寸。 结果是 VFU 数据发送到打印机的次数。</p></td>
</tr>
</tbody>
</table>

 

可以指定一系列可接受任何参数的值。 为此，请通过将它们放置在一组方括号内包括参数的最小和最大值 ( \[， \] )、 立即以下参数的类型说明符，并由逗号分隔值。 例如，以下命令指定 0 到 255 之间 LinefeedSpacing/2 的值的可接受范围为：

```cpp
*Command:CmdSetLineSpacing{*Cmd:"<1B>3"%c[0,255]{(LinefeedSpacing/2)}}
```

 

 




