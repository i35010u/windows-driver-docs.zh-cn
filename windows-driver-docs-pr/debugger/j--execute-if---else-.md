---
title: j（执行 If - Else）
description: J 命令有条件地执行指定的命令之一，具体取决于给定表达式的计算。
keywords:
- j) Windows 调试时执行 j (
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- j (Execute If - Else)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 16d07ebc7b75bf5c0f68f428467f4757b94a3aae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801941"
---
# <a name="j-execute-if---else"></a>j（执行 If - Else）


**J** 命令有条件地执行指定的命令之一，具体取决于给定表达式的计算。

```dbgcmd
j Expression Command1 ; Command2 
j Expression 'Command1' ; 'Command2' 
```

## <a name="span-idddk_cmd_execute_if_else_dbgspanspan-idddk_cmd_execute_if_else_dbgspanparameters"></a><span id="ddk_cmd_execute_if_else_dbg"></span><span id="DDK_CMD_EXECUTE_IF_ELSE_DBG"></span>参数


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span>*表达式*   
要计算的表达式。 如果此表达式的计算结果为非零值，则执行 *command1.enabled* 。 如果此表达式的计算结果为零，则执行 *Command2* 。 有关此表达式的语法的详细信息，请参阅 [数值表达式语法](numerical-expression-syntax.md)。

<span id="_______Command1______"></span><span id="_______command1______"></span><span id="_______COMMAND1______"></span>*Command1.enabled*   
如果 *表达式* 中的表达式的计算结果为非零值 (TRUE) ，则为要执行的命令字符串。 可以通过在命令字符串两侧加上直引号 ( **"** ) 并使用分号分隔命令来合并多个命令。 如果命令字符串是单个命令，则单引号是可选的。

<span id="_______Command2______"></span><span id="_______command2______"></span><span id="_______COMMAND2______"></span>*Command2*   
如果 *表达式* 中的表达式的计算结果为零，则为要执行的命令字符串 (FALSE) 。 可以通过在命令字符串两侧加上直引号 ( **"** ) 并使用分号分隔命令来合并多个命令。 如果命令字符串是单个命令，则单引号是可选的。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
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

**J** 命令后面不能添加分号或其他命令。 如果在 *Command2* 之后出现分号，则忽略分号后面的所有内容。

以下命令显示 **eax** 的值（如果 **MySymbol** 等于零，并显示 **ebx** 和 **ecx** 的值，否则为。

```dbgcmd
0:000> j (MySymbol=0) 'r eax'; 'r ebx; r ecx' 
```

可以省略 **r eax** 附近的单引号，但使命令更易于读取。 如果你想要省略其中一个命令，则可以包含空引号或省略该命令的参数，如以下命令中所示。

```dbgcmd
0:000> j (MySymbol=0) ''; 'r ebx; r ecx' 
0:000> j (MySymbol=0)  ; 'r ebx; r ecx' 
```

你还可以在其他命令中使用 **j** 命令。 例如，可以使用 **j** 命令创建条件断点。

```dbgcmd
0:000> bp `mysource.cpp:143` "j (poi(MyVar)>0n20) ''; 'gc' "
```

有关条件断点语法的详细信息，请参阅 [设置条件断点](setting-a-conditional-breakpoint.md)。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**z（执行 While）**](z--execute-while-.md)

 

 






