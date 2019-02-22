---
title: 伪寄存器语法
description: 伪寄存器语法
ms.assetid: f7dc52ea-e97e-4251-a517-c115cbc7d056
keywords:
- pseudo-registers
- 伪寄存器自动
- 伪寄存器中，用户定义
- 寄存器，伪寄存器
- 循环变量
- 寄信人地址
- $ 到 $t19 伪寄存器
- $bp ID pseudo-register
- $ea
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d459b99d76a14123a6a407d69a271822451f52b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520584"
---
# <a name="pseudo-register-syntax"></a>伪寄存器语法


## <span id="ddk_pseudo_register_syntax_dbg"></span><span id="DDK_PSEUDO_REGISTER_SYNTAX_DBG"></span>


调试器支持保存某些值的多个伪寄存器。

调试程序集*自动伪寄存器*到某些有用的值。 *用户定义的伪寄存器*是整数变量，您可以读取或写入。

所有伪寄存器开头美元符号 (**$**)。 如果您使用 MASM 语法，您可以添加 at 符号 ( **@** ) 之前美元符号。 在登录这将告知调试器下一个标记是寄存器或伪寄存器，不是符号。 如果省略 at 符号，调试程序的响应速度更慢，因为它具有整个符号表中搜索。

例如，以下两个命令生成相同的输出，但第二个命令的速度更快。

```dbgcmd
0:000> ? $exp
Evaluate expression: 143 = 0000008f
0:000> ? @$exp
Evaluate expression: 143 = 0000008f
```

如果存在具有相同名称作为伪寄存器的符号，则必须添加 at 符号。

如果您使用的 c + + 表达式语法，at 符号 ( **@** ) 始终是必需的。

[ **R （寄存器）** ](r--registers-.md)命令是此规则的例外。 调试器始终解释为寄存器或伪寄存器，其第一个参数。 (在登录不要求或不允许。)如果没有为第二个参数**r**命令时，它根据默认表达式语法进行解释。 如果默认表达式语法是 c + +，您必须使用以下命令复制 **$t2**到伪寄存器 **$t1**伪寄存器。

```dbgcmd
0:000> r $t1 = @$t2
```

### <a name="span-idautomaticpseudoregistersspanspan-idautomaticpseudoregistersspanautomatic-pseudo-registers"></a><span id="automatic_pseudo_registers"></span><span id="AUTOMATIC_PSEUDO_REGISTERS"></span>自动伪寄存器

调试器将自动设置以下伪寄存器。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">伪寄存器</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>$ea</strong></p></td>
<td align="left"><p>已执行的最后一个指令的有效地址。 如果此指令没有有效的地址，则调试器会显示&quot;寄存器错误&quot;。 如果此指令有两个有效的地址，调试器会显示第一个地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$ea2</strong></p></td>
<td align="left"><p>已执行的最后一个指令的第二个的有效地址。 如果此指令不具有两个有效的地址，则调试器会显示&quot;寄存器错误&quot;。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exp</strong></p></td>
<td align="left"><p>最后一个表达式的计算。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$ra</strong></p></td>
<td align="left"><p>寄信人地址为当前位于堆栈上。</p>
<p>此地址是在执行命令中尤其有用。 例如， <strong>g @$ ra</strong>继续，直到找到返回地址 (尽管<strong><a href="gu--go-up-.md" data-raw-source="[gu (Go Up)](gu--go-up-.md)">(Go Up) gu</a></strong>是更精确的有效方式&quot;出单步执行&quot;的当前函数)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$ip</strong></p></td>
<td align="left"><p>指令指针寄存器。</p>
<p></p>
<strong>基于 x86 的处理器：</strong>与相同<strong>eip</strong>。
<strong>基于 Itanium 处理器：</strong>与相关<strong>iip</strong>。 （有关详细信息，请参阅此表后面的说明）。<strong>基于 x64 的处理器：</strong>与相同<strong>rip</strong>。</td>
</tr>
<tr class="even">
<td align="left"><p><strong>$eventip</strong></p></td>
<td align="left"><p>当前事件的时间处的指令指针。 此指针通常与匹配<strong>$ip</strong>，除非你切换线程或手动更改指令指针的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$previp</strong></p></td>
<td align="left"><p>上一事件的时间处的指令指针。 （中断到调试器计为一个事件。）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$relip</strong></p></td>
<td align="left"><p>指令指针与当前事件相关的。 分支跟踪时，此指针是指向分支源的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$scopeip</strong></p></td>
<td align="left"><p>当前指令指针<a href="changing-contexts.md#local-context" data-raw-source="[local context](changing-contexts.md#local-context)">本地上下文</a>(也称为<em>作用域</em>)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exentry</strong></p></td>
<td align="left"><p>当前进程的第一个可执行文件的入口点的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$retreg</strong></p></td>
<td align="left"><p>主要的返回值寄存器中。</p>
<p></p>
<strong>基于 x86 的处理器：</strong>与相同<strong>eax</strong>。
<strong>基于 Itanium 处理器：</strong>与相同<strong>ret0</strong>。
<strong>基于 x64 的处理器：</strong>与相同<strong>rax</strong>。</td>
</tr>
<tr class="even">
<td align="left"><p><strong>$retreg64</strong></p></td>
<td align="left"><p>在 64 位格式中注册主要的返回值。</p>
<p><strong>x86 处理器：</strong>与相同<strong>edx: eax</strong>对。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$csp</strong></p></td>
<td align="left"><p>当前调用堆栈指针。 此指针是最具代表性的调用堆栈深度的寄存器。</p>
<p></p>
<strong>基于 x86 的处理器：</strong>与相同<strong>esp</strong>。<strong>基于 Itanium 处理器：</strong>与相同<strong>bsp</strong>。
<strong>基于 x64 的处理器：</strong>与相同<strong>rsp</strong>。</td>
</tr>
<tr class="even">
<td align="left"><p><strong>$p</strong></p></td>
<td align="left"><p>值的最后一个<strong><a href="d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md" data-raw-source="[d* (Display Memory)](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)">d * （显示内存）</a></strong>打印命令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$proc</strong></p></td>
<td align="left"><p>当前进程 （即，地址 EPROCESS 块） 的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$thread</strong></p></td>
<td align="left"><p>当前线程的地址。 在内核模式调试，此地址是 ETHREAD 块的地址。 在用户模式调试，此地址为线程环境块 (TEB) 的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$peb</strong></p></td>
<td align="left"><p>当前进程的进程环境块 (PEB) 的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$teb</strong></p></td>
<td align="left"><p>当前线程的线程环境块 (TEB) 的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$tpid</strong></p></td>
<td align="left"><p>拥有当前线程的进程的进程 ID (PID)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$tid</strong></p></td>
<td align="left"><p>当前线程的线程 ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$dtid</strong></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$dpid</strong></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$dsid</strong></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$bp</strong><em>Number</em></p></td>
<td align="left"><p>相应的断点的地址。 例如，<strong>美元 bp3</strong> (或<strong>美元 bp03</strong>) 指的是断点的断点 ID 为 3。 <em>数字</em>始终是一个十进制数。 如果任何断点不的 ID 为<em>数量</em>， <strong>$bp</strong><em>数</em>计算结果为零。 有关断点的详细信息，请参阅<a href="using-breakpoints.md" data-raw-source="[Using Breakpoints](using-breakpoints.md)">使用断点</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$frame</strong></p></td>
<td align="left"><p>当前的帧索引。 此索引是相同的帧号<strong><a href="-frame--set-local-context-.md" data-raw-source="[.frame (Set Local Context)](-frame--set-local-context-.md)">.frame （设置本地上下文）</a></strong>命令使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$dbgtime</strong></p></td>
<td align="left"><p>根据计算机上运行调试器的当前时间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$callret</strong></p></td>
<td align="left"><p>返回值的最后一个函数<strong><a href="-call--call-function-.md" data-raw-source="[.call (Call Function)](-call--call-function-.md)">.call （调用函数）</a></strong>中使用或调用<strong><a href="-fnret--display-function-return-value-.md" data-raw-source="[.fnret /s](-fnret--display-function-return-value-.md)">.fnret /s</a></strong>命令。 数据类型<strong>$callret</strong>是此返回值的数据类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$extret</strong></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$extin</strong></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$clrex</strong></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$lastclrex</strong></p></td>
<td align="left"><p><strong>托管仅调试：</strong>上一次遇到公共语言运行时 (CLR) 异常对象的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$ptrsize</strong></p></td>
<td align="left"><p>指针的大小。 在内核模式下，此大小是目标计算机上的指针大小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pagesize</strong></p></td>
<td align="left"><p>在一页上的内存字节数。 在内核模式下，此大小为目标计算机上的页面大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$pcr</strong></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pcrb</strong></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$argreg</strong></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr_chance</strong></p></td>
<td align="left"><p>当前的异常记录的可能性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exr_code</strong></p></td>
<td align="left"><p>当前的异常记录异常代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr_numparams</strong></p></td>
<td align="left"><p>当前的异常记录中的参数数量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exr_param0</strong></p></td>
<td align="left"><p>当前的异常记录中的参数 0 的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr_param1</strong></p></td>
<td align="left"><p>当前的异常记录中的值的参数 1。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exr_param2</strong></p></td>
<td align="left"><p>当前的异常记录中的参数 2 的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr_param3</strong></p></td>
<td align="left"><p>当前的异常记录中的参数 3 的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exr_param4</strong></p></td>
<td align="left"><p>当前的异常记录中的参数 4 的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr_param5</strong></p></td>
<td align="left"><p>当前的异常记录中的参数 5 的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exr_param6</strong></p></td>
<td align="left"><p>当前的异常记录中的参数 6 的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr_param7</strong></p></td>
<td align="left"><p>当前的异常记录中的值的参数 7。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exr_param8</strong></p></td>
<td align="left"><p>当前的异常记录中的参数 8 的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr_param9</strong></p></td>
<td align="left"><p>当前的异常记录中的值的参数 9。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exr_param10</strong></p></td>
<td align="left"><p>当前的异常记录中的参数 10 的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr_param11</strong></p></td>
<td align="left"><p>当前的异常记录中的参数 11 的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exr_param12</strong></p></td>
<td align="left"><p>当前的异常记录中的值的参数 12。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr_param13</strong></p></td>
<td align="left"><p>当前的异常记录中的值的参数 13。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exr_param14</strong></p></td>
<td align="left"><p>当前的异常记录中的值为 14 个参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$bug_code</strong></p></td>
<td align="left"><p>如果发生了错误检查，这是错误代码。 适用于实时内核模式调试和内核故障转储。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$bug_param1</strong></p></td>
<td align="left"><p>如果发生了错误检查，这是参数 1 的值。 适用于实时内核模式调试和内核故障转储。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$bug_param2</strong></p></td>
<td align="left"><p>如果发生了错误检查，这是参数 2 的值。 适用于实时内核模式调试和内核故障转储。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$bug_param3</strong></p></td>
<td align="left"><p>如果发生了错误检查，这是参数 3 的值。 适用于实时内核模式调试和内核故障转储。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$bug_param4</strong></p></td>
<td align="left"><p>如果发生了错误检查，这是参数 4 的值。 适用于实时内核模式调试和内核故障转储。</p></td>
</tr>
</tbody>
</table>

 

这些伪寄存器的一些可能无法在某些调试方案中。 例如，不能使用 **$peb**， **$tid**，并 **$tpid**在调试小型转储用户模式下或某些内核模式转储文件。 可以从何处了解从线程信息的情况将会[ **~ （线程状态）** ](---thread-status-.md)但不能从 **$tid**。 不能使用 **$previp**伪寄存器上的第一个调试器事件。 不能使用 **$relip**伪寄存器，除非您是分支跟踪。 如果使用伪寄存器不可用，将发生语法错误。

如保留的地址结构-伪寄存器 **$thread**， **$proc**， **$teb**， **$peb**，和 **$lastclrex** -将根据适当的数据类型在 c + + 表达式计算器，但不是在 MASM 表达式计算器计算。 例如，命令 **？ $teb** TEB，该命令时的地址将显示 **?? @$ teb**显示整个 TEB 结构。 有关详细信息，请参阅[评估表达式](evaluating-expressions.md)。

在基于 Itanium 处理器上， **iip**中注册被*捆绑对齐*，这意味着，它指向包含当前指令，捆绑中槽 0，即使正在执行另一个槽。 因此**iip**不是完整的指令指针。 **$Ip**伪寄存器是实际的指令指针，其中包括此捆绑包和槽。 保存地址指针的其他伪寄存器 (**$ra**， **$retreg**， **$eventip**， **$previp**， **$relip**，并 **$exentry**) 具有相同的结构 **$ip**所有处理器上。

可以使用**r**命令以更改的值 **$ip**。 此更改还会自动更改相应的注册。 当继续执行时，继续在新的指令指针地址。 此寄存器是仅自动伪寄存器，您可以手动更改。

**请注意**  在 MASM 语法中，您可以指示 **$ip**有时间段的伪寄存器 ( **。** )。 不添加 at 符号 (@) 之前此时间段，并不使用句点作为第一个参数**r**命令。 C + + 表达式中不允许使用此语法。

 

自动伪寄存器是类似于[自动别名](using-aliases.md)。 但您可以使用与别名相关令牌一起自动别名 (如 **$ {}**)，也不能使用此类令牌使用伪寄存器。

### <a name="span-iduserdefinedpseudoregistersspanspan-iduserdefinedpseudoregistersspanuser-defined-pseudo-registers"></a><span id="user_defined_pseudo_registers"></span><span id="USER_DEFINED_PSEUDO_REGISTERS"></span>用户定义的伪寄存器

20 用户定义的伪寄存器 (**美元 t0**， **$t1**，...，**美元 t19**)。 这些伪寄存器是变量，您可以读取和写入通过调试程序。 您可以在这些伪寄存器中存储的任何整数值。 它们可以是循环变量这很有用。

若要写入到一个这些伪寄存器，使用[ **r （寄存器）** ](r--registers-.md)命令，如以下示例所示。

```dbgcmd
0:000> r $t0 = 7
0:000> r $t1 = 128*poi(MyVar)
```

与所有伪寄存器中，您可以在任何表达式中，如以下示例所示使用用户定义的伪寄存器。

```dbgcmd
0:000> bp $t3 
0:000> bp @$t4 
0:000> ?? @$t1 + 4*@$t2 
```

伪寄存器始终类型化为一个整数，除非使用 **？** 切换连同**r**命令。 如果使用此开关，伪寄存器将获取的任何分配给它的类型。 例如，以下命令将 UNICODE\_字符串\*\*类型和 0x0012FFBC 值到**美元 t15**。

```dbgcmd
0:000> r? $t15 = * (UNICODE_STRING*) 0x12ffbc
```

启动调试器时，用户定义的伪寄存器使用零作为默认值。

**请注意**  别名**美元 u0**，**美元 u1**，...，**美元 u9**不是伪寄存器，尽管其外观类似。 有关这些别名的详细信息，请参阅[Using 别名](using-aliases.md)。

 

### <a name="span-idexample1spanspan-idexample1spanexample"></a><span id="example1"></span><span id="EXAMPLE1"></span>示例

下面的示例设置了当前线程调用每次命中的断点**NtOpenFile**。 但在其他线程调用时，则不会命中此断点**NtOpenFile**。

```dbgcmd
kd> bp /t @$thread nt!ntopenfile
```

### <a name="span-idexample2spanspan-idexample2spanexample"></a><span id="example2"></span><span id="EXAMPLE2"></span>示例

下面的示例执行一个命令，直到注册包含指定的值。 首先，将在名为"eaxstep"的脚本文件中的条件性单步执行下面的代码。

```dbgcmd
.if (@eax == 1234) { .echo 1234 } .else { t "$<eaxstep" }
```

接下来，发出以下命令。

```dbgcmd
t "$<eaxstep"
```

调试器执行一个步骤，并运行你的命令。 在这种情况下，调试器在运行脚本，其中任一显示**1234年**或重复此过程。

 

 





