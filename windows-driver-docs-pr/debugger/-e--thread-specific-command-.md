---
title: ~e（线程特定的命令）
description: ~ E 命令为特定线程或目标进程中的所有线程执行一个或多个命令。请勿将此命令与 e (将) 命令输入值。
keywords:
- Thread-Specific 命令 (~ e) 命令
- 线程，Thread-Specific 命令 (~ e) 命令
- ~ e (线程特定命令) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~e (Thread-Specific Command)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 93618ea4abeb5f8e555bd695510c888c30f8505e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799893"
---
# <a name="e-thread-specific-command"></a>~e（线程特定的命令）


**~ E** 命令为特定线程或目标进程中的所有线程执行一个或多个命令。

请勿将此命令与 [**e (将) 命令输入值**](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md) 。

```dbgcmd
~Thread e CommandString
```

## <a name="span-idddk_cmd_thread_specific_command_dbgspanspan-idddk_cmd_thread_specific_command_dbgspanparameters"></a><span id="ddk_cmd_thread_specific_command_dbg"></span><span id="DDK_CMD_THREAD_SPECIFIC_COMMAND_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
指定调试器将对其执行 *command.commandstring* 的一个或一些线程。 有关语法的详细信息，请参阅 [线程语法](thread-syntax.md)。

<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span>*Command.commandstring*   
指定要执行的一个或多个命令。 应使用分号分隔多个命令。 *Command.commandstring* 包括输入行的其余部分。 字母 "e" 后的所有文本将被解释为此字符串的一部分。 不要将 *command.commandstring* 用引号引起来。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅用户模式</p></td>
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

有关控制线程的其他命令的详细信息，请参阅 [控制进程和线程](controlling-processes-and-threads.md)。

<a name="remarks"></a>备注
-------

只能在用户模式下指定线程。 在内核模式下，颚化 (~) 引用处理器。

将 **~ e** 命令与一个线程一起使用时， **~ e** 命令仅保存某些键入内容。 例如，以下两个命令是等效的。

```dbgcmd
0:000> ~2e r; k; kd 

0:000> ~2r; ~2k; ~2kd 
```

但是，可以使用 **~ e** 限定符多次重复执行命令或扩展命令。 如果以这种方式使用限定符，则会消除额外的键入。 例如，下面的命令为要调试的每个线程重复 [**！ gle**](-gle.md) 扩展命令。

```dbgcmd
0:000> ~*e !gle 
```

如果执行一个命令时出错，则继续执行下一个命令。

不能将 **~ e** 限定符与执行命令一起使用， ([**g**](g--go-.md)， [**gh**](gh--go-with-exception-handled-.md)， [**gn**](gn--gn--go-with-exception-not-handled-.md)， **gn**， [**gu**](gu--go-up-.md)， [**p**](p--step-.md)， [**pa**](pa--step-to-address-.md)， [**pc**](pc--step-to-next-call-.md)， [**t**](t--trace-.md)， [**ta**](ta--trace-to-address-.md)， [**tb**](tb--trace-to-next-branch-.md)， [**tc**](tc--trace-to-next-call-.md)， [**wt**](wt--trace-and-watch-data-.md)) 。

如果) 条件命令，则不能将 **~ e** 限定符与 [**j (execute 一起使用（如果-Else)**](j--execute-if---else-.md) 或 [**z (执行**](z--execute-while-.md) ）。

如果正在调试多个进程，则不能使用 **~ e** 命令访问不活动进程的虚拟内存空间。

 

 





