---
title: .pcmd （set 提示命令）
description: .Pcmd 命令会使调试器发出命令，只要目标停止执行，并在注册或目标的状态信息的调试器命令窗口中显示的提示。
ms.assetid: 8cda10c3-860c-453d-9fdd-0dfc74d71c53
keywords:
- .pcmd （set 提示命令） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .pcmd (Set Prompt Command)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 25113801956a4519271aca0743b6dbfa9ffa6b2b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544155"
---
# <a name="pcmd-set-prompt-command"></a>.pcmd （set 提示命令）


**.Pcmd**命令将导致发出命令，只要目标停止执行并显示提示，可在调试器[调试器命令窗口](debugger-command-window.md)与注册或目标的状态信息。

```dbgcmd
.pcmd -s CommandString 
.pcmd -c 
.pcmd 
```

## <a name="span-idddkmetasetpromptcommanddbgspanspan-idddkmetasetpromptcommanddbgspanparameters"></a><span id="ddk_meta_set_prompt_command_dbg"></span><span id="DDK_META_SET_PROMPT_COMMAND_DBG"></span>参数


<span id="_______-s_______CommandString______"></span><span id="_______-s_______commandstring______"></span><span id="_______-S_______COMMANDSTRING______"></span> **-s** **** *CommandString*   
指定新的提示命令字符串。 目标时停止执行，调试器问题并立即运行*CommandString*命令。 如果*CommandString*包含空格或分号，则必须将其括在引号中。

<span id="_______-c______"></span><span id="_______-C______"></span> **-c**   
删除任何现有提示命令字符串。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关调试器的命令窗口提示的详细信息，请参阅[使用调试器命令](using-debugger-commands.md)。

<a name="remarks"></a>备注
-------

如果您使用 **.pcmd**不带参数，命令显示当前提示命令。

当使用设置提示命令 **.pcmd-s**，指定*CommandString*只要目标停止执行颁发 (例如，当[ **g**](g--go-.md)， [ **p**](p--step-.md)，或[ **t** ](t--trace-.md)命令结束)。 *CommandString*不时发出命令，使用非执行命令，除非该命令显示寄存器或目标的状态信息。

在以下示例中，使用的第一个 **.pcmd**设置显示的提示的固定的字符串。 第二个利用 **.pcmd**使调试器可以显示目标的当前进程 ID 和线程则提示将显示每个时间的 ID。 特殊提示符后未出现[ **.ttime** ](-ttime--display-thread-times-.md)使用命令，因为该命令不涉及执行。

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

 

 





