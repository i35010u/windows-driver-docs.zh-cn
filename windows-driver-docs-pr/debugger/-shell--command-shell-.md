---
title: .shell（命令 Shell）
description: Shell 命令启动 shell 进程，并将其输出重定向到调试器，或重定向到指定的文件。
keywords:
- 命令行界面 ( shell) 命令
- MS-DOS Shell ( shell) 命令
- DOS Shell ( shell) 命令
- shell 命令，命令行界面 ( 命令行界面) 命令
- shell (命令外壳) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .shell (Command Shell)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b6b59f1f314594c8f8283d341f84cdab52b22597
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838539"
---
# <a name="shell-command-shell"></a>.shell（命令 Shell）


**Shell** 命令启动 shell 进程，并将其输出重定向到调试器，或重定向到指定的文件。

```dbgcmd
.shell [Options] [ShellCommand] 
.shell -i InFile [-o OutFile [-e ErrFile]] [Options] ShellCommand
```

## <a name="span-idddk_meta_command_shell_dbgspanspan-idddk_meta_command_shell_dbgspanparameters"></a><span id="ddk_meta_command_shell_dbg"></span><span id="DDK_META_COMMAND_SHELL_DBG"></span>参数


<span id="_______InFile______"></span><span id="_______infile______"></span><span id="_______INFILE______"></span>*InFile*   
指定用于输入的文件的路径和文件名。 如果你打算在初始命令之后提供任何输入，则可以指定单个连字符 (-) 而不是 *InFile*，连字符前无空格。

<span id="_______OutFile______"></span><span id="_______outfile______"></span><span id="_______OUTFILE______"></span>*OutFile*   
指定要用于标准输出的文件的路径和文件名。 如果省略 **-o**  ****  *OutFile* ，则会将输出发送到调试器命令窗口。 如果你不希望在文件中显示或保存此输出，则可以指定单个连字符 (-) 而不是 *输出，连* 字符前无空格。

<span id="_______ErrFile______"></span><span id="_______errfile______"></span><span id="_______ERRFILE______"></span>*大错误 e*   
指定用于错误输出的文件的路径和文件名。 如果省略-e 大错误 e，则会将错误输出发送到与标准输出相同的位置。 如果你不希望在文件中显示或保存此输出，则可以指定单个连字符 (-) 而不是 *大错误 e*，连字符前无空格。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
可以是下列任意数量的选项：

<span id="-ci__Commands_"></span><span id="-ci__commands_"></span><span id="-CI__COMMANDS_"></span>**-ci "**<em>命令</em>**"**  
处理指定的调试器命令，然后将其输出作为输入文件传递给要启动的进程。 *命令* 可以是任意数量的调试器命令（用分号分隔），并用引号引起来。

<span id="-x"></span><span id="-X"></span>**-x**  
导致生成的任何进程都与调试器完全分离。 这允许您创建即使在调试会话结束后仍继续运行的进程。

<span id="_______ShellCommand______"></span><span id="_______shellcommand______"></span><span id="_______SHELLCOMMAND______"></span>*ShellCommand*   
指定要执行的应用程序命令行或 Microsoft MS-DOS 命令。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关访问命令行界面的其他方式，请参阅 [使用 Shell 命令](using-shell-commands.md)。

<a name="remarks"></a>备注
-------

将用户模式调试器的输出重定向到内核调试器时，不支持 **shell** 命令。 有关将输出重定向到内核调试器的详细信息 (有时称为 NTSD over KD) ，请参阅 [从内核调试器控制 User-Mode 调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。

即使包含分号) ， **shell** 命令后的整行也将被解释为 Windows 命令 (。 此行不应用引号引起来。 在 **. shell** 和 *ShellCommand* 之间必须有空格 (将忽略) 的其他前导空格。

除非使用 **-o**  ****  *OutFile* 参数，否则命令的输出将显示在调试器命令窗口中。

发出不带参数的 **shell** 命令将激活 shell 并使其保持打开状态。 所有后续命令将被解释为 Windows 命令。 在此期间，调试器将显示消息 "正在读取" **&lt; 。 shell 进程可能 &gt; 需要输入**，而 WinDbg 提示符将替换为 **输入 &gt;** 提示。 有时，当调试器使 shell 保持打开状态时，会显示一个单独的命令提示符窗口。 应忽略此窗口;所有输入和输出都是通过调试器命令窗口来完成的。

若要关闭此 shell 并返回到调试器本身，请键入 **exit** 或 **shell \_ quit**。  (**shell \_ quit** 命令的功能更强大，因为它即使 shell 已冻结也能正常工作。 ) 

调试 CSRSS 时不能使用此命令，因为在没有 CSRSS 处于活动状态的情况下，无法创建新进程。

您可以使用-ci 标志来运行一个或多个调试程序命令，然后将其输出传递到 shell 进程。 例如，可以使用以下命令将输出从 [**！ process 0 7**](-process.md) 命令传递到 Perl 脚本：

```dbgcmd
0:000> .shell -ci "!process 0 7" perl.exe parsemyoutput.pl 
```

 

 





