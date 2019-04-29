---
title: ba（访问时中断）
description: Ba 命令设置处理器断点 （通常称为，不太准确地说，数据断点）。 访问指定的内存时，会触发此断点。
ms.assetid: 0d39d883-363e-421b-a1b8-08bf2d216724
keywords:
- ba （中断的访问权限） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ba (Break on Access)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9b47a8b7ca128f12293ad5a63c2d46e8ffb567d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355386"
---
# <a name="ba-break-on-access"></a>ba（访问时中断）


**Ba**命令设置处理器断点 (通常称为，小于准确地说，*数据断点*)。 访问指定的内存时，会触发此断点。

User-Mode

```dbgcmd
[~Thread] ba[ID] Access Size [Options] [Address [Passes]] ["CommandString"]
```

Kernel-Mode

```dbgcmd
ba[ID] Access Size [Options] [Address [Passes]] ["CommandString"]
```

## <a name="span-idddkcmdbreakonaccessdbgspanspan-idddkcmdbreakonaccessdbgspanparameters"></a><span id="ddk_cmd_break_on_access_dbg"></span><span id="DDK_CMD_BREAK_ON_ACCESS_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
指定断点适用于的线程。 有关语法的详细信息，请参阅[线程语法](thread-syntax.md)。 仅在用户模式下，可以指定线程。

<span id="_______ID______"></span><span id="_______id______"></span> *ID*   
指定可选的数字，用于标识该断点。 如果未指定*ID*，使用第一个可用的断点数字。 无法添加间距**ba**和 ID 号。 每个处理器支持只有有限的数量的处理器断点，但没有任何限制的值*ID*数。 如果将括*ID*用方括号括起来 (\[\])， *ID*可以包含任何表达式。 有关语法的详细信息，请参阅[数值表达式语法](numerical-expression-syntax.md)。

<span id="_______Access______"></span><span id="_______access______"></span><span id="_______ACCESS______"></span> *Access*   
指定满足断点的访问的类型。 此参数可以是下列值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Option</th>
<th align="left">操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>e</strong> （执行）</p></td>
<td align="left"><p>当 CPU 检索一条指令从指定的地址时进入调试器。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r</strong> （读/写）</p></td>
<td align="left"><p>当 CPU 读取或写入指定地址处时进入调试器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>w</strong> （写入）</p></td>
<td align="left"><p>进入调试器，当 CPU 将在指定的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>i</strong> (i/o)</p></td>
<td align="left"><p>（内核模式下唯一的、 基于 x86 的系统仅）在指定 I/O 端口时中断到调试器<em>地址</em>访问。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span> *大小*   
指定位置，的大小以字节为单位，若要监视的访问权限。 在基于 x86 的处理器上，此参数可以是 1、 2 或 4。 但是，如果*访问*等于**e**，*大小*必须为 1。

在基于 x64 的处理器上，此参数可以是 1、 2、 4 或 8。 但是，如果*访问*等于**e**，*大小*必须为 1。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
指定断点的选项。 所示，可以使用任意数量的以下选项除外：

<span id="_1"></span>**/1**  
创建"单稳"断点。 触发此断点后，断点永久从断点列表中删除。

<span id="_p_EProcess"></span><span id="_p_eprocess"></span><span id="_P_EPROCESS"></span>**/p** *EProcess*  
（仅适用于内核模式）指定与此断点关联的进程。 *EProcess*应为 EPROCESS 结构，不 PID 的实际地址。 仅当遇到此进程的上下文中触发断点。

<span id="_t_EThread"></span><span id="_t_ethread"></span><span id="_T_ETHREAD"></span>**/t** *EThread*  
（仅适用于内核模式）指定与此断点关联的线程。 *EThread*应的实际地址 ETHREAD 结构，不是线程 id。 仅当遇到此线程的上下文中触发断点。 如果您使用 **/p** *EProcess*并 **/t** *EThread* ，可以按任意顺序输入它们。

<span id="_c_MaxCallStackDepth"></span><span id="_c_maxcallstackdepth"></span><span id="_C_MAXCALLSTACKDEPTH"></span>**/c** *MaxCallStackDepth*  
会导致断点处于活动状态，只有当调用堆栈深度是小于*MaxCallStackDepth*。 不能将此选项一起使用的组合 **/C**。

<span id="_C_MinCallStackDepth"></span><span id="_c_mincallstackdepth"></span><span id="_C_MINCALLSTACKDEPTH"></span>**/C** *MinCallStackDepth*  
会导致断点处于活动状态，仅当调用堆栈深度大于*MinCallStackDepth*。 不能将此选项一起使用的组合 **/c**。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定任何有效的地址。 如果应用程序访问在此地址的内存，调试器将停止执行，并显示所有寄存器和标志的当前值。 此地址必须是偏移量并适当对齐到匹配*大小*参数。 (例如，如果*大小*为 4，*地址*必须是 4 的倍数。)如果省略*地址*，使用当前指令指针。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______Passes______"></span><span id="_______passes______"></span><span id="_______PASSES______"></span> *传递*   
指定断点通过传递，直到它激活次数。 此数字可以是任何 16 位值。 通过此点中没有重大是一个程序计数器传递次数小于此数值的值。 因此，省略此数字是等于 1 的设置相同。 此数计数的时间仅另请注意，该应用程序*执行*忽略这一点。 单步执行或忽略这一点跟踪不会。 达到最大计数后，您可以重置此数字仅清除和重置断点。

<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
指定一系列命令执行断点是每次遇到指定的次数。 仅当您发出后命中断点，则执行这些命令[ **g （转向）** ](g--go-.md)命令，而不是后[ **t (Trace)** ](t--trace-.md)或[ **p （步骤）** ](p--step-.md)命令。 调试器中的命令*CommandString*可以包括参数。

必须将此命令字符串括在引号中，并应由分号分隔多个命令。 可以使用标准 C 控制字符 (如 **\\n**并 **\\"**)。 包含在第二级别引号中的分号 (**\\"**) 被解释为属于嵌入带引号的字符串。

该参数为可选参数。

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

有关处理器断点的详细信息，请参阅[处理器断点 (ba 断点)](processor-breakpoints---ba-breakpoints-.md)。 有关详细信息和使用断点、 其他断点的命令和控制断点，并了解如何从内核调试程序在用户空间中设置断点的方法的示例，请参阅[使用断点](using-breakpoints.md). 有关条件断点的详细信息，请参阅[设置条件断点](setting-a-conditional-breakpoint.md)。

<a name="remarks"></a>备注
-------

调试器使用*ID*编号，以更高版本参考中的断点[ **bc （清除断点）**](bc--breakpoint-clear-.md)， [ **（断点禁用）bd**](bd--breakpoint-disable-.md)，并[**是 （启用断点）** ](be--breakpoint-enable-.md)命令。

使用[ **bl （断点列表）** ](bl--breakpoint-list-.md)命令列出所有现有断点、 它们的 ID 号，以及它们的状态。

使用[ **.bpcmds （显示断点命令）** ](-bpcmds--display-breakpoint-commands-.md)命令列出所有现有断点、 它们的 ID 号，以及用于创建它们的命令。

每个处理器断点具有与之关联的大小。 例如， **w** （写入） 无法在大小为 4 个字节的地址 0x70001008 设置处理器断点。 这将监视从 0x70001008 到 0x7000100B，非独占地址块。 如果此内存块写入后，将触发断点。

它可能处理器执行操作的内存区域的*重叠*，但不等于指定的区域。 在此示例中，单个写入操作，包括范围 0x70001000 到 0x7000100F 或包含仅在 0x70001009，字节写入操作将是重叠的操作。 在这种情况下，触发断点是否与处理器相关。 有关特定详细信息，应该咨询处理器手册。 若要对 x86 处理器、 读取或写入断点每当访问的范围重叠的断点范围就会触发其执行一个特定实例。

同样，如果**e** （执行） 上的地址 0x00401003，设置断点和执行这些地址 0x00401002 和 0x00401003 双字节指令跨越，则结果是处理器相关。 同样，有关详细信息需要查阅处理器体系结构手册。

处理器区分用户模式下调试程序设置的断点和内核模式调试程序设置的断点。 用户模式下处理器断点不会影响任何内核模式的进程。 内核模式下处理器断点可能会或可能不会影响用户模式进程，具体取决于用户模式代码使用调试注册状态以及是否有用户模式下调试程序附加。

若要应用到不同的寄存器上下文当前进程的现有数据断点，使用[ **.apply\_dbp （到上下文应用数据断点）** ](-apply-dbp--apply-data-breakpoint-to-context-.md)命令。

在多处理器计算机中，每个处理器断点适用于所有处理器。 例如，如果当前处理器 3，并使用命令`ba e1 MyAddress`要将断点放在 MyAddress，任何处理器--不仅 3--执行处理器在该地址将触发断点。 （它将保存为软件的断点。）

不能在相同的唯一区别的地址创建多个处理器断点他们*CommandString*值。 但是，可以创建多个断点在相同的位置具有不同的限制 (例如，不同的值的 **/p**， **/t**， **/c**，和 **/C**选项)。

有关处理器断点，并向其应用的其他限制的详细信息，请参阅[处理器断点 (ba 断点)](processor-breakpoints---ba-breakpoints-.md)。

下面的示例演示**ba**命令。 以下命令设置 4 个字节的变量 myVar 上的读取访问权限的断点。

```dbgcmd
0:000> ba r4 myVar
```

以下命令从通过 0x3FB 0x3F8 地址与所有串行端口上添加断点。 如果任何读取或写入到这些端口时，会触发此断点。

```dbgcmd
kd> ba i4 3f8
```

 

 





