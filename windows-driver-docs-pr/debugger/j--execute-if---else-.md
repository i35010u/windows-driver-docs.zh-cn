---
title: j（执行 If - Else）
description: J 命令有条件地执行一个指定命令，具体取决于给定表达式的计算。
ms.assetid: c6bb2415-e888-458b-8fb9-9d50b90cc531
keywords:
- j (如果执行-其他) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- j (Execute If - Else)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8030afbb9018c7063104c288c10ac46be94b6cc1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367227"
---
# <a name="j-execute-if---else"></a>j（执行 If - Else）


**J**命令有条件地执行一个指定命令，具体取决于给定表达式的计算。

```dbgcmd
j Expression Command1 ; Command2 
j Expression 'Command1' ; 'Command2' 
```

## <a name="span-idddkcmdexecuteifelsedbgspanspan-idddkcmdexecuteifelsedbgspanparameters"></a><span id="ddk_cmd_execute_if_else_dbg"></span><span id="DDK_CMD_EXECUTE_IF_ELSE_DBG"></span>参数


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *表达式*   
要计算的表达式。 此表达式的计算结果为非零值，如果*Command1*执行。 如果此表达式的计算结果为零， *Command2*执行。 此表达式的语法的详细信息，请参阅[数值表达式语法](numerical-expression-syntax.md)。

<span id="_______Command1______"></span><span id="_______command1______"></span><span id="_______COMMAND1______"></span> *Command1*   
如果要执行的命令字符串中的表达式*表达式*计算结果为非零值 (TRUE)。 可以通过命令将字符串用直单引号将合并多个命令 (  ) 并使用分号分隔的命令。 如果命令字符串是一条命令，单引号是可选的。

<span id="_______Command2______"></span><span id="_______command2______"></span><span id="_______COMMAND2______"></span> *Command2*   
如果要执行的命令字符串中的表达式*表达式*的计算结果为零 (FALSE)。 可以通过命令将字符串用直单引号将合并多个命令 (  ) 并使用分号分隔的命令。 如果命令字符串是一条命令，单引号是可选的。

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

不能添加分号或其他命令后的**j**命令。 如果之后出现分号*Command2*，忽略分号后面的所有内容。

下面的命令显示的值**eax**如果**MySymbol**等于零，并显示的值**ebx**并**ecx**否则为。

```dbgcmd
0:000> j (MySymbol=0) 'r eax'; 'r ebx; r ecx' 
```

可以省略单引号括**r eax**，但它们使命令更易于读取。 如果你想要忽略的命令之一，可以包括空引号或省略该命令，如以下命令中所示的参数。

```dbgcmd
0:000> j (MySymbol=0) ''; 'r ebx; r ecx' 
0:000> j (MySymbol=0)  ; 'r ebx; r ecx' 
```

此外可以使用**j**命令内的其他命令。 例如，可以使用**j**命令以创建条件断点。

```dbgcmd
0:000> bp `mysource.cpp:143` "j (poi(MyVar)>0n20) ''; 'gc' "
```

有关条件断点的语法的详细信息，请参阅[设置条件断点](setting-a-conditional-breakpoint.md)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**z （执行时）**](z--execute-while-.md)

 

 






