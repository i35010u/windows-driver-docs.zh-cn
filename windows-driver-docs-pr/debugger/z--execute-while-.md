---
title: z （执行时）
description: 给定的条件为 true 时，z 命令执行的命令。
ms.assetid: 075dc012-68c2-4172-9d37-57bc8358297c
keywords:
- z （执行时） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- z (Execute While)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 24447078209a4c97c2d359c9ccf1b3c9c1974d93
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524426"
---
# <a name="z-execute-while"></a>z （执行时）


**Z**命令在给定的条件为 true 时执行的命令。

User-Mode

```dbgcmd
Command ; z( Expression ) 
```

Kernel-Mode

```dbgcmd
Command ; [Processor] z( Expression )
```

## <a name="span-idddkcmdexecutewhiledbgspanspan-idddkcmdexecutewhiledbgspanparameters"></a><span id="ddk_cmd_execute_while_dbg"></span><span id="DDK_CMD_EXECUTE_WHILE_DBG"></span>参数


<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span> *命令*   
指定要执行的命令时*表达式*条件的计算结果为非零值。 始终至少一次执行此命令。

<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *Processor*   
指定适用于测试的处理器。 有关语法的详细信息，请参阅[包含多个处理器语法](multiprocessor-syntax.md)。 仅在内核模式下，可以指定处理器。

<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *表达式*   
指定要测试的条件。 如果此条件计算结果为非零值，*命令*再次执行命令，然后*表达式*再次测试。 有关语法的详细信息，请参阅[数值表达式语法](numerical-expression-syntax.md)。

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

在许多调试器命令中，分号用于分隔不相关的命令。 但是，在**z**命令，以分号分隔，"z"从*命令*参数。

*命令*始终至少一次，执行命令，然后*表达式*进行测试。 如果条件为非零值，再次执行该命令，然后*表达式*再次测试。 (此行为是类似于 C 语言**do-** 循环，不是简单**虽然**循环。)

如果有多个分号"z"的左侧，所有命令到"z"的重复为 long 类型的值作为左*表达式*条件为 true。 此类命令可以是任何允许终端分号的调试器命令。

如果您添加另一个分号和其他命令后的**z**命令时，该循环完成后执行以下附加命令。 我们通常不建议以"z"开头，因为它会生成不相关的输出永远除非条件变为 false 由于某些其他操作的行。 请注意，您可以嵌套**z**命令。

若要中断循环继续的时间太长，请使用[ **CTRL + C** ](ctrl-c--break-.md) CDB 或 KD，或使用[调试 |中断](debug---break.md)或 CTRL + BREAK 在 WinDbg 中。

下面的代码示例显示了不必要地复杂的方式为零**eax**注册。

```dbgcmd
0:000> reax = eax - 1 ; z(eax)
```

下面的示例递增**eax**并**ebx**注册直到其中一个为至少 8，并且然后递增**ecx**注册一次。

```dbgcmd
0:000> reax=eax+1; rebx=ebx+1; z((eax<8)|(ebx<8)); recx=ecx+1
```

下面的示例使用 c + + 表达式语法，并使用伪寄存器**美元 t0**作为循环变量。

```dbgcmd
0:000> .expr /s c++
Current expression evaluator: C++ - C++ source expressions

0:000> db pindexcreate[@$t0].szKey; r$t0=@t0+1; z( @$t0 < cIndexCreate )
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**j （执行 If Else）**](j--execute-if---else-.md)

 

 






