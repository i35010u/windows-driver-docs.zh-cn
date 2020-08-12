---
title: '处理器断点 (ba 断点) '
description: '处理器断点 (ba 断点) '
ms.assetid: 2681cebd-dce2-48f1-8953-9af65d15f378
keywords:
- 断点，处理器断点
- 断点，数据断点
- 断点，软件断点
- 断点、BP 与 BA
- 软件断点
- 软件断点，概述
- 软件断点，限制
- 处理器断点
- 处理器断点，概述
ms.date: 05/13/2020
ms.localizationpriority: medium
ms.openlocfilehash: b69a277ee9f335b48296eb8f5ea7bcf506fd6d26
ms.sourcegitcommit: bb3b62a57ba3aea4a0adeefd2d81993367b7b334
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88148400"
---
# <a name="processor-breakpoints-ba-breakpoints"></a>处理器断点 (ba 断点) 


由处理器在调试器请求控制的断点称为 *处理器断点* 或 *数据断点*。 由调试器直接控制的断点称为 " *软件断点*"。

**注意**   尽管术语*数据断点*通常用作*处理器断点*的同义词，但这一术语可能会产生误导。 有两种基本类型的断点：处理器断点由处理器控制，软件断点由调试器控制。 处理器断点通常是在程序数据上设置的，这就是所谓的 "数据断点"，但也可以在可执行代码上设置。 软件断点通常设置为可执行代码，但也可以在程序数据上进行设置。 遗憾的是，调试文献通常会将处理器断点称为 "数据断点"，即使它们是在可执行代码上设置的也是如此。

 

### <a name="span-idprocessor_breakpointsspanspan-idprocessor_breakpointsspanprocessor-breakpoints"></a><span id="processor_breakpoints"></span><span id="PROCESSOR_BREAKPOINTS"></span>处理器断点

当访问特定内存位置时，将触发处理器断点。 有四种类型的处理器断点，它们对应于触发它的内存访问类型：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">断点类型</th>
<th align="left">操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>e</strong> (执行) </p></td>
<td align="left"><p>处理器检索指定地址的指令时触发。</p></td>
</tr>
<tr class="even">
<td align="left"><p>读/写) <strong>r</strong> (</p></td>
<td align="left"><p>处理器在指定地址读取或写入内存时触发。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>w</strong> (写入) </p></td>
<td align="left"><p>当处理器写入指定地址处的内存时触发。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>我</strong> (i/o) </p></td>
<td align="left"><p>当访问指定 <em>地址</em> 处的 i/o 端口时触发。</p></td>
</tr>
</tbody>
</table>

 

每个处理器断点都具有与之关联的大小。 例如，可以在0x70001008 的地址（大小为四个字节）设置一个 **w** (写入) 处理器断点。 这会监视0x70001008 到0x7000100B （含）之间的地址块。 如果将此内存块写入，则会触发断点。

出现这种情况的原因是，处理器对与指定的区域重叠但不完全相同的内存区域执行操作。 在上一段落中给出的示例中，包含0x70001000 到0x7000100F 范围的单个写入操作或只包含0x70001009 中的字节的写入操作将是重叠操作。 在这种情况下，是否触发断点与处理器相关。 有关如何在特定处理器上处理此情况的详细信息，请参阅 processor archictecture 手册并查找 "调试寄存器" 或 "调试控制寄存器"。 若要采用某种特定的处理器类型作为示例，在 x86 处理器上，只要访问的范围与断点范围重叠，就会触发读取或写入断点。

同样，如果在地址0x00401003 上设置 **e** (执行) 断点，然后执行跨地址0x00401002 和0x00401003 的双字节指令，则结果与处理器相关。 同样，有关详细信息，请参阅处理器体系结构手册。

处理器区分用户模式调试器设置的断点和内核模式调试器设置的断点。 用户模式处理器断点不会影响任何内核模式进程。 内核模式处理器断点可能会也可能不会影响用户模式进程，具体取决于用户模式代码是否使用调试寄存器状态以及是否已附加用户模式调试器。

若要将当前进程的现有数据断点应用于其他寄存器上下文，请使用 [**。应用 \_ .Dbp (将数据断点应用于上下文) **](-apply-dbp--apply-data-breakpoint-to-context-.md) 命令。

在多处理器计算机上，每个处理器断点都适用于所有处理器。 例如，如果当前处理器为3，并且使用命令 `ba e1 MyAddress` 在 **MyAddress**中放置一个断点，则在该地址执行的任何处理器（不仅是处理器3）都将触发断点。 这也适用于软件断点。

### <a name="span-idsoftware_breakpointsspanspan-idsoftware_breakpointsspansoftware-breakpoints"></a><span id="software_breakpoints"></span><span id="SOFTWARE_BREAKPOINTS"></span>软件断点

与处理器断点不同，软件断点由调试器控制。 当调试器在某个位置设置软件断点时，它会使用中断指令暂时替换该内存位置的内容。 调试器会记住此位置的原始内容，因此，如果此内存显示在调试器中，调试器将显示该内存位置的原始内容，而不是中断指令。 当目标进程在此位置执行代码时，中断指令会使进程进入调试器。 在您执行了您选择的任何操作后，您可以使目标恢复执行，并且执行将恢复为最初位于该位置的指令。

### <a name="span-idavailability_of_processor_breakpoint_typesspanspan-idavailability_of_processor_breakpoint_typesspanavailability-of-processor-breakpoint-types"></a><span id="availability_of_processor_breakpoint_types"></span><span id="AVAILABILITY_OF_PROCESSOR_BREAKPOINT_TYPES"></span>处理器断点类型的可用性

只有在内核模式调试期间，才能使用在基于 x86 的处理器上运行 Windows XP 或更高版本的 Windows 的目标计算机， **i** (i/o) 选项可用。

并非所有数据大小都可用于所有处理器断点类型。 允许的大小取决于目标计算机的处理器。 有关详细信息，请参阅 [**ba (访问) 时中断 **](ba--break-on-access-.md)。

### <a name="span-idlimitations_of_software_breakpoints_and_processor_breakpointsspanspan-idlimitations_of_software_breakpoints_and_processor_breakpointsspanlimitations-of-software-breakpoints-and-processor-breakpoints"></a><span id="limitations_of_software_breakpoints_and_processor_breakpoints"></span><span id="LIMITATIONS_OF_SOFTWARE_BREAKPOINTS_AND_PROCESSOR_BREAKPOINTS"></span>软件断点和处理器断点的限制

使用 [**bp**](bp--bu--bm--set-breakpoint-.md) 或 bm.exe/a 命令时，可以指定数据地址而不是程序地址。 但是，即使指定了数据位置，这些命令也会创建软件断点，而不是处理器断点。 当调试器在某个位置放置软件断点时，它会使用中断指令暂时替换该内存位置的内容。 这不会损坏可执行的映像，因为调试器会记住此位置的原始内容，并且当目标进程尝试执行此代码时，调试器可以相应地做出响应。 但在数据位置设置软件断点时，生成的覆盖可能会导致数据损坏。 因此，仅当你确定仅将此位置用作可执行代码时，才可以安全地在数据位置设置软件断点。

**Bp**、 **bu**和**bm.exe**命令通过用 break 指令替换处理器指令来设置软件断点。 因此，它们不能用于只读代码或无法覆盖的任何其他代码。 若要在此类代码中设置断点，必须使用 " [**ba (在 Access) 上中断 **](ba--break-on-access-.md) ，并使用 **e** (execute) 选项。

不能在同一地址上创建多个处理器断点，该地址仅在触发断点时自动执行的命令中有所不同。 但是，你可以在不同于其他限制的同一地址创建多个断点 (例如，你可以通过使用带有 **/p**、 **/t**、 **/c**和 **/c**) 选项的不同值的**ba**命令，在同一地址创建多个断点。

用户模式进程中的初始断点 (通常在 **main** 函数或其等效) 上设置，而不能是处理器断点。

支持的处理器断点数取决于目标处理器的体系结构。

### <a name="span-idcontrolling_software_breakpoints_and_processor_breakpointsspanspan-idcontrolling_software_breakpoints_and_processor_breakpointsspancontrolling-software-breakpoints-and-processor-breakpoints"></a><span id="controlling_software_breakpoints_and_processor_breakpoints"></span><span id="CONTROLLING_SOFTWARE_BREAKPOINTS_AND_PROCESSOR_BREAKPOINTS"></span>控制软件断点和处理器断点

可以通过 [**最佳实践 (设置断点 **](bp--bu--bm--set-breakpoint-.md)来创建软件断点) 、 **Bm.exe (设置符号断点) **和 **Bu () 命令设置未解析的断点 ** 。 可以使用 [**ba (Access) **](ba--break-on-access-.md) 命令创建处理器断点。 禁用、启用和修改断点的命令适用于所有类型的断点。 显示断点列表的命令包括所有断点，并指示每个断点的类型。 有关这些命令的列表，请参阅 [控制断点的方法](methods-of-controlling-breakpoints.md)。

"WinDbg **断点** " 对话框显示所有断点，指出带有 "e"、"r"、"w"、"w"、"i" 和块大小的处理器断点。 此对话框可用于修改任何断点。 此对话框上的 " **命令** " 文本框可用于创建任何类型的断点。如果需要处理器断点，则使用 "ba" 开始输入。 有关详细信息，请参阅 [编辑 |断点](edit---breakpoints.md)。 当你在 "WinDbg [反汇编" 窗口](disassembly-window.md) 或 " [源](source-window.md)" 窗口中使用鼠标设置断点时，调试器将创建一个未解析的软件断点。

处理器断点存储在处理器的调试寄存器中。 可以通过手动编辑调试寄存器值来设置断点，但强烈建议不要这样做。

 

 





