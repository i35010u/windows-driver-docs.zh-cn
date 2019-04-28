---
title: .shell（命令 Shell）
description: .Shell 命令启动外壳进程，并将其输出重定向到调试器，或指定的文件。
ms.assetid: 351cbd54-6e1a-4dc1-b0d8-8e61294b0e86
keywords:
- 命令外壳 (.shell) 命令
- MS-DOS 外壳 (.shell) 命令
- DOS 命令行程序 (.shell) 命令
- shell 命令，命令行界面 (.shell) 命令
- .shell （命令行界面） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .shell (Command Shell)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 24774ef64bb31b80eb473bee91ccf4b35cfb5068
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339780"
---
# <a name="shell-command-shell"></a>.shell（命令 Shell）


**.Shell**命令启动外壳进程，并将其输出重定向到调试器，或指定的文件。

```dbgcmd
.shell [Options] [ShellCommand] 
.shell -i InFile [-o OutFile [-e ErrFile]] [Options] ShellCommand
```

## <a name="span-idddkmetacommandshelldbgspanspan-idddkmetacommandshelldbgspanparameters"></a><span id="ddk_meta_command_shell_dbg"></span><span id="DDK_META_COMMAND_SHELL_DBG"></span>参数


<span id="_______InFile______"></span><span id="_______infile______"></span><span id="_______INFILE______"></span> *InFile*   
指定要用于输入的文件路径和文件名。 如果你想要在初始命令后提供任何输入，则可以指定一个连字符 （-） 而不是*InFile*，连字符前没有空格。

<span id="_______OutFile______"></span><span id="_______outfile______"></span><span id="_______OUTFILE______"></span> *OutFile*   
指定要使用的标准输出文件的路径和文件。 如果 **-o** **** *OutFile*是省略，输出将发送到调试器命令窗口。 如果不希望显示的或在文件中保存此输出，则可以指定一个连字符 （-），而不是*OutFile*，连字符前没有空格。

<span id="_______ErrFile______"></span><span id="_______errfile______"></span><span id="_______ERRFILE______"></span> *ErrFile*   
指定要用于错误输出的文件路径和文件名。 如果省略-e 大，则错误输出将发送到标准输出的同一位置。 如果不希望显示的或在文件中保存此输出，则可以指定一个连字符 （-），而不是*大*，连字符前没有空格。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
可以是任意数量的以下选项：

<span id="-ci__Commands_"></span><span id="-ci__commands_"></span><span id="-CI__COMMANDS_"></span>**-ci "**<em>Commands</em>**"**  
处理指定的调试程序命令，然后将其输出作为输入文件传递给正在启动的进程。 *命令*可以是任意数量的调试器命令由分号隔开，并括在引号内。

<span id="-x"></span><span id="-X"></span>**-x**  
会导致正在生成要从调试器完全分离的任何进程。 这使您可以创建的进程将继续运行，甚至在调试会话后结束。

<span id="_______ShellCommand______"></span><span id="_______shellcommand______"></span><span id="_______SHELLCOMMAND______"></span> *ShellCommand*   
指定应用程序命令行或要执行 Microsoft MS-DOS 命令。

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

访问命令行界面的其他方式，请参阅[使用 Shell 命令](using-shell-commands.md)。

<a name="remarks"></a>备注
-------

**.Shell**用户模式下调试程序的输出重定向到内核调试程序时，不支持命令。 将输出重定向到内核调试器 （有时通过 KD 称为 NTSD） 的详细信息，请参阅[控制用户模式下调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。

后面的整个行 **.shell** （即使它包含分号） 命令将解释为 Windows 命令。 此行不应该用括起来。 必须有之间有空格 **.shell**并*ShellCommand* （忽略其他前导空格）。

在调试器命令窗口中，会显示该命令的输出，除非 **-o** **** *OutFile*使用参数。

发出 **.shell**不带任何参数的命令将激活 shell 并使其保持打开状态。 所有后续命令将被解释为 Windows 命令。 在此期间，调试器将显示一个消息读取 **&lt;.shell 过程可能需要输入&gt;**，并将替换为提示符 WinDbg**输入&gt;** 提示。 有时，调试器使外壳程序保持打开状态时，将显示一个单独的命令提示符窗口。 应忽略此窗口;所有输入和输出将通过调试器命令窗口。

若要关闭此外壳，并返回给调试器本身，请键入**退出**或 **.shell\_退出**。 ( **.Shell\_退出**命令，功能更强大，因为它仍可正常工作外壳处于冻结状态。)

不能同时调试 CSRSS，使用此命令，因为没有活动的 CSRSS 的情况下无法创建新进程。

-Ci 标志可用于运行一个或多个调试器命令，然后将其输出传递至外壳进程。 例如，无法传递的输出[ **！ 处理 0 7** ](-process.md)命令 Perl 脚本使用以下命令：

```dbgcmd
0:000> .shell -ci "!process 0 7" perl.exe parsemyoutput.pl 
```

 

 





