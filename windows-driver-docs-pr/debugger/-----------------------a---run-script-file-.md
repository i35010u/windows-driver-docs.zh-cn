---
title: $，$，$$ $$ $$ （运行的脚本文件）
description: $、 $、 $$、 $$ 和 $$ 命令读取指定的脚本文件的内容，并使用其内容作为输入的调试器命令。
ms.assetid: b3584680-765d-4aaf-ad43-c7d73552e5fb
keywords:
- （运行脚本文件） 的 $ 命令
- $$ （运行脚本文件） 命令
- $$ （运行脚本文件） 命令
- 运行脚本文件 （$） 命令
- 运行脚本文件 （$） 命令
- 运行脚本文件 （$$） 命令
- 运行脚本文件 （$$） 通信
- $，$，$$ $$ $$ （运行的脚本文件） Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- $ , $ , $$ , $$ , $$ a (Run Script File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6b6d169b34905526d7358f1dbe4c93883935a991
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334869"
---
# <a name="-----a-run-script-file"></a>$<、$><、$$<、$$><、$$ >a<（运行脚本文件）


**$ &lt;**， **$ &gt; &lt;**， **$$ &lt;**， **$$ &gt; &lt;** ，并**$$ &gt;&lt;** 命令读取指定的脚本的内容文件中并使用作为其内容调试器命令输入。

```dbgcmd
    $<Filename 
    $><Filename 
    $$<Filename 
    $$><Filename 
    $$>a<Filename [arg1 arg2 arg3 ...] 
```

## <a name="span-idddkcmdrunscriptfiledbgspanspan-idddkcmdrunscriptfiledbgspanparameters"></a><span id="ddk_cmd_run_script_file_dbg"></span><span id="DDK_CMD_RUN_SCRIPT_FILE_DBG"></span>参数


<span id="_______Filename______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *文件名*   
指定包含有效的调试器命令文本的文件。 文件名称必须遵守 Microsoft Windows 文件命名约定。 文件名称可能包含空格。

<span id="_______argn______"></span><span id="_______ARGN______"></span> *argn*   
指定任意数量的调试程序要传递给脚本的字符串参数。 调试器会将窗体 $ 任何字符串替换 {$arg*n*} 中具有相应的脚本文件*argn*之前执行脚本。 参数不得包含引号或分号。 多个自变量必须以空格分隔;如果参数包含的空格，则必须用引号引起来。 所有自变量是可选的。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>模式</p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p>目标</p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p>平台</p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**$$ &lt;** 并**$ &lt;** 令牌执行按原义找到脚本文件中的命令。 但是，对于**$ &lt;** 可以指定任何文件名，其中包括一个包含分号。 因为**$ &lt;** 允许以文件的文件名中使用分号作为不能连接**$ &lt;** 与其他调试程序命令，因为为命令分隔符和文件名称的一部分，不能使用分号。

**$$ &gt; &lt;** 并**$ &gt; &lt;** 令牌执行按字面意思找到脚本文件中的命令这意味着它们打开脚本文件，用分号，替换所有回车符和执行单个命令块为生成的文本。 如同**$ &lt;** 已经讨论过， **$ &gt; &lt;** 变体允许文件的名称包含分号，这意味着不能串联**$ &gt; &lt;** 与其他调试程序命令。

**$$ &gt; &lt;** 并**$ &gt; &lt;** 令牌是很有用，如果运行的脚本中包含调试器命令程序。 有关这些程序的详细信息，请参阅[使用调试器命令程序](using-debugger-command-programs.md)。

除非您有包含分号的文件名，不需要使用两种**$ &lt;** 或**$ &gt; &lt;**。

**$$ &gt;&lt;** 令牌使调试器能够在将参数传递给脚本。 如果*文件名*包含空格，则必须用引号引起来。 如果提供的参数太多了，将忽略多余的参数。 如果未提供的参数太少，任何令牌的窗体 $ 源文件中 {$arg*n*} 位置*n*大于提供的参数数量将保留在其文本的形式，并且将不替换为任何内容。 可以按照此命令使用分号和其他命令;存在分号终止参数列表。

当调试器执行的脚本文件时中, 显示的命令和相应的输出[调试器命令窗口](debugger-command-window.md)。 当达到脚本文件的末尾时，控制权返回给调试器。

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
<th align="left">令牌</th>
<th align="left">允许包含分号的文件名</th>
<th align="left">允许其他命令之间用分号分隔的串联</th>
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
<td align="left"><p><strong>$$&gt;a&lt;</strong></p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

**$ &lt;**， **$ &gt; &lt;**， **$$ &lt;**，和**$$ &gt; &lt;** 命令回显的脚本中包含的命令文件，并显示这些命令的输出。 **$$ &gt;&lt;** 命令不会将回显在脚本文件中，找到的命令，但只显示其输出。

可以嵌套的脚本文件。 如果调试器遇到其中一个令牌中的脚本文件，执行将移至新的脚本文件，并完成新的脚本文件时，返回到前一个位置。 也可以调用脚本以递归方式。

在 WinDbg 中，你可以粘贴调试器命令窗口中的其他命令文本。

<a name="examples"></a>示例
--------

下面的示例演示如何将参数传递到脚本文件，Myfile.txt。 假定该文件包含以下文本：

```console
.echo The first argument is ${$arg1}.
.echo The second argument is ${$arg2}.
```

然后可以通过使用如下命令对此文件传递参数：

```console
0:000> $$>a<myfile.txt myFirstArg mySecondArg 
```

此命令的结果将是：

```console
The first argument is myFirstArg.
The second argument is mySecondArg.
```

下面是参数的提供数目不正确时，会发生什么情况的示例。 假设我 Script.txt 该文件包含以下文本：

```console
.echo The first argument is ${$arg1}.
.echo The fifth argument is ${$arg5}.
.echo The fourth argument is ${$arg4}.
```

然后以分号分隔的以下命令行会将因此生成输出：

```console
0:000> $$>a< "c:\binl\my script.txt" "First one" Two "Three More" Four; recx 
The first argument is First one.
The fifth argument is ${$arg5}.
The fourth argument is Four.
ecx=0021f4ac
```

在前面的示例中，文件名称被用引号将因为它包含一个空格，并且包含空格的参数括在引号引起来也。 尽管第五个参数看起来所需的脚本，以分号终止**$$ &gt;&lt;** 命令后的第四个参数。

 


