---
title: 伪寄存器语法
description: 伪寄存器语法
keywords:
- 伪寄存器
- 伪注册，自动
- 伪寄存器，用户定义
- 注册，伪寄存器
- 循环变量
- 寄信人地址
- $to 到 $t 19 个伪寄存器
- $bp ID 伪注册
- $ea
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6eccc33d9bf19b0cd9e964c83967f2f1af0bf082
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811209"
---
# <a name="pseudo-register-syntax"></a>伪寄存器语法


## <span id="ddk_pseudo_register_syntax_dbg"></span><span id="DDK_PSEUDO_REGISTER_SYNTAX_DBG"></span>


调试器支持多个用于保存某些值的伪寄存器。

调试器将 *自动伪寄存器* 设置为某些有用的值。 *用户定义的伪寄存器* 是可以写入或读取的整数变量。

所有伪寄存器均以美元符号 () 开头 **$** 。 如果使用的是 MASM 语法，则可以在美元符号前面添加 at 符号 ( **@** ) 。 此 at 符号通知调试器以下标记是寄存器或伪寄存器，而不是符号。 如果省略 at 符号，则调试器的响应速度会变慢，因为它必须搜索整个符号表。

例如，下面的两个命令生成相同的输出，但第二个命令的速度更快。

```dbgcmd
0:000> ? $exp
Evaluate expression: 143 = 0000008f
0:000> ? @$exp
Evaluate expression: 143 = 0000008f
```

如果存在与伪寄存器名称相同的符号，则必须添加 at 符号。

如果使用 c + + 表达式语法，则始终需要 at 符号 ( **@** ) 。

[**R (寄存器)**](r--registers-.md)命令是此规则的例外情况。 调试器始终将其第一个参数解释为寄存器或伪寄存器。  (at 符号不是必需的或不允许的。 ) 如果 **r** 命令有另一个参数，则将根据默认表达式语法对其进行解释。 如果默认表达式语法是 c + +，则必须使用以下命令将 **$t 2** 伪寄存器复制到 **$t 1** 伪寄存器。

```dbgcmd
0:000> r $t1 = @$t2
```

### <a name="span-idautomatic_pseudo_registersspanspan-idautomatic_pseudo_registersspanautomatic-pseudo-registers"></a><span id="automatic_pseudo_registers"></span><span id="AUTOMATIC_PSEUDO_REGISTERS"></span>自动 Pseudo-Registers

调试器会自动设置以下伪寄存器。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">伪注册</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>$ea</strong></p></td>
<td align="left"><p>最后执行的指令的有效地址。 如果此指令没有有效地址，调试器将显示 "错误寄存器错误"。 如果此指令具有两个有效地址，则调试器将显示第一个地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$ea 2</strong></p></td>
<td align="left"><p>执行的最后一条指令的第二个有效地址。 如果此指令没有两个有效地址，调试器将显示 "错误寄存器错误"。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exp</strong></p></td>
<td align="left"><p>计算的最后一个表达式。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$ra</strong></p></td>
<td align="left"><p>当前位于堆栈上的返回地址。</p>
<p>此地址在执行命令中特别有用。 例如， <strong>g @ $ra</strong> 将继续，直到找到返回地址 (不过，如果 <strong><a href="gu--go-up-.md" data-raw-source="[gu (Go Up)](gu--go-up-.md)">gu (，) </a></strong> 是当前函数) 的 "跳出" 的更精确的方式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$ip</strong></p></td>
<td align="left"><p>指令指针寄存器。</p>
<p></p>
<strong>基于 x86 的处理器：</strong> 与 <strong>eip</strong>相同。
<strong>基于 Itanium 的处理器：</strong> 与 <strong>iip</strong>相关。  (有关详细信息，请参阅此表后面的说明。 <strong>基于 x64 的处理器 ) ：</strong> 与 <strong>rip</strong>相同。</td>
</tr>
<tr class="even">
<td align="left"><p><strong>$eventip</strong></p></td>
<td align="left"><p>当前事件时的指令指针。 此指针通常与 <strong>$ip</strong>匹配，除非你切换了线程或手动更改了指令指针的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$previp</strong></p></td>
<td align="left"><p>上一事件发生时的指令指针。  (中断到调试器将计为一个事件。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$relip</strong></p></td>
<td align="left"><p>与当前事件相关的指令指针。 当你作为分支跟踪时，此指针是指向分支源的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$scopeip</strong></p></td>
<td align="left"><p>当前 <a href="changing-contexts.md#local-context" data-raw-source="[local context](changing-contexts.md#local-context)">本地上下文</a> 的指令指针 (也称为 <em>范围</em>) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exentry</strong></p></td>
<td align="left"><p>当前进程的第一个可执行文件的入口点地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$retreg</strong></p></td>
<td align="left"><p>主返回值 register。</p>
<p></p>
<strong>基于 x86 的处理器：</strong> 与 <strong>eax</strong>相同。
<strong>基于 Itanium 的处理器：</strong> 与 <strong>ret0</strong>相同。
<strong>基于 x64 的处理器：</strong> 与 <strong>rax</strong>相同。</td>
</tr>
<tr class="even">
<td align="left"><p><strong>$retreg 64</strong></p></td>
<td align="left"><p>以64位格式注册的主返回值。</p>
<p><strong>x86 处理器：</strong> 与 <strong>edx： eax</strong> 对相同。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$csp</strong></p></td>
<td align="left"><p>当前调用堆栈指针。 此指针是最代表调用堆栈深度的寄存器。</p>
<p></p>
<strong>基于 x86 的处理器：</strong> 与 <strong>esp</strong>相同的。 <strong>基于 Itanium 的处理器：</strong> 与 <strong>bsp</strong>相同。
<strong>基于 x64 的处理器：</strong> 与 <strong>rsp</strong>相同的。</td>
</tr>
<tr class="even">
<td align="left"><p><strong>$p</strong></p></td>
<td align="left"><p>最后一个 <strong><a href="d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md" data-raw-source="[d* (Display Memory)](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)">d * (显示内存) </a></strong> 命令的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$proc</strong></p></td>
<td align="left"><p>当前进程的地址 (即，EPROCESS 块的地址) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$thread</strong></p></td>
<td align="left"><p>当前线程的地址。 在内核模式调试中，此地址是 ETHREAD 块的地址。 在用户模式调试中，此地址是线程环境块 (TEB) 的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$peb</strong></p></td>
<td align="left"><p>进程环境块的地址 (当前进程的 PEB) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$teb</strong></p></td>
<td align="left"><p>线程环境的地址块 (当前线程的 TEB) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$tpid</strong></p></td>
<td align="left"><p>拥有当前线程的进程的进程 ID (PID) 。</p></td>
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
<td align="left"><p><strong>$bp</strong><em>号</em></p></td>
<td align="left"><p>对应断点的地址。 例如， <strong>$bp 3</strong> (或 <strong>$Bp 03</strong>) 引用断点 ID 为3的断点。 <em>Number</em> 始终是一个十进制数。 如果没有断点的 ID 为 <em>number</em>，则 <strong>$bp</strong><em>数字</em> 的计算结果为零。 有关断点的详细信息，请参阅 <a href="using-breakpoints.md" data-raw-source="[Using Breakpoints](using-breakpoints.md)">使用断点</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$frame</strong></p></td>
<td align="left"><p>当前帧索引。 此索引与 <strong><a href="-frame--set-local-context-.md" data-raw-source="[.frame (Set Local Context)](-frame--set-local-context-.md)"> (设置本地上下文) </a></strong> 命令使用的帧号相同。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$dbgtime</strong></p></td>
<td align="left"><p>当前时间，根据调试器正在其上运行的计算机。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$callret</strong></p></td>
<td align="left"><p><strong><a href="-call--call-function-.md" data-raw-source="[.call (Call Function)](-call--call-function-.md)">) 调用 (调用函数</a></strong>的最后一个函数的返回值，或在<strong><a href="-fnret--display-function-return-value-.md" data-raw-source="[.fnret /s](-fnret--display-function-return-value-.md)">fnret/s</a></strong>命令中使用的。 <strong>$Callret</strong>的数据类型是此返回值的数据类型。</p></td>
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
<td align="left"><p><strong>仅限托管调试：</strong> 上次遇到的公共语言运行时的地址 (CLR) exception 对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$ptrsize</strong></p></td>
<td align="left"><p>指针的大小。 在内核模式下，此大小是目标计算机上的指针大小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pagesize</strong></p></td>
<td align="left"><p>一页内存中的字节数。 在内核模式下，此大小是目标计算机上的页面大小。</p></td>
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
<td align="left"><p><strong>$exr _chance</strong></p></td>
<td align="left"><p>当前异常记录的可能性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exr _code</strong></p></td>
<td align="left"><p>当前异常记录的异常代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr _numparams</strong></p></td>
<td align="left"><p>当前异常记录中参数的数目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exr _param0</strong></p></td>
<td align="left"><p>当前异常记录中参数0的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr _param1</strong></p></td>
<td align="left"><p>当前异常记录中参数1的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exr _param2</strong></p></td>
<td align="left"><p>当前异常记录中参数2的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr _param3</strong></p></td>
<td align="left"><p>当前异常记录中参数3的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exr _param4</strong></p></td>
<td align="left"><p>当前异常记录中参数4的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr _param5</strong></p></td>
<td align="left"><p>当前异常记录中参数5的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exr _param6</strong></p></td>
<td align="left"><p>当前异常记录中的参数6的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr _param7</strong></p></td>
<td align="left"><p>当前异常记录中参数7的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exr _param8</strong></p></td>
<td align="left"><p>当前异常记录中参数8的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr _param9</strong></p></td>
<td align="left"><p>当前异常记录中参数9的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exr _param10</strong></p></td>
<td align="left"><p>当前异常记录中参数10的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr _param11</strong></p></td>
<td align="left"><p>当前异常记录中的参数11的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exr _param12</strong></p></td>
<td align="left"><p>当前异常记录中参数12的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr _param13</strong></p></td>
<td align="left"><p>当前异常记录中参数13的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exr _param14</strong></p></td>
<td align="left"><p>当前异常记录中参数14的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$bug _code</strong></p></td>
<td align="left"><p>如果发生 bug 检查，则这是错误代码。 适用于实时内核模式调试和内核故障转储。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$bug _param1</strong></p></td>
<td align="left"><p>如果发生 bug 检查，则这是参数1的值。 适用于实时内核模式调试和内核故障转储。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$bug _param2</strong></p></td>
<td align="left"><p>如果发生 bug 检查，则这是参数2的值。 适用于实时内核模式调试和内核故障转储。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$bug _param3</strong></p></td>
<td align="left"><p>如果发生 bug 检查，则这是参数3的值。 适用于实时内核模式调试和内核故障转储。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$bug _param4</strong></p></td>
<td align="left"><p>如果发生 bug 检查，则这是参数4的值。 适用于实时内核模式调试和内核故障转储。</p></td>
</tr>
</tbody>
</table>

 

其中一些伪寄存器在某些调试方案中可能不可用。 例如，在调试用户模式的小型转储或某些内核模式转储文件时，不能使用 **$peb**、 **$tid** 和 **$tpid** 。 在某些情况下，你可以从 [**~ (线程状态**](---thread-status-.md) 了解线程信息) 但不能从 **$tid** 中学习。 在第一个调试器事件上不能使用 **$previp** 伪寄存器。 除非你是分支跟踪，否则不能使用 **$relip** 伪寄存器。 如果使用不可用的伪寄存器，则会出现语法错误。

保存结构（例如 **$thread**、 **$proc**、 **$teb**、 **$peb** 和 **$Lastclrex** ）地址的伪寄存器将根据 c + + 表达式计算器中的正确数据类型进行计算，但不会根据 MASM 表达式计算器中的数据类型进行计算。 例如，命令 **？ $teb** 显示 teb 的地址，而命令 **？ @ $TEB** 显示整个 teb 结构。 有关详细信息，请参阅 [计算表达式](evaluating-expressions.md)。

在基于 Itanium 的处理器上， **iip** 寄存器是 *捆绑* 在一起的，这意味着它指向包含当前指令的捆绑中的插槽0，即使正在执行其他槽也是如此。 因此 **iip** 不是完整的指令指针。 **$Ip** 伪寄存器是实际的指令指针，包括捆绑包和槽。 保存地址指针的其他伪寄存器 (**$ra**、 **$retreg**、 **$eventip**、 **$previp**、 **$relip** 和 **$exentry**) 与所有处理器上的 **$ip** 具有相同的结构。

可以使用 **r** 命令更改 **$ip** 的值。 此更改还会自动更改相应的寄存器。 执行恢复后，它将在新的指令指针地址处恢复。 此注册是唯一可手动更改的自动伪寄存器。

**注意**   在 MASM 语法中，可以用句点 ( 指示 **$ip** 伪寄存器 **。** ). 在此时间段之前，不会将 @ sign ( @ ) 添加到，也不要使用句点作为 **r** 命令的第一个参数。 C + + 表达式中不允许使用此语法。

 

自动伪寄存器类似于 [自动别名](using-aliases.md)。 但是，可以将自动别名与别名相关标记一起使用 (如 **$ {}**) ，而不能将伪寄存器与此类标记一起使用。

### <a name="span-iduser_defined_pseudo_registersspanspan-iduser_defined_pseudo_registersspanuser-defined-pseudo-registers"></a><span id="user_defined_pseudo_registers"></span><span id="USER_DEFINED_PSEUDO_REGISTERS"></span>用户定义的 Pseudo-Registers

有20个用户定义的伪寄存器 (**$t 0**， **$t 1**，...， **$t 19**) 。 这些伪寄存器是可通过调试器进行读取和写入的变量。 可以在这些伪寄存器中存储任何整数值。 它们对于循环变量特别有用。

若要写入这些伪寄存器中的一个，请使用 [**r (寄存器)**](r--registers-.md) 命令，如以下示例所示。

```dbgcmd
0:000> r $t0 = 7
0:000> r $t1 = 128*poi(MyVar)
```

与所有伪寄存器一样，你可以在任何表达式中使用用户定义的伪寄存器，如下面的示例所示。

```dbgcmd
0:000> bp $t3 
0:000> bp @$t4 
0:000> ?? @$t1 + 4*@$t2 
```

伪寄存器始终类型化为整数，除非使用 **？** 与 **r** 命令一起切换。 如果使用此开关，伪寄存器将获取分配给它的任何类型。 例如，以下命令将 UNICODE \_ 字符串 \* \* 类型和0x0012FFBC 值分配到 **$t 15**。

```dbgcmd
0:000> r? $t15 = * (UNICODE_STRING*) 0x12ffbc
```

在启动调试器时，用户定义的伪寄存器使用零作为默认值。

**注意**  尽管别名 **$u 0**， **$u 1**，...， **$u 9** 不是伪寄存器，尽管它们的外观类似。 有关这些别名的详细信息，请参阅 [使用别名](using-aliases.md)。

 

### <a name="span-idexample1spanspan-idexample1spanexample"></a><span id="example1"></span><span id="EXAMPLE1"></span>示例

下面的示例设置一个断点，该断点将在每次当前线程调用 **NtOpenFile** 时命中。 但当其他线程调用 **NtOpenFile** 时，不会命中此断点。

```dbgcmd
kd> bp /t @$thread nt!ntopenfile
```

### <a name="span-idexample2spanspan-idexample2spanexample"></a><span id="example2"></span><span id="EXAMPLE2"></span>示例

下面的示例执行一个命令，直到寄存器持有指定的值。 首先，将以下代码添加到名为 "eaxstep" 的脚本文件中的条件单。

```dbgcmd
.if (@eax == 1234) { .echo 1234 } .else { t "$<eaxstep" }
```

接下来，发出以下命令。

```dbgcmd
t "$<eaxstep"
```

调试器执行步骤，然后运行命令。 在这种情况下，调试器将运行脚本，该脚本显示 **1234** 或重复该过程。

 

 





