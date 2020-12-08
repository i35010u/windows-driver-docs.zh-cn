---
title: 标准变量表达式
description: 标准变量表达式
keywords:
- 打印机命令 WDK Unidrv，字符串
- 命令字符串 WDK Unidrv
- 字符串 WDK Unidrv
- 标准变量表达式 WDK Unidrv
- max_repeat
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdea39834ef9672246b4c53f160ba522ea06ccd2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806865"
---
# <a name="standard-variable-expressions"></a>标准变量表达式





在命令字符串中指定参数时，可以将参数值指定为表达式。 此表达式可以使用 [标准变量](standard-variables.md)的当前值执行操作。 命令字符串内的每个标准变量表达式由大括号分隔 ( {，} ) 。

标准变量表达式可以包含以下组件的组合：

-   零个、一个或多个 [标准变量](standard-variables.md)

-   整数 [数值](numeric-values.md)

-   表达式运算符

标准变量表达式不能包含嵌入的宏引用。

表达式运算符包括在下表中。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>运算符</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Val1</em> <strong>+</strong><em>Val2</em></p></td>
<td><p>加。</p></td>
</tr>
<tr class="even">
<td><p><em>Val1</em> <strong>-</strong><em>Val2</em></p></td>
<td><p>减。</p></td>
</tr>
<tr class="odd">
<td><p><em>Val1</em> <strong>/</strong><em>Val2</em></p></td>
<td><p>除。</p></td>
</tr>
<tr class="even">
<td><p><em>Val1</em> <strong>*</strong><em>Val2</em></p></td>
<td><p>乘。</p></td>
</tr>
<tr class="odd">
<td><p><em>Val1</em><strong>MOD</strong><em>Val2</em></p></td>
<td><p>取模。 值是除以<em>Val2</em> <em>Val1</em>的余数。</p></td>
</tr>
<tr class="even">
<td><p><strong>max</strong> ( <em>Val1</em> ， <em>Val2</em> ) </p></td>
<td><p>最大值。 值是 <em>Val1</em> 和 <em>Val2</em>的最大值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>max_repeat</strong> ( <em>Val1</em> ) </p></td>
<td><p>请参阅 <strong>Using max_repeat</strong> 部分。</p></td>
</tr>
<tr class="even">
<td><p><strong>min</strong> ( <em>Val1</em> ， <em>Val2</em> ) </p></td>
<td><p>最小值。 值是 <em>Val1</em> 和 <em>Val2</em>的最小值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>( )</strong></p></td>
<td><p>优先运算符。 如果未使用，则使用 C 语言优先顺序。</p></td>
</tr>
</tbody>
</table>

 

标准变量表达式不会修改赋给标准变量的值。 使用 [命令字符串参数类型](command-string-argument-types.md) 说明符指定的格式将计算的值置于转义序列中。

### <a name="using-max_repeat"></a><a href="" id="ddk-using-max-repeat-gg"></a>使用 max \_ repeat

使用 **最大 \_ 重复** 效果的最佳方式是使用一个示例。 假设 GPD 文件包含以下条目：

```cpp
*Command:CmdXMoveRelRight{*Cmd:"<1B>["%d[0,9600]{max_repeat((DestXRel/4))}"a"}
```

此命令包含一个类型为 **% d** 的参数。 它还包含参数范围规范。 每当 Unidrv 将此命令发送到打印机时，它首先计算 DestXRel/4 并确定它是否在指定的范围内。 如果计算出的值大于9600，Unidrv 将重复发送命令，最大值为9600，直到发送指定的值。 因此，如果 DestXRel/4 等于20000，则 Unidrv 将发送以下命令：

```cpp
<1B>[9600
<1B>[9600
<1B>[800
```

仅当满足以下条件时，才能使用 **max \_ repeat** 运算符：

-   命令字符串只包含一个参数。

-   参数包括范围规范。

 

 




