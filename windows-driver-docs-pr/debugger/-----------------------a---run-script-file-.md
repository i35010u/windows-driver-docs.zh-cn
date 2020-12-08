---
title: '$，$，$ $，$ $，$ $ a (运行脚本文件) '
description: $，$，$ $，$ $ 和 $ $ a 命令读取指定脚本文件的内容，并将其内容用作调试器命令输入。
keywords:
- $ () 命令运行脚本文件
- $ $ () 命令运行脚本文件
- $ $ () 命令运行脚本文件
- " ($ ) 命令运行脚本文件"
- " ($ ) 命令运行脚本文件"
- " ($ $ ) 命令运行脚本文件"
- 运行脚本文件 ($ $ ) 通信
- $，$，$ $，$ $，$ $ a (运行脚本文件) Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- $ , $ , $$ , $$ , $$ a (Run Script File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 79a3ec75a2c76ecdb0f8f7df1bdb499d602f3b1f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800239"
---
# <a name="-----a-run-script-file"></a>$<、$><、$$<、$$><、$$ >a<（运行脚本文件）


**$&lt;**、、 **$&gt;&lt;** 、 **$$&lt;** **$$&gt;&lt;** **$$ &gt; 和 &lt;** 命令读取指定脚本文件的内容，并将其内容用作调试器命令输入。

```dbgcmd
    $<Filename 
    $><Filename 
    $$<Filename 
    $$><Filename 
    $$>a<Filename [arg1 arg2 arg3 ...] 
```

## <a name="span-idddk_cmd_run_script_file_dbgspanspan-idddk_cmd_run_script_file_dbgspanparameters"></a><span id="ddk_cmd_run_script_file_dbg"></span><span id="DDK_CMD_RUN_SCRIPT_FILE_DBG"></span>参数


<span id="_______Filename______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span>*Filename*   
指定包含有效调试器命令文本的文件。 文件名必须遵循 Microsoft Windows 文件名约定。 文件名可以包含空格。

<span id="_______argn______"></span><span id="_______ARGN______"></span>*argn*   
指定调试器要传递到脚本的任意数量的字符串参数。 在执行脚本之前，调试器会将脚本文件中的任何格式为 $ {$arg *n*} 的字符串替换为相应的 *argn* 。 参数不能包含引号或分号。 必须用空格分隔多个参数;如果参数包含空格，则必须用引号将其引起来。 所有参数均为可选。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>模式</p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p>目标</p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p>平台</p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**$$&lt;** 和 **$&lt;** 令牌按原义执行脚本文件中的命令。 但是， **$&lt;** 您可以指定任何文件名，包括包含分号的任何文件名。 由于 **$&lt;** 允许在文件名中使用分号，因此不能 **$&lt;** 与其他调试器命令连接，因为分号不能同时用作命令分隔符和文件名的一部分。

**$$&gt;&lt;** 和 **$&gt;&lt;** 令牌按原义执行脚本文件中的命令，这意味着它们会打开脚本文件，将所有回车返回替换为分号，并将生成的文本作为单个命令块执行。 如 **$&lt;** 前面所述， **$&gt;&lt;** 变体允许文件名包含分号，这意味着不能 **$&gt;&lt;** 与其他调试器命令连接。

**$$&gt;&lt;** 如果正在 **$&gt;&lt;** 运行包含调试器命令程序的脚本，则和令牌非常有用。 有关这些程序的详细信息，请参阅 [使用调试器命令程序](using-debugger-command-programs.md)。

除非文件名包含分号，否则不需要使用 **$&lt;** 或 **$&gt;&lt;** 。

标记 **允许调试器将参数传递给脚本。 $$ &gt; &lt;** 如果 *Filename* 包含空格，则必须用引号将其引起来。 如果提供的参数过多，将忽略多余的参数。 如果提供的参数太少，则源文件中形式为 $ {$arg *n*} 的任何标记（其中 *n* 大于提供的参数的数量）将保留为其文本形式，并且不会替换为任何内容。 可以在此命令后面加上分号和其他命令;存在分号会终止参数列表。

调试器执行脚本文件时，命令及其输出会显示在 [调试器命令窗口](debugger-command-window.md)中。 当到达脚本文件的末尾时，控件将返回到调试器。

下表总结了如何使用这些令牌。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Token</th>
<th align="left">允许包含分号的文件名</th>
<th align="left">允许串联用分号分隔的其他命令</th>
<th align="left">会将到单个命令块</th>
<th align="left">允许脚本参数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>$&lt;</strong></p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$&gt;&lt;</strong></p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$$&lt;</strong></p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$$&gt;&lt;</strong></p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$$&gt;的&lt;</strong></p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

**$&lt;**、、 **$&gt;&lt;** **$$&lt;** 和 **$$&gt;&lt;** 命令回显脚本文件中包含的命令并显示这些命令的输出。 **$$ &gt; A &lt;** 命令不会回显在脚本文件中找到的命令，而只显示其输出。

脚本文件可以嵌套。 如果调试器在脚本文件中遇到其中一个标记，执行操作会移动到新的脚本文件，并在新的脚本文件完成后返回到以前的位置。 还可以以递归方式调用脚本。

在 WinDbg 中，你可以将其他命令文本粘贴命令窗口中。

<a name="examples"></a>示例
--------

下面的示例演示如何 Myfile.txt 传递参数到脚本文件。 假定该文件包含以下文本：

```console
.echo The first argument is ${$arg1}.
.echo The second argument is ${$arg2}.
```

然后，可以使用如下所示的命令将参数传递给此文件：

```console
0:000> $$>a<myfile.txt myFirstArg mySecondArg 
```

此命令的结果将为：

```console
The first argument is myFirstArg.
The second argument is mySecondArg.
```

下面是在提供错误数目的参数时所发生情况的示例。 假设文件 "我的 Script.txt 包含以下文本：

```console
.echo The first argument is ${$arg1}.
.echo The fifth argument is ${$arg5}.
.echo The fourth argument is ${$arg4}.
```

接下来以分号分隔的命令行生成输出，因此：

```console
0:000> $$>a< "c:\binl\my script.txt" "First one" Two "Three More" Four; recx 
The first argument is First one.
The fifth argument is ${$arg5}.
The fourth argument is Four.
ecx=0021f4ac
```

在前面的示例中，文件名括在引号中，因为它包含空格，而包含空格的参数也用引号引起来。 尽管脚本看起来是第五个参数，但在第四个参数后，分号将终止 **$$ &gt; a &lt;** 命令。

 


