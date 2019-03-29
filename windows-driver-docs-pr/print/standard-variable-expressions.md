---
title: 标准变量表达式
description: 标准变量表达式
ms.assetid: b77c6b88-9ef2-4485-b77c-50acb21e13b9
keywords:
- 打印机命令 WDK Unidrv，字符串
- 命令字符串 WDK Unidrv
- 字符串 WDK Unidrv
- 标准变量表达式 WDK Unidrv
- max_repeat
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7117dd8b674d5877b75d6c5ee677b2f522813910
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576215"
---
# <a name="standard-variable-expressions"></a>标准变量表达式





当在命令字符串中指定参数时，可以作为表达式来指定参数值。 此表达式可以使用执行操作的当前值[标准变量](standard-variables.md)。 由大括号 （{，}） 分隔命令字符串中的每个标准变量表达式。

标准变量表达式可以包含以下组件的组合：

-   零、 一个或多个[标准变量](standard-variables.md)

-   整数[数字值](numeric-values.md)

-   表达式运算符

标准变量表达式不能包含嵌入的宏的引用。

下表中包含的表达式运算符。

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
<td><p><em>Val1</em><strong>+</strong><em>Val2</em></p></td>
<td><p>添加。</p></td>
</tr>
<tr class="even">
<td><p><em>Val1</em><strong>-</strong><em>Val2</em></p></td>
<td><p>减法。</p></td>
</tr>
<tr class="odd">
<td><p><em>Val1</em><strong>/</strong><em>Val2</em></p></td>
<td><p>除。</p></td>
</tr>
<tr class="even">
<td><p><em>Val1</em><strong>*</strong><em>Val2</em></p></td>
<td><p>乘法。</p></td>
</tr>
<tr class="odd">
<td><p><em>Val1</em><strong>MOD</strong><em>Val2</em></p></td>
<td><p>取模。 值是后所得的余数<em>Val1</em>通过<em>Val2</em>。</p></td>
</tr>
<tr class="even">
<td><p><strong>max</strong> ( <em>Val1</em> , <em>Val2</em> )</p></td>
<td><p>最大值。 值为的最大<em>Val1</em>并<em>Val2</em>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>max_repeat</strong> ( <em>Val1</em> )</p></td>
<td><p>请参阅<strong>使用 max_repeat</strong>部分。</p></td>
</tr>
<tr class="even">
<td><p><strong>min</strong> ( <em>Val1</em> , <em>Val2</em> )</p></td>
<td><p>最小值。 值为的最小<em>Val1</em>并<em>Val2</em>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>( )</strong></p></td>
<td><p>优先运算符。 如果未使用，则使用 C 语言的优先级。</p></td>
</tr>
</tbody>
</table>

 

标准变量表达式不要修改分配给标准变量的值。 计算的值将放入使用指定的格式的转义序列[命令字符串自变量类型](command-string-argument-types.md)说明符。

### <a href="" id="ddk-using-max-repeat-gg"></a>使用最大\_重复

利用**最大\_重复**很好地解释通过一个示例。 假设 GPD 文件包含以下条目：

```cpp
*Command:CmdXMoveRelRight{*Cmd:"<1B>["%d[0,9600]{max_repeat((DestXRel/4))}"a"}
```

此命令包含类型的单个参数 **%d**。 它还包含参数范围规范。 每当 Unidrv 将此命令发送到打印机，它首先计算 DestXRel/4 并确定它是否在指定范围内。 如果计算的值是否大于 9600，Unidrv 发送该命令重复 9600，直到指定的值已发送的最大值。 因此如果 DestXRel/4 等于 20,000，Unidrv 发送以下命令：

```cpp
<1B>[9600
<1B>[9600
<1B>[800
```

**最大\_重复**仅当满足以下条件时，可以使用运算符：

-   命令字符串包含一个自变量。

-   参数将包含范围规范。

 

 




