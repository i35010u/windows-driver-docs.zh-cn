---
title: （计算表达式）
description: 问号 （） 命令的计算结果，并显示表达式的值。注意问号本身 （） 显示命令的帮助。
ms.assetid: fae689b3-47c9-44bd-992d-8344805fb4b7
keywords:
- （计算表达式）Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- (Evaluate Expression)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0a3314967d8b9b9249a8c66ca0889ec536c90308
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337063"
---
# <a name="-evaluate-expression"></a>? （计算表达式）


问号 (**？**) 命令的计算结果并显示表达式的值。

**请注意**  本身的问号 ([**？**](---command-help-.md)) 显示命令的帮助。 **？** *表达式*命令计算给定的表达式的值。

```dbgcmd
    ? Expression
```

## <a name="span-idddkcmdevaluateexpressiondbgspanspan-idddkcmdevaluateexpressiondbgspanparameters"></a><span id="ddk_cmd_evaluate_expression_dbg"></span><span id="DDK_CMD_EVALUATE_EXPRESSION_DBG"></span>参数


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *表达式*   
指定要计算的表达式。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

输入和输出 **？** 命令取决于是否使用 MASM 表达式语法或C++表达式语法。 有关这些类型的表达式语法的详细信息，请参阅[评估表达式](evaluating-expressions.md)并[数值表达式语法](numerical-expression-syntax.md)。

如果使用 MASM 语法，输入和输出取决于当前的基数。 若要更改的基数，请使用[ **n (设置数量 Base)** ](n--set-number-base-.md)命令。

**？** 命令可评估当前的线程和进程的上下文中的表达式中的符号。

某些字符串可能包含转义符，如 **\\n**，  **\\"**，  **\\r**，并 **\\b**，，是应按字面意思读取而不是解释计算器。 如果在字符串内的转义解释计算器，可能会出现在计算中的错误。 例如：

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

在前两个示例中，即使字符串与模式匹配，计算器返回的值**FALSE**。 在第三，则计算器无法进行的比较由于一个反斜杠结尾的字符串 ( \\ )，因此 **\\"** 计算器转换。

若要获取的字符串按原义解释该计算器，必须使用<strong>@"</strong>*字符串*<strong>"</strong>语法。 下面的代码示例显示了正确的结果：

```console
0:000> ? $spat( @"c:\dir\name.txt", "*name*" )
Evaluate expression: 1 = 00000000`00000001
0:000> ? $spat( @"${AliasName}", "*name*" )
Evaluate expression: 1 = 00000000`00000001
0:001> ? $spat( @"c:\dir\", "*filename*" )
Evaluate expression: 0 = 00000000
```

在上述示例中， **$spat** MASM 运算符检查以确定它与匹配 （不区分大小写） 的第一个字符串的第二个字符串的模式。 有关 MASM 运算符的详细信息，请参阅[MASM 数字和运算符](masm-numbers-and-operators.md)主题。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**??(评估C++表达式)**](----evaluate-c---expression-.md)

[**.formats （显示数字格式）**](-formats--show-number-formats-.md)

 

 






