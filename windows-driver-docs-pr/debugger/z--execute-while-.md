---
title: z（执行 While）
description: 当给定的条件为 true 时，z 命令执行命令。
keywords:
- ) Windows 调试时执行 z (
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- z (Execute While)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b89f6028dc72423462d4a863dd20bc9c0532403b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802709"
---
# <a name="z-execute-while"></a>z（执行 While）


当给定的条件为 true 时， **z** 命令执行命令。

User-Mode

```dbgcmd
Command ; z( Expression ) 
```

Kernel-Mode

```dbgcmd
Command ; [Processor] z( Expression )
```

## <a name="span-idddk_cmd_execute_while_dbgspanspan-idddk_cmd_execute_while_dbgspanparameters"></a><span id="ddk_cmd_execute_while_dbg"></span><span id="DDK_CMD_EXECUTE_WHILE_DBG"></span>参数


<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span>*命令*   
指定在 *表达式* 条件的计算结果为非零值时要执行的命令。 此命令始终执行至少一次。

<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*处理器*   
指定适用于测试的处理器。 有关语法的详细信息，请参阅 [多处理器语法](multiprocessor-syntax.md)。 只能在内核模式下指定处理器。

<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span>*表达式*   
指定要测试的条件。 如果此条件的计算结果为非零值，则会再次执行 *命令* 命令，然后再次测试 *表达式* 。 有关语法的详细信息，请参阅 [数值表达式语法](numerical-expression-syntax.md)。

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

在许多调试器命令中，分号用于分隔不相关的命令。 但是，在 **z** 命令中，分号将 "z" 与 *命令* 参数隔开。

*命令* 命令始终执行至少一次，然后对 *表达式* 进行测试。 如果条件为非零值，则再次执行该命令，然后再次测试 *表达式* 。  (此行为类似于 C 语言的 **do while** 循环，而不是简单的 **while** 循环。 ) 

如果 "z" 的左侧有几个分号，则只要 *表达式* 条件为 true，就会重复 "z" 左侧的所有命令。 此类命令可以是任何允许终端分号的调试器命令。

如果在 **z** 命令后面添加另一个分号和其他命令，则在循环完成后，将执行这些附加命令。 通常不建议以 "z" 开头的行，因为它会永久生成不需要的输出，除非由于其他操作而导致条件变为 false。 请注意，可以嵌套 **z** 命令。

若要中断持续时间太长的循环，请在 CDB 或 KD 中使用 [**CTRL + C**](ctrl-c--break-.md) ，或使用 " [调试" |](debug---break.md) 在 WinDbg 中中断或 CTRL + break。

下面的代码示例演示了一种不太复杂的非 **eax** 注册方法。

```dbgcmd
0:000> reax = eax - 1 ; z(eax)
```

下面的示例将递增 **eax** 和 **ebx** 寄存器，直到其中一个寄存器至少为8，然后将 **ecx** 寄存器递增一次。

```dbgcmd
0:000> reax=eax+1; rebx=ebx+1; z((eax<8)|(ebx<8)); recx=ecx+1
```

下面的示例使用 c + + 表达式语法，并使用伪寄存器 **$t 0** 作为循环变量。

```dbgcmd
0:000> .expr /s c++
Current expression evaluator: C++ - C++ source expressions

0:000> db pindexcreate[@$t0].szKey; r$t0=@t0+1; z( @$t0 < cIndexCreate )
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**j (执行 If-Else)**](j--execute-if---else-.md)

 

 






