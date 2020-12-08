---
title: .pcmd（设置提示命令）
description: Pcmd 命令使调试器在目标停止执行时发出命令，并在调试器中显示带有寄存器或目标状态信息的提示命令窗口。
keywords:
- pcmd (Set Prompt 命令) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .pcmd (Set Prompt Command)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 31ddcfa9c1db54de40c903d929fd6764daa6c3e0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792009"
---
# <a name="pcmd-set-prompt-command"></a>.pcmd（设置提示命令）


**Pcmd** 命令使调试器在目标停止执行时发出命令，并在调试器中显示带有寄存器或目标状态信息的提示 [命令窗口](debugger-command-window.md)。

```dbgcmd
.pcmd -s CommandString 
.pcmd -c 
.pcmd 
```

## <a name="span-idddk_meta_set_prompt_command_dbgspanspan-idddk_meta_set_prompt_command_dbgspanparameters"></a><span id="ddk_meta_set_prompt_command_dbg"></span><span id="DDK_META_SET_PROMPT_COMMAND_DBG"></span>参数


<span id="_______-s_______CommandString______"></span><span id="_______-s_______commandstring______"></span><span id="_______-S_______COMMANDSTRING______"></span>**-s**  **** *Command.commandstring*   
指定新的提示命令字符串。 每当目标停止执行时，调试器都会发出问题并立即运行 *command.commandstring* 命令。 如果 *command.commandstring* 包含空格或分号，则必须用引号将其引起来。

<span id="_______-c______"></span><span id="_______-C______"></span>**-c**   
删除任何现有的提示命令字符串。

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关调试器命令窗口提示符的详细信息，请参阅 [使用调试器命令](using-debugger-commands.md)。

<a name="remarks"></a>备注
-------

如果使用不带参数的 **pcmd** 命令，则会显示 "当前提示" 命令。

使用 **. pcmd-s** 设置 prompt 命令时，只要目标停止执行，就会发出指定的 *command.commandstring* (例如，当 [**g**](g--go-.md)、 [**p**](p--step-.md)或 [**t**](t--trace-.md) 命令结束时) 。 如果使用非执行命令，则不会发出 *command.commandstring* 命令，除非该命令显示寄存器或目标状态信息。

在下面的示例中，第一次使用 **。 pcmd** 设置一个与提示一起显示的固定字符串。 第二次使用时， **pcmd** 会使调试器在每次出现提示时显示目标的当前进程 id 和线程 id。 使用 [**ttime**](-ttime--display-thread-times-.md) 命令后，不会出现特殊提示，因为该命令不涉及执行。

```dbgcmd
0:000> .pcmd
No per-prompt command

0:000> .pcmd -s ".echo Execution is done."
Per-prompt command is '.echo Execution is done.'

0:000> t
Prymes!isPrime+0xd0:
004016c0 837dc400      cmp dword ptr [ebp-0x3c],0x0 ss:0023:0012fe70=00000002
Execution is done.

0:000> t
Prymes!isPrime+0xd4:
004016c4 7507             jnz     Prymes!isPrime+0xdd (004016cd)
 [br=1]
Execution is done.

0:000> .ttime
Created: Thu Aug 21 13:18:59 2003
Kernel:  0 days 0:00:00.031
User:    0 days 0:00:00.000

0:000> .pcmd -s "r $tpid, $tid"
Per-prompt command is 'r $tpid, $tid'

0:000> t
Prymes!isPrime+0xdd:
004016cd ebc0             jmp     Prymes!isPrime+0x9f (0040168f)
$tpid=0000080c $tid=00000514

0:000> t
Prymes!isPrime+0x9f:
0040168f 8b55fc           mov     edx,[ebp-0x4]     ss:0023:0012fea8=00000005
$tpid=0000080c $tid=00000514
```

 

 





