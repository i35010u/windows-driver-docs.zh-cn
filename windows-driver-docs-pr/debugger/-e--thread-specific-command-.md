---
title: ~e（线程特定的命令）
description: ~ E 命令目标进程中执行一个或多个命令在特定线程或所有线程。不要混淆此命令使用 e （输入值） 命令。
ms.assetid: a14f0a5f-48f9-46dd-baa6-b7d91b15772c
keywords:
- 特定于线程的命令 (~ 电子) 命令
- 线程特定于线程的命令 (~ 电子) 命令
- ~ e （特定于线程的命令） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~e (Thread-Specific Command)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 35ecb0d499b458c29a6211fe3a16711c72f314be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563115"
---
# <a name="e-thread-specific-command"></a>~e（线程特定的命令）


**~ E**目标进程中执行一个或多个命令在特定线程或所有线程。

不要将使用此命令相混淆[ **e （输入值）** ](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md)命令。

```dbgcmd
~Thread e CommandString
```

## <a name="span-idddkcmdthreadspecificcommanddbgspanspan-idddkcmdthreadspecificcommanddbgspanparameters"></a><span id="ddk_cmd_thread_specific_command_dbg"></span><span id="DDK_CMD_THREAD_SPECIFIC_COMMAND_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
指定的线程或线程，则调试器将执行*CommandString*的。 有关语法的详细信息，请参阅[线程语法](thread-syntax.md)。

<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
指定一个或多个要执行的命令。 应使用分号来分隔多个命令。 *CommandString*包含输入行的其余内容。 后面的字母"e"的文本的所有被解释为此字符串的一部分。 不能将放*CommandString*引号引起来。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>仅限用户模式</p></td>
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

有关其他命令的控制线程的详细信息，请参阅[控制进程和线程](controlling-processes-and-threads.md)。

<a name="remarks"></a>备注
-------

仅在用户模式下，可以指定线程。 在内核模式下颚化符 （~） 是指一个处理器。

当你使用 **~ 电子**命令及一个线程 **~ e**命令仅将保存键入一些内容。 例如，以下两个命令是等效的。

```dbgcmd
0:000> ~2e r; k; kd 

0:000> ~2r; ~2k; ~2kd 
```

但是，可以使用 **~ e**要重复的命令或扩展命令执行几次限定符。 当以这种方式使用限定符时，它可以消除额外劳动。 例如，以下命令重复[ **！ gle** ](-gle.md)正在调试的每个线程的扩展命令。

```dbgcmd
0:000> ~*e !gle 
```

如果一个命令的执行过程中发生错误，与下一个命令将继续执行。

不能使用 **~ 电子**限定符以及执行命令 ([**g**](g--go-.md)， [ **gh**](gh--go-with-exception-handled-.md)， [**gn**](gn--gn--go-with-exception-not-handled-.md)， **gN**， [ **gu**](gu--go-up-.md)， [ **p** ](p--step-.md)， [ **pa**](pa--step-to-address-.md)， [ **pc**](pc--step-to-next-call-.md)， [ **t**](t--trace-.md)， [**ta**](ta--trace-to-address-.md)， [ **tb**](tb--trace-to-next-branch-.md)， [ **tc**](tc--trace-to-next-call-.md)， [ **wt**](wt--trace-and-watch-data-.md))。

不能使用 **~ 电子**一起使用的限定符[ **j (执行 If-else)** ](j--execute-if---else-.md)或者[ **z （执行时）** ](z--execute-while-.md)条件性命令。

如果你正在调试多个进程，则无法使用 **~ e**命令访问处于非活动状态的进程的虚拟内存空间。

 

 





