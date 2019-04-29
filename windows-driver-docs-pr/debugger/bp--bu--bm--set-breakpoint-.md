---
title: bp、bu、bm（设置断点）
description: 最佳实践、 bu、 和 bm 命令设置一个或多个软件断点。 您可以组合位置、 条件和设置不同种类的软件断点的选项。
ms.assetid: 77d095fe-06d1-4842-ad49-8420ab4d5d72
keywords:
- 最佳实践，bu，bm （设置断点） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bp, bu, bm (Set Breakpoint)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 80efb09843561eb4b3d4bf360fc79980f1053346
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357627"
---
# <a name="bp-bu-bm-set-breakpoint"></a>bp、bu、bm（设置断点）


**Bp**， **bu**，并**bm**命令设置一个或多个软件断点。 您可以组合位置、 条件和设置不同种类的软件断点的选项。

User-Mode

```dbgcmd
[~Thread] bp[ID] [Options] [Address [Passes]] ["CommandString"] 
[~Thread] bu[ID] [Options] [Address [Passes]] ["CommandString"] 
[~Thread] bm [Options] SymbolPattern [Passes] ["CommandString"]
```

Kernel-Mode

```dbgcmd
bp[ID] [Options] [Address [Passes]] ["CommandString"] 
bu[ID] [Options] [Address [Passes]] ["CommandString"] 
bm [Options] SymbolPattern [Passes] ["CommandString"]
```

## <a name="span-idddkcmdsetbreakpointdbgspanspan-idddkcmdsetbreakpointdbgspanparameters"></a><span id="ddk_cmd_set_breakpoint_dbg"></span><span id="DDK_CMD_SET_BREAKPOINT_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
指定断点适用于的线程。 有关语法的详细信息，请参阅[线程语法](thread-syntax.md)。 仅在用户模式下，可以指定线程。 如果不指定线程，该断点适用于所有线程。

<span id="_______ID______"></span><span id="_______id______"></span> *ID*   
指定标识断点的十进制数。

调试器将分配*ID*时创建所需断点，但您可以通过使用对其进行更改[ **br （断点重新编号）** ](br--breakpoint-renumber-.md)命令。 可以使用*ID*来指代更高版本的调试器命令中的断点。 若要显示*ID*的断点、 使用[ **bl （断点列表）** ](bl--breakpoint-list-.md)命令。

当你使用*ID*命令时，请不要键入该命令之间有空格 (**bp**或**bu**) 和 ID 号。

*ID*参数始终是可选的。 如果未指定*ID*，调试器使用的第一个可用的断点号。 在内核模式下，您可以设置只有 32 断点。 在用户模式下，可以设置任意数量的断点。 在任一情况下，没有任何限制的值*ID*数。 如果将括*ID*用方括号括起来 (**\[\]**)， *ID*可以包含任何表达式。 有关语法的详细信息，请参阅[数值表达式语法](numerical-expression-syntax.md)。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
指定断点的选项。 所示，可以指定任意数量的以下选项，除非：

<span id="_1"></span>**/1**  
创建"单稳"断点。 触发此断点后，它是从断点列表中删除。

<span id="_f_PredNum"></span><span id="_f_prednum"></span><span id="_F_PREDNUM"></span>**/f** *PredNum*  
（基于 Itanium 的仅限用户仅模式）指定的谓词的数字。 断点都与相应的谓词寄存器。 (例如， **bp /f 4** *地址*设置的前提是使用断点**p4**谓词寄存器。)

<span id="_p_EProcess"></span><span id="_p_eprocess"></span><span id="_P_EPROCESS"></span>**/p** *EProcess*  
（仅内核模式）指定与此断点关联的进程。 *EProcess*应为 EPROCESS 结构，不 PID 的实际地址。 仅当遇到此进程的上下文中触发断点。

<span id="_t_EThread"></span><span id="_t_ethread"></span><span id="_T_ETHREAD"></span>**/t** *EThread*  
（仅内核模式）指定与此断点关联的线程。 *EThread*应的实际地址 ETHREAD 结构，不是线程 id。 仅当遇到此线程的上下文中触发断点。 如果您使用 **/p** *EProcess*并 **/t** *EThread*，可以按任意顺序输入它们。

<span id="_c_MaxCallStackDepth"></span><span id="_c_maxcallstackdepth"></span><span id="_C_MAXCALLSTACKDEPTH"></span>**/c** *MaxCallStackDepth*  
仅当调用堆栈深度为时激活该断点小于*MaxCallStackDepth*。 不能使用此选项一起使用 **/C**。

<span id="_C_MinCallStackDepth"></span><span id="_c_mincallstackdepth"></span><span id="_C_MINCALLSTACKDEPTH"></span>**/C** *MinCallStackDepth*  
仅当调用堆栈深度大于激活断点*MinCallStackDepth*。 不能使用此选项一起使用 **/c**。

<span id="_a"></span><span id="_A"></span>**/a**  
(有关**bm**仅) 上的所有指定的位置中，设置断点，不管它们是在数据空间或代码空间。 数据上的断点可能会导致程序失败，因为使用此选项仅在已知安全的位置上。

<span id="_d"></span><span id="_D"></span>**/d**  
(有关**bm**仅) 将断点位置转换为地址。 因此，如果移动代码，这些断点会保留在相同的地址，而不是被设置为根据*SymbolPattern*。 使用 **/d**以避免重新计算对断点的更改，当加载或卸载模块。

<span id="__"></span>**/(**  
(有关**bm**仅) 包括在符号中的参数列表信息字符串*SymbolString*定义。

此功能，可对具有相同名称但不同的参数列表的重载函数设置断点。 例如，bm / (myFunc 上设置断点**myFunc(int a)** 并**myFunc(char a)**。 无需"/ (", 设置一个断点**myFunc**失败，因为它并不表示该**myFunc**断点适用于函数。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定在其中设置断点的指令的第一个字节。 如果省略*地址*，使用当前指令指针。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______Passes______"></span><span id="_______passes______"></span><span id="_______PASSES______"></span> *传递*   
指定在激活该断点的执行阶段的数量。 调试器会跳过断点位置，直到它达到指定的传递。 值*传递*可以是任何 16 位或 32 位值。

默认情况下，断点处于活动状态的应用程序执行包含断点位置的代码的第一个时间。 此默认情况下是值的等效**1**有关*传递*。 若要激活该断点仅在程序执行的代码在至少一次后，输入值**2**或详细信息。 例如，值**2**激活断点执行的代码的第二个时间。

此参数创建一个计数器，它将减少在每次通过代码。 若要查看的初始和当前值*Pass*计数器的信息，使用[ **bl （断点列表）**](bl--breakpoint-list-.md)。

*Pass*计数器是递减仅当应用程序*执行*过去的响应中的断点[ **g （转向）** ](g--go-.md)命令。 该计数器如果逐句通过代码或跟踪过去它不会减少。 当*Pass*计数器达到**1**，您可以仅通过清除和重置断点重置它。

<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
指定断点是每次执行的命令的列表中遇到指定的次数。 必须将*CommandString*在引号中的参数。 使用分号分隔多个命令。

调试器中的命令*CommandString*可以包括参数。 可以使用标准的 C-控制字符 (如 **\\n**并 **\\"**)。 包含在第二级别引号中的分号 (**\\"**) 被解释为属于嵌入带引号的字符串。

*CommandString*到达断点时该应用程序时，才会执行命令*执行*响应[ **g （转向）** ](g--go-.md)命令。 如果您要单步执行代码或跟踪忽略这一点，不会执行命令。

任一命令恢复程序执行在断点后的 (如**g**或**t**) 结束执行命令列表。

<span id="_______SymbolPattern______"></span><span id="_______symbolpattern______"></span><span id="_______SYMBOLPATTERN______"></span> *SymbolPattern*   
指定一种模式。 调试器会尝试以匹配此模式与现有的符号并且将在所有模式匹配项上设置断点。 *SymbolPattern*可以包含各种通配符和说明符。 有关此语法的详细信息，请参阅[字符串通配符语法](string-wildcard-syntax.md)。 要与符号匹配这些字符，因为匹配时不区分大小写，并在单个前导下划线 (\_) 表示任意数量的前导下划线。

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
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息和如何使用断点、 其他断点的命令和控制断点的方法以及如何从内核调试程序在用户空间中设置断点的示例，请参阅[使用断点](using-breakpoints.md)。 有关条件断点的详细信息，请参阅[设置条件断点](setting-a-conditional-breakpoint.md)。

<a name="remarks"></a>备注
-------

**Bp**， **bu**，并**bm**命令设置新断点，但它们具有不同的特征：

-   **（设置断点） 最佳实践**命令设置新断点处*地址*命令中指定的断点位置。 如果调试器无法解析的地址表达式的断点位置设置断点时， **bp**断点将自动转换为**bu**断点。 使用**bp**命令以创建该模块的不再是活动如果断点被卸载。

-   **Bu （设置无法解析断点）** 命令集*延迟*或*无法解析*断点。 一个**bu**断点位置 （而不是在上一个地址） 在命令中指定并解决与引用的模块时激活的符号引用上设置断点。 有关这些断点的详细信息，请参阅[无法解析断点 (bu 断点)](unresolved-breakpoints---bu-breakpoints-.md)。

-   **Bm （设置符号断点）** 命令与指定的模式匹配的符号上设置新断点。 此命令可以创建多个断点。 默认情况下，匹配模式，则后**bm**断点将与相同**bu**断点。 即**bm**断点是延迟的符号引用设置的断点。 但是，bm /d 命令创建一个或多个**bp**断点。 每个断点的匹配位置的地址上设置并不会跟踪模块状态。

如果您不确定使用哪个命令设置现有断点，请使用[ **.bpcmds （显示断点命令）** ](-bpcmds--display-breakpoint-commands-.md)若要列出所有断点以及用来创建它们的命令。

有三个主要区别**bp**断点并**bu**断点：

-   一个**bp**断点位置始终转换为一个地址。 如果模块更改的移动代码**bp**设置了断点，断点仍保持在相同的地址。 但是， **bu**断点仍与已使用的符号值 （通常是一个符号加上偏移量） 相关联，还会跟踪此符号的位置，即使其地址发生变化。

-   如果**bp**断点地址是位于已加载模块，并且如果该模块是更高版本中卸载，从断点列表中删除断点。 但是， **bu**重复的卸载和加载后保留断点。

-   使用设置的断点**bp**不会保存在 WinDbg[工作区](using-workspaces.md)。 使用设置的断点**bu**保存在工作区中。

**Bm**命令很有用，当你想要针对某个断点符号模式中使用通配符。 **Bm** *SymbolPattern*语法相当于使用[ **x SymbolPattern** ](x--examine-symbols-.md) ，然后使用**bu**上的每个结果。 例如，若要在所有中的符号上设置断点*Myprogram*字符串"内存优化，"开头的模块使用以下命令。

示例

```dbgcmd
0:000> bm myprogram!mem* 
  4: 0040d070 MyProgram!memcpy
 5: 0040c560 MyProgram!memmove
  6: 00408960 MyProgram!memset
```

因为**bm**命令设置软件断点 （而不是处理器断点），它会自动排除数据位置时设置断点，以避免会损坏数据。

可以使用时指定数据地址而不是程序地址**bp**或 bm/a 命令。 但是，即使指定的数据位置，这些命令将创建软件断点、 不处理器断点。 如果软件断点放置在程序数据，而不是可执行代码中，它可能会导致数据损坏。 因此您应使用这些命令的数据位置仅当确定该存储中存储为可执行代码而不是程序数据，将使用位置的内存。 否则，应使用[ **ba （中断的访问权限）** ](ba--break-on-access-.md)命令。 有关更多详细信息，请参阅[处理器断点 (ba 断点)](processor-breakpoints---ba-breakpoints-.md)。

有关如何指定更复杂的语法，例如的成员的位置上设置断点的详细信息C++公共类，或一个任意文本字符串，其中包含不允许的字符，请参阅[断点语法](breakpoint-syntax.md)。

如果包含一个逻辑源行跨多个物理行，语句或调用的最后一个物理行上设置断点。 如果调试器无法在请求的位置设置断点，它将断点放在下一个允许的位置。

如果指定*线程*，在指定的线程上设置断点。 例如，  **~ \*bp**命令在所有线程上设置断点 **~ \#bp**使当前线程上设置断点异常，并 **~ 123bp**线程 123 上设置断点。 **~ Bp**并 **~.bp**同时在当前线程上设置断点的命令。

在调试多处理器系统在内核模式下，使用设置的断点**bp**或[ **ba （中断的访问权限）** ](ba--break-on-access-.md)适用于所有处理器。 例如，如果当前处理器 3，并键入**bp MemoryAddress**若要放置在一个断点**MemoryAddress**。 在该地址 （不只是处理器 3） 执行任何处理器会导致断点陷阱。

**Bp**， **bu**，并**bm**命令由处理器指令替换为中断指令设置软件断点。 若要调试仅限读的代码或不能更改的代码，使用 ba e 命令，其中**e**表示只执行访问权限。

以下命令设置断点函数的开头过去的 12 个字节**MyTest**。 对于在前六个阶段执行代码，将忽略此断点，但将在执行代码的第七个传递停止执行。

```dbgcmd
0:000> bp MyTest+0xb 7 
```

以下命令将设置一个断点处**RtlRaiseException**，将显示**eax**注册详细信息，显示的符号值**MyVar**，并继续执行。

```dbgcmd
kd> bp ntdll!RtlRaiseException "r eax; dt MyVar; g"
```

以下两个**bm**命令设置三个断点。 命令执行时，显示的结果不会区分使用创建的断点 **/d**开关以及创建并没有它。 [ **.Bpcmds （显示断点命令）** ](-bpcmds--display-breakpoint-commands-.md)可用来区分这两种类型。 如果通过创建断点**bm**而无需 **/d**切换，请 **.bpcmds**显示指示的断点类型**bu**，后面是由计算括起来的符号 **@ ！""** （这表明它是一种文字符号并不是数值表达式或注册） 的标记。 如果通过创建断点**bm**与 **/d**切换，请 **.bpcmds**显示指示的断点类型**bp**。

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

 

 





