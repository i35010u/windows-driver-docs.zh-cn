---
title: ba（访问时中断）
description: Ba 命令设置一个处理器断点，该断点 (经常称为) 的数据断点。 当访问指定的内存时，将触发此断点。
keywords:
- ba (在访问) Windows 调试时中断
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ba (Break on Access)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d9122343c4946be61da2821d81d3ab594017ec7e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826185"
---
# <a name="ba-break-on-access"></a>ba（访问时中断）


**Ba** 命令设置一个处理器断点，该断点 (经常称为) 的 *数据断点*。 当访问指定的内存时，将触发此断点。

User-Mode

```dbgcmd
[~Thread] ba[ID] Access Size [Options] [Address [Passes]] ["CommandString"]
```

Kernel-Mode

```dbgcmd
ba[ID] Access Size [Options] [Address [Passes]] ["CommandString"]
```

## <a name="span-idddk_cmd_break_on_access_dbgspanspan-idddk_cmd_break_on_access_dbgspanparameters"></a><span id="ddk_cmd_break_on_access_dbg"></span><span id="DDK_CMD_BREAK_ON_ACCESS_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
指定断点适用的线程。 有关语法的详细信息，请参阅 [线程语法](thread-syntax.md)。 只能在用户模式下指定线程。

<span id="_______ID______"></span><span id="_______id______"></span>*ID*   
指定标识断点的可选数字。 如果未指定 *ID*，则使用第一个可用的断点号。 你无法在 **ba** 和 ID 号之间添加空格。 每个处理器仅支持有限数量的处理器断点，但对于 *ID* 号值没有限制。 如果用方括号将 *id* 括起来 (\[ \]) ， *ID* 可以包含任何表达式。 有关语法的详细信息，请参阅 [数值表达式语法](numerical-expression-syntax.md)。

<span id="_______Access______"></span><span id="_______access______"></span><span id="_______ACCESS______"></span>*访问*   
指定满足断点的访问类型。 此参数可以是下列值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>e</strong> (执行) </p></td>
<td align="left"><p>当 CPU 从指定的地址检索指令时，中断到调试器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>读/写) <strong>r</strong> (</p></td>
<td align="left"><p>当 CPU 读取或写入指定地址时，中断调试器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>w</strong> (写入) </p></td>
<td align="left"><p>当 CPU 写入指定地址时中断调试器。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>我</strong> (i/o) </p></td>
<td align="left"><p>仅 (内核模式，如果访问指定 <em>地址</em> 处的 i/o 端口，则仅限基于 x86 的系统) 中断到调试器。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span>*大小*   
指定监视访问的位置大小（以字节为单位）。 在基于 x86 的处理器上，此参数可以是1、2或4。 但是，如果 *访问* 等于 **e**，则 *大小* 必须为1。

在基于 x64 的处理器上，此参数可以是1、2、4或8。 但是，如果 *访问* 等于 **e**，则 *大小* 必须为1。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
指定断点选项。 你可以使用以下任意数量的选项，除非指定：

<span id="_1"></span>**/1**  
创建 "一步" 断点。 触发此断点后，断点将从断点列表中永久删除。

<span id="_p_EProcess"></span><span id="_p_eprocess"></span><span id="_P_EPROCESS"></span>**/P** *EProcess*  
仅 (内核模式) 指定与此断点关联的进程。 *EProcess* 应是 EProcess 结构的实际地址，而不是 PID。 仅当在此进程的上下文中遇到断点时才触发断点。

<span id="_t_EThread"></span><span id="_t_ethread"></span><span id="_T_ETHREAD"></span>**/T** *EThread*  
仅 (内核模式) 指定与此断点关联的线程。 *EThread* 应是 EThread 结构的实际地址，而不是线程 ID。 仅当在此线程的上下文中遇到断点时才触发断点。 如果使用 **/P** *EProcess* 和 **/t** *EThread* ，则可以按任意顺序输入。

<span id="_c_MaxCallStackDepth"></span><span id="_c_maxcallstackdepth"></span><span id="_C_MAXCALLSTACKDEPTH"></span>**/c** *MaxCallStackDepth*  
使断点仅在调用堆栈深度小于 *MaxCallStackDepth* 时才处于活动状态。 不能将此选项与 **/c** 组合在一起。

<span id="_C_MinCallStackDepth"></span><span id="_c_mincallstackdepth"></span><span id="_C_MINCALLSTACKDEPTH"></span>**/C** *MinCallStackDepth*  
使断点仅在调用堆栈深度大于 *MinCallStackDepth* 时才处于活动状态。 不能将此选项与 **/c** 组合在一起。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定任何有效的地址。 如果应用程序在此地址访问内存，调试器将停止执行，并显示所有寄存器和标志的当前值。 此地址必须是偏移量，并适当调整以匹配 *大小* 参数。  (例如，如果 *Size* 为4，则 *Address* 必须是4的倍数 ) 。如果省略 *address*，则使用当前指令指针。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

<span id="_______Passes______"></span><span id="_______passes______"></span><span id="_______PASSES______"></span>*传递*   
指定在激活断点之前断点的次数。 此数字可以是任何16位值。 程序计数器在不中断的情况下传递到此点的次数小于此数字的值。 因此，省略此数字与将其设置为等于1相同。 另请注意，此数字只计算应用程序在此点之后 *执行* 的时间。 此点之后的单步执行或跟踪不计数。 达到完整计数后，只能通过清除并重置断点来重置此数字。

<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span>*Command.commandstring*   
指定每次遇到指定次数的断点时要执行的命令的列表。 仅当发出 [**g (中转)**](g--go-.md) 命令，而不是在 [**t (Trace)**](t--trace-.md) 或 [**p (步骤)**](p--step-.md) 命令后，才会执行这些命令。 *Command.commandstring* 中的调试器命令可以包含参数。

必须用引号将此命令字符串括起来，并且应该用分号分隔多个命令。 可以使用标准的 C 控制字符 (如 **\\ n** 和 **\\ "**) 。 第二级引号中包含的分号 (**\\ "**) 被解释为嵌入的带引号字符串的一部分。

此参数是可选的。

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
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关处理器断点的详细信息，请参阅 [ (Ba 断点) 处理器断点 ](processor-breakpoints---ba-breakpoints-.md)。 有关使用断点的详细信息和使用断点、其他断点命令和控制断点的方法的详细信息，以及如何在用户空间中从内核调试器设置断点的详细信息，请参阅 [使用断点](using-breakpoints.md)。 有关条件断点的详细信息，请参阅 [设置条件断点](setting-a-conditional-breakpoint.md)。

<a name="remarks"></a>备注
-------

调试器使用 *ID* 号在以后的 bc 中引用断点 [**(断点清除)**](bc--breakpoint-clear-.md)、 [**bd (断点禁用)**](bd--breakpoint-disable-.md)，并 [**(断点启用)**](be--breakpoint-enable-.md) 命令。

使用 [**bl (断点列表)**](bl--breakpoint-list-.md) 命令可列出所有现有断点、其 ID 号及其状态。

使用 [**bpcmds (显示断点命令)**](-bpcmds--display-breakpoint-commands-.md) 命令可列出所有现有断点、其 ID 号以及用于创建它们的命令。

每个处理器断点都具有与之关联的大小。 例如，可以在0x70001008 的地址（大小为四个字节）设置一个 **w** (写入) 处理器断点。 这会监视0x70001008 到0x7000100B （含）之间的地址块。 如果将此内存块写入，则会触发断点。

出现这种情况的原因是，处理器对与指定的区域 *重叠* 但不完全相同的内存区域执行操作。 在此示例中，包含0x70001000 到0x7000100F 的范围的单个写入操作或只包含0x70001009 中的字节的写入操作将是重叠操作。 在这种情况下，是否触发断点与处理器相关。 有关具体的详细信息，请参阅处理器手册。 若要获取一个特定实例，在 x86 处理器上，只要访问的范围与断点范围重叠，就会触发读取或写入断点。

同样，如果在地址0x00401003 上设置 **e** (执行) 断点，然后执行跨地址0x00401002 和0x00401003 的双字节指令，则结果与处理器相关。 同样，有关详细信息，请参阅处理器体系结构手册。

处理器区分用户模式调试器设置的断点和内核模式调试器设置的断点。 用户模式处理器断点不会影响任何内核模式进程。 内核模式处理器断点可能会也可能不会影响用户模式进程，具体取决于用户模式代码是否使用调试寄存器状态以及是否已附加用户模式调试器。

若要将当前进程的现有数据断点应用于其他寄存器上下文，请使用 [**。应用 \_ .Dbp (将数据断点应用于上下文)**](-apply-dbp--apply-data-breakpoint-to-context-.md) 命令。

在多处理器计算机上，每个处理器断点都适用于所有处理器。 例如，如果当前处理器为3，并且使用命令 `ba e1 MyAddress` 在 MyAddress 中放置一个断点，则在该地址执行的任何处理器（不仅是处理器3）都将触发断点。  (这也适用于软件断点。 ) 

不能在与 *command.commandstring* 值不同的同一地址上创建多个处理器断点。 但是，可以在具有不同限制的同一地址上创建多个断点 (例如， **/p**、 **/t**、 **/c** 和 **/c** 选项的不同值) 。

有关处理器断点的详细信息以及适用于这些断点的其他限制，请参阅 [)  (Ba 断点的处理器断点 ](processor-breakpoints---ba-breakpoints-.md)。

以下示例显示了 **ba** 命令。 以下命令将设置一个断点，以在 myVar 的4个字节的情况下进行读取访问。

```dbgcmd
0:000> ba r4 myVar
```

以下命令在包含0x3F8 到0x3FB 地址的所有串行端口上添加一个断点。 如果读取或写入到这些端口，则触发此断点。

```dbgcmd
kd> ba i4 3f8
```

 

 





