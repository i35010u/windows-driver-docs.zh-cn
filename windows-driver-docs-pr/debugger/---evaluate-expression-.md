---
title: （计算表达式）
description: 问号 ( ) 命令计算并显示表达式的值。请注意问号本身 ( ) 显示命令帮助。
keywords:
- ) Windows 调试 (计算表达式
ms.date: 03/30/2021
topic_type:
- apiref
api_name:
- (Evaluate Expression)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b6eec0092c5e9791de471837de4c46f57cb66efe
ms.sourcegitcommit: 83a11e69f7b175011d032a179e4cfa6d5ede9ac2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2021
ms.locfileid: "106113606"
---
# <a name="-evaluate-expression"></a>? （计算表达式）


问号 (**？**) 命令计算并显示表达式的值。

**注意**   问号会自行 ([**？**](---command-help-.md)) 显示命令帮助。 **?** *expression* 命令计算给定表达式的值。

```dbgcmd
    ? Expression
```

## <a name="parameters"></a>参数

*表达式*   
指定要计算的表达式。

### <a name="environment"></a>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

的输入和输出 **？** 命令取决于使用的是 MASM 表达式语法还是 c + + 表达式语法。 有关这些类型的表达式语法的详细信息，请参阅 [计算表达式](evaluating-expressions.md) 和 [数值表达式语法](numerical-expression-syntax.md)。

如果使用的是 MASM 语法，则输入和输出取决于当前的基数。 若要更改基数，请使用 [**n (设置 Number Base)**](n--set-number-base-.md) 命令。

**?** 命令在当前线程和进程的上下文中计算表达式中的符号。

某些字符串可能包含转义，如 **\\ n**、 **\\ "**、 **\\ r** 和 **\\ b**，它们应按原义读取，而不是由计算器解释。 如果由计算器解释字符串内的转义符，则会发生计算错误。 例如：

```console
0:000> as AliasName c:\dir\name.txt
0:000> al
  Alias            Value
 -------          -------
 AliasName        c:\dir\name.txt
0:001> ? $spat( "c:\dir\name.txt", "*name*" )
Evaluate expression: 0 = 00000000
0:001> ? $spat( "${AliasName}", "*name*" )
Evaluate expression: 0 = 00000000
0:001> ? $spat( "c:\dir\", "*filename*" )
Syntax error at '( "c:\dir\", "*filename*" )
```

在前两个示例中，尽管字符串与模式匹配，但计算返回的值为 **FALSE**。 在第三种情况下，计算器无法进行比较，因为字符串以反斜杠 ( \\ ) 结束，因此 **\\ "** 由计算器转换。

若要使计算器按字面解释字符串，必须使用 <strong>@ "</strong>*string*<strong>"</strong> 语法。 下面的代码示例演示正确的结果：

```console
0:000> ? $spat( @"c:\dir\name.txt", "*name*" )
Evaluate expression: 1 = 00000000`00000001
0:000> ? $spat( @"${AliasName}", "*name*" )
Evaluate expression: 1 = 00000000`00000001
0:001> ? $spat( @"c:\dir\", "*filename*" )
Evaluate expression: 0 = 00000000
```

在前面的示例中， **$spat** MASM 运算符检查第一个字符串，以确定它是否与第二个字符串的模式 (不) 区分大小写。 有关 MASM 运算符的详细信息，请参阅 [Masm 数字和运算符](masm-numbers-and-operators.md) 主题。

## <a name="see-also"></a>另请参阅

[**?? (评估 c + + 表达式)**](----evaluate-c---expression-.md)

[**.formats（显示数字格式）**](-formats--show-number-formats-.md)

[MASM 数字和运算符](masm-numbers-and-operators.md)

[C++ 数字和运算符](c---numbers-and-operators.md)

[MASM 表达式与C++ 表达式](masm-expressions-vs--c---expressions.md)

[混合表达式示例](expression-examples.md)
 

 






