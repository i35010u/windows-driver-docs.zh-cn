---
title: bp、bu、bm（设置断点）
description: Bp、bu 和 bm.exe 命令设置一个或多个软件断点。 可以组合位置、条件和选项来设置不同类型的软件断点。
ms.assetid: 77d095fe-06d1-4842-ad49-8420ab4d5d72
keywords:
- 最佳实践、bu、bm.exe (设置断点) Windows 调试
ms.date: 05/13/2020
topic_type:
- apiref
api_name:
- bp, bu, bm (Set Breakpoint)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 968c4b53dbc721bb48542481707f3c4326c2c030
ms.sourcegitcommit: bb3b62a57ba3aea4a0adeefd2d81993367b7b334
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88148504"
---
# <a name="bp-bu-bm-set-breakpoint"></a>bp、bu、bm（设置断点）


**Bp**、 **bu**和**bm.exe**命令设置一个或多个软件断点。 可以组合位置、条件和选项来设置不同类型的软件断点。

用户模式

```dbgcmd
[~Thread] bp[ID] [Options] [Address [Passes]] ["CommandString"] 
[~Thread] bu[ID] [Options] [Address [Passes]] ["CommandString"] 
[~Thread] bm [Options] SymbolPattern [Passes] ["CommandString"]
```

内核模式

```dbgcmd
bp[ID] [Options] [Address [Passes]] ["CommandString"] 
bu[ID] [Options] [Address [Passes]] ["CommandString"] 
bm [Options] SymbolPattern [Passes] ["CommandString"]
```

## <a name="span-idddk_cmd_set_breakpoint_dbgspanspan-idddk_cmd_set_breakpoint_dbgspanparameters"></a><span id="ddk_cmd_set_breakpoint_dbg"></span><span id="DDK_CMD_SET_BREAKPOINT_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
指定断点适用的线程。 有关语法的详细信息，请参阅 [线程语法](thread-syntax.md)。 只能在用户模式下指定线程。 如果未指定线程，则断点适用于所有线程。

<span id="_______ID______"></span><span id="_______id______"></span>*ID*   
指定标识断点的十进制数字。

调试器在创建断点时分配 *ID* ，但你可以使用 [**br (断点重新编号) **](br--breakpoint-renumber-.md) 命令来更改它。 可以使用 *ID* 在后面的调试器命令中引用断点。 若要显示断点的 *ID* ，请使用 [**Bl (断点列表) **](bl--breakpoint-list-.md) 命令。

在命令中使用 *ID* 时，请不要在命令 (**bp** 或 **bu**) 与 id 号之间键入空格。

*ID*参数始终是可选的。 如果未指定 *ID*，则调试器将使用第一个可用的断点号。 在内核模式下，只能设置32断点。 在用户模式下，可以设置任意数量的断点。 在任一情况下， *ID* 号的值都没有限制。 如果用方括号将 *id* 括起来 (**\[\]**) ， *ID* 可以包含任何表达式。 有关语法的详细信息，请参阅 [数值表达式语法](numerical-expression-syntax.md)。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
指定断点选项。 您可以指定下列任意数量的选项，除非指明：

<span id="_1"></span>**/1**  
创建 "一步" 断点。 触发此断点后，将从断点列表中删除它。

<span id="_p_EProcess"></span><span id="_p_eprocess"></span><span id="_P_EPROCESS"></span>**/P** *EProcess*  
仅 (内核模式) 指定与此断点关联的进程。 *EProcess* 应是 EProcess 结构的实际地址，而不是 PID。 仅当在此进程的上下文中遇到断点时才触发断点。

<span id="_t_EThread"></span><span id="_t_ethread"></span><span id="_T_ETHREAD"></span>**/T** *EThread*  
仅 (内核模式) 指定与此断点关联的线程。 *EThread* 应是 EThread 结构的实际地址，而不是线程 ID。 仅当在此线程的上下文中遇到断点时才触发断点。 如果使用 **/P** *EProcess* 和 **/t** *EThread*，则可以按任意顺序输入这些项。

<span id="_c_MaxCallStackDepth"></span><span id="_c_maxcallstackdepth"></span><span id="_C_MAXCALLSTACKDEPTH"></span>**/c** *MaxCallStackDepth*  
仅当调用堆栈深度小于 *MaxCallStackDepth*时才激活断点。 不能将此选项与 **/c**一起使用。

<span id="_C_MinCallStackDepth"></span><span id="_c_mincallstackdepth"></span><span id="_C_MINCALLSTACKDEPTH"></span>**/C** *MinCallStackDepth*  
仅当调用堆栈深度大于 *MinCallStackDepth*时才激活断点。 不能将此选项与 **/c**一起使用。

<span id="_a"></span><span id="_A"></span>**/a**  
 (For **bm.exe** 仅) 在所有指定位置上设置断点，无论它们是在数据空间中还是在代码空间中。 由于数据上的断点可能导致程序失败，因此只能在已知安全的位置上使用此选项。

<span id="_d"></span><span id="_D"></span>**/d**  
 (For **bm.exe** 仅) 将断点位置转换为地址。 因此，如果移动了代码，则断点将保留在同一地址，而不是根据 *SymbolPattern*进行设置。 当加载或卸载模块时，请使用 **/d** 避免对断点进行重新计算更改。

<span id="__"></span>**/(**  
 (For **bm.exe** 仅) 在 *SymbolString* 定义的符号字符串中包含参数列表信息。

利用此功能，可以在具有相同名称但参数列表不同的重载函数上设置断点。 例如，bm.exe/ ( myFunc 在 MyFunc 上设置断点 ** (int a) ** 和 **myFunc (char a) **。 如果不使用 "/ ("，则在 **myFunc** 上设置的断点将失败，因为它不指示断点适用的 **myFunc** 函数。

<span id="_______dxObjectExpression______"></span><span id="_______dxObjectExpression______"></span><span id="_______DXOBJECTEXPRESSION______"></span>**/w dx 对象表达式**基于 dx 对象表达式返回的布尔值设置条件断点。 参数是 (dx) 表达式的数据模型，该表达式的计算结果为 true (匹配条件–中断) 或 false (不匹配条件–不要中断) 。

此示例根据 localVariable 的值设置条件断点。

```dbgcmd
bp /w "localVariable == 4" mymodule!myfunction
```

此示例演示如何使用 JavaScript 设置断点。

```dbgcmd
bp /w "@$scriptContents.myFunc(localVariable)" @rip
```

有关调试器对象的详细信息，请参阅 [dx (显示调试器对象模型表达式) ](dx--display-visualizer-variables-.md)。

> [!NOTE] 
> /W 选项为试验，需要最新版本的调试器。 



<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定设置断点的指令的第一个字节。 如果省略 *Address*，则使用当前指令指针。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

<span id="_______Passes______"></span><span id="_______passes______"></span><span id="_______PASSES______"></span>*传递*   
指定在其上激活断点的执行传递的次数。 调试器将跳过断点位置，直到到达指定的通过。 Pass *的值可以是* 任何16位或32位值。

默认情况下，当应用程序第一次执行包含断点位置的代码时，断点将处于活动状态。 此默认情况相当于*传递*的值**1** 。 若要在应用程序至少执行一次代码之后激活断点，请输入值 **2** 或更多。 例如，如果值为 **2** ，则在第二次执行代码时激活断点。

此参数创建一个计数器，该计数器在每次通过代码时递减。 若要查看 *pass 计数器的* 初始值和当前值，请使用 [**Bl (断点列表) **](bl--breakpoint-list-.md)。

仅当应用程序在断点之后*执行*，以响应[**g (中转) **](g--go-.md)命令时， *pass 计数器才*会减少。 如果要单步执行代码或跟踪，则计数器不会减少。 当 pass *计数器达到* **1**时，可以通过清除并重置断点来重置它。

<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span>*Command.commandstring*   
指定每次遇到指定次数的断点时执行的命令的列表。 必须用引号将 *command.commandstring* 参数引起来。 使用分号分隔多个命令。

*Command.commandstring*中的调试器命令可以包含参数。 可以使用标准的 C 控制字符 (如** \\ n**和** \\ "**) 。 第二级引号中包含的分号 (** \\ "**) 被解释为嵌入的带引号字符串的一部分。

仅当在应用程序*执行*时响应[**g (中转) **](g--go-.md)命令时，才会执行*command.commandstring*命令。 如果要逐句通过此点的代码或跟踪，则不会执行这些命令。

在断点 (（如 **g** 或 **t**) 后恢复程序执行的任何命令都将结束命令列表的执行。

<span id="_______SymbolPattern______"></span><span id="_______symbolpattern______"></span><span id="_______SYMBOLPATTERN______"></span>*SymbolPattern*   
指定模式。 调试器尝试将此模式与现有符号匹配，并在所有模式匹配项上设置断点。 *SymbolPattern* 可以包含各种通配符和说明符。 有关此语法的详细信息，请参阅 [字符串通配符语法](string-wildcard-syntax.md)。 由于这些字符将与符号匹配，因此匹配不区分大小写，并且单个前导下划线 (\_) 表示任意数量的前导下划线。



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
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>All</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何使用断点、其他断点命令和控制断点的方法以及如何在用户空间中从内核调试器设置断点的详细信息，请参阅 [使用断点](using-breakpoints.md)。 有关条件断点的详细信息，请参阅 [设置条件断点](setting-a-conditional-breakpoint.md)。

<a name="remarks"></a>备注
-------

**Bp**、 **bu**和**bm.exe**命令设置了新断点，但它们具有不同的特征：

-   **最佳实践 (设置断点) **命令在命令中指定的断点位置的*地址*设置新断点。 如果在设置断点时，调试器无法解析断点位置的地址表达式，则 **bp** 断点会自动转换为 **bu** 断点。 如果卸载了模块，请使用 **bp** 命令创建一个不再处于活动状态的断点。

-   **Bu (设置未解析的断点) **命令设置*延迟*或*未解析*的断点。 **Bu**断点设置在对命令中指定的断点位置的符号引用上 (不在地址) 上，并且每当解析具有引用的模块时激活。 有关这些断点的详细信息，请参阅 [)  (Bu 断点的未解析断点 ](unresolved-breakpoints---bu-breakpoints-.md)。

-   **Bm.exe (设置符号断点) **命令在与指定模式匹配的符号上设置新断点。 此命令可创建多个断点。 默认情况下，匹配模式后， **bm.exe** 断点与 **bu** 断点相同。 也就是说， **bm.exe** 断点是在符号引用上设置的延迟断点。 但是，bm.exe/d 命令会创建一个或多个 **bp** 断点。 每个断点都在匹配位置的地址上设置，而不跟踪模块状态。

如果你不确定用于设置现有断点的命令，请使用 [**. bpcmds (显示断点命令) **](-bpcmds--display-breakpoint-commands-.md) 来列出所有断点以及用于创建断点的命令。

**Bp**断点与**bu**断点之间有三个主要差异：

-   **最佳**的断点位置始终转换为地址。 如果模块更改移动了用于设置 **bp** 断点的代码，则断点将保留在同一地址。 另一方面， **bu** 断点仍与符号值关联 (通常是符号加上所使用的偏移量) ，即使其地址发生更改，也会跟踪该符号位置。

-   如果在已加载的模块中找到 **bp** 断点地址，并且以后卸载该模块，则会从断点列表中删除该断点。 另一方面，在重复卸载和加载后， **bu** 断点会保持不变。

-   用 **bp** 设置的断点不保存在 WinDbg [工作区](using-workspaces.md)中。 用 **bu** 设置的断点保存在工作区中。

如果要在断点的符号模式中使用通配符， **bm.exe** 命令会很有用。 **Bm.exe** *SymbolPattern*语法等效于使用[**x SymbolPattern**](x--examine-symbols-.md) ，然后在每个结果上使用**bu** 。 例如，若要在 *myprogram.exe* 模块中的所有符号上设置以字符串 "mem" 开头的断点，请使用以下命令。

示例

```dbgcmd
0:000> bm myprogram!mem* 
  4: 0040d070 MyProgram!memcpy
 5: 0040c560 MyProgram!memmove
  6: 00408960 MyProgram!memset
```

由于 **bm.exe** 命令设置软件断点 (不) 处理器断点，因此在设置断点时，它会自动排除数据位置，以避免数据损坏。

使用 **bp** 或 bm.exe/a 命令时，可以指定数据地址而不是程序地址。 但是，即使指定了数据位置，这些命令也会创建软件断点，而不是处理器断点。 如果软件断点放置在程序数据而不是可执行代码中，则可能会导致数据损坏。 因此，仅当确信存储在该位置的内存将用作可执行代码而不是程序数据时，才应在数据位置使用这些命令。 否则，应改为使用 [**ba (访问) **](ba--break-on-access-.md) 命令。 有关更多详细信息，请参阅 [ (Ba 断点) 处理器断点 ](processor-breakpoints---ba-breakpoints-.md)。

若要详细了解如何在更复杂的语法指定的位置（例如 c + + 公共类的成员）或任意文本字符串（包含其他受限制的字符）设置断点，请参阅 [断点语法](breakpoint-syntax.md)。

如果一个逻辑源行跨越多个物理行，则在语句或调用的最后一个物理行上设置断点。 如果调试器无法在请求的位置设置断点，则会将该断点置于允许的下一个位置。

如果指定 *Thread*，则会在指定的线程上设置断点。 例如， ** ~ \* bp**命令在所有线程上设置断点， ** ~ \# bp**在导致当前异常的线程上设置断点， **~ 123bp**在线程123上设置断点。 **~ Bp**和 **~ bp**命令均在当前线程上设置断点。

调试内核模式下的多处理器系统时，使用 **bp** 或 ba 设置的断点 [** (在访问) **](ba--break-on-access-.md) 应用于所有处理器。 例如，如果当前处理器为3，并且你键入 **Bp MemoryAddress** 将断点置于 **MemoryAddress**中。 在该地址执行的任何处理器不仅 (处理器 3) 导致断点陷阱。

**Bp**、 **bu**和**bm.exe**命令通过用 break 指令替换处理器指令来设置软件断点。 若要调试只读代码或无法更改的代码，请使用 ba e 命令，其中 **e** 表示仅执行执行访问。

以下命令在函数 **MyTest**的开头之前设置一个断点12个字节。 对于前六次通过代码，将忽略此断点，但执行将在第7步通过代码时停止。

```dbgcmd
0:000> bp MyTest+0xb 7 
```

以下命令在 **RtlRaiseException**设置断点，显示 **eax** 寄存器，显示符号 **MyVar**的值，然后继续。

```dbgcmd
kd> bp ntdll!RtlRaiseException "r eax; dt MyVar; g"
```

以下两个 **bm.exe** 命令设置了三个断点。 执行这些命令时，显示的结果不区分用 **/d** 开关创建的断点以及不带它创建的断点。 [**Bpcmds (显示断点命令) **](-bpcmds--display-breakpoint-commands-.md)可用于区分这两种类型。 如果断点是通过**bm.exe**创建的，而不是使用 **/d**开关，则**bpcmds**显示将断点类型指示为**bu**，后面跟在 **@！ ""** 中的计算符号 标记 (指示它是一个文字符号，而不是数值表达式或寄存器) 。 如果断点是由 **bm.exe** 使用 **/d** 开关创建的，则 **bpcmds** 显示将断点类型指示为 **bp**。

```dbgcmd
0:000> bm myprog!openf* 
  0: 00421200 @!"myprog!openFile"
  1: 00427800 @!"myprog!openFilter"

0:000> bm /d myprog!closef* 
  2: 00421600 @!"myprog!closeFile"

0:000> .bpcmds
bu0 @!"myprog!openFile";
bu1 @!"myprog!openFilter";
bp2 0x00421600 ;
```

 

 





