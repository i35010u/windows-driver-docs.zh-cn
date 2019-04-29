---
title: 处理器断点 (ba 断点)
description: 处理器断点 (ba 断点)
ms.assetid: 2681cebd-dce2-48f1-8953-9af65d15f378
keywords:
- 断点，处理器断点
- 数据断点的断点
- 软件断点的断点
- 断点，最佳实践与 BA
- 软件断点
- 软件断点概述
- 软件断点限制
- 处理器断点
- 处理器断点概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76fd595e3a33456cb5e0b9d666eca87bc24622ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385690"
---
# <a name="processor-breakpoints-ba-breakpoints"></a>处理器断点 (ba 断点)


控制在调试器的请求时处理器的断点被称为*处理器断点*或*数据断点*。 直接受调试器的断点被称为*软件断点*。

**请注意**  尽管术语*数据断点*通常用作同义词*处理器断点*，此术语可能会产生误导。 有两种基本类型的断点： 受控制的处理器，处理器断点以及软件断点，调试器控制。 处理器断点通常设置程序的数据--这是它们被称为"数据断点"-原因，但是他们还可以设置可执行的代码。 可执行的代码，通常设置软件断点，但他们还可以设置计划的数据。 遗憾的是，它是常见的调试宣传资料来指代处理器断点作为"数据断点"，即使它们设置可执行的代码。

 

### <a name="span-idprocessorbreakpointsspanspan-idprocessorbreakpointsspanprocessor-breakpoints"></a><span id="processor_breakpoints"></span><span id="PROCESSOR_BREAKPOINTS"></span>处理器断点

访问特定的内存位置时，会触发处理器断点。 有四种类型的处理器断点，对应的触发它的内存访问类型：

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
<td align="left"><p><strong>e</strong> （执行）</p></td>
<td align="left"><p>当处理器检索一条指令从指定的地址时触发。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r</strong> （读/写）</p></td>
<td align="left"><p>当处理器读取或写入指定地址处的内存时触发。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>w</strong> （写入）</p></td>
<td align="left"><p>处理器将写入指定地址处的内存时触发。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>i</strong> (i/o)</p></td>
<td align="left"><p>触发时指定的 I/O 端口<em>地址</em>访问。</p></td>
</tr>
</tbody>
</table>

 

每个处理器断点具有与之关联的大小。 例如， **w** （写入） 无法在大小为 4 个字节的地址 0x70001008 设置处理器断点。 这将监视从 0x70001008 到 0x7000100B，非独占地址块。 如果此内存块写入后，将触发断点。

它可能会发生处理器执行的操作与重叠的但不是等同于指定区域的内存区域。 在上一段中给出的示例，包括范围 0x70001000 到 0x7000100F 一次写入操作或写入操作，包括仅在 0x70001009，字节将是重叠的操作。 在这种情况下，触发断点是否与处理器相关。 有关这种情况下特定处理器上的处理方式的详细信息，请参阅处理器结构手册并查找"调试注册"或"调试控件注册"。 若要以一种特定的处理器类型为例，x86 处理器、 读取或写入触发断点时的访问的范围重叠的断点范围。

同样，如果**e** （执行） 上的地址 0x00401003，设置断点和执行这些地址 0x00401002 和 0x00401003 双字节指令跨越，则结果是处理器相关。 同样，有关详细信息需要查阅处理器体系结构手册。

处理器区分用户模式下调试程序设置的断点和内核模式调试程序设置的断点。 用户模式下处理器断点不会影响任何内核模式的进程。 内核模式下处理器断点可能会或可能不会影响用户模式进程，具体取决于用户模式代码使用调试注册状态以及是否有用户模式下调试程序附加。

若要应用到不同的寄存器上下文当前进程的现有数据断点，使用[ **.apply\_dbp （到上下文应用数据断点）** ](-apply-dbp--apply-data-breakpoint-to-context-.md)命令。

在多处理器计算机中，每个处理器断点适用于所有处理器。 例如，如果当前处理器 3，并使用命令`ba e1 MyAddress`要将在断点放**MyAddress**，在该地址执行的任何处理器-不只是处理器 3--触发断点。 这适用于软件的断点。

### <a name="span-idsoftwarebreakpointsspanspan-idsoftwarebreakpointsspansoftware-breakpoints"></a><span id="software_breakpoints"></span><span id="SOFTWARE_BREAKPOINTS"></span>软件断点

软件断点，处理器与断点不同，由调试器控制。 调试器将软件断点设置在某个位置，它暂时将该内存位置的内容替换中断指令。 调试器会记住此位置的原始内容，因此，如果在调试器中显示此内存，则调试器会显示该内存位置，而不中断指令的原始内容。 当目标进程执行的代码在此位置时，中断指令会导致进程进入调试器。 执行选择的操作之后，可能会导致目标以继续执行，并执行将继续使用最初在该位置中的说明。

### <a name="span-idavailabilityofprocessorbreakpointtypesspanspan-idavailabilityofprocessorbreakpointtypesspanavailability-of-processor-breakpoint-types"></a><span id="availability_of_processor_breakpoint_types"></span><span id="AVAILABILITY_OF_PROCESSOR_BREAKPOINT_TYPES"></span>处理器断点类型的可用性

在 Windows Server 2003 Service Pack 1 (SP1)，使用 WOW64 来模拟 x86 的基于 Itanium 的计算机上，处理器断点不适用于**e** （执行） 选项，但它们并适用于**r** (读/写） 和**w** （写入） 选项。

**我**仅在内核模式调试中，与目标计算机在基于 x86 的处理器上运行 Windows XP 或更高版本的 Windows 过程 (i/o) 选项才可用。

并非所有数据大小可以都用于所有处理器断点类型。 允许的大小取决于目标计算机的处理器。 有关详细信息，请参阅[ **ba （中断的访问权限）**](ba--break-on-access-.md)。

### <a name="span-idlimitationsofsoftwarebreakpointsandprocessorbreakpointsspanspan-idlimitationsofsoftwarebreakpointsandprocessorbreakpointsspanlimitations-of-software-breakpoints-and-processor-breakpoints"></a><span id="limitations_of_software_breakpoints_and_processor_breakpoints"></span><span id="LIMITATIONS_OF_SOFTWARE_BREAKPOINTS_AND_PROCESSOR_BREAKPOINTS"></span>软件断点和处理器断点的限制

可以使用时指定数据地址而不是程序地址[ **bp** ](bp--bu--bm--set-breakpoint-.md)或 bm/a 命令。 但是，即使指定的数据位置，这些命令将创建软件断点、 不处理器断点。 调试器会软件断点放在某个位置，它暂时将该内存位置的内容替换中断指令。 这不会损坏可执行映像，因为调试器会记住此位置的原始内容并在目标进程尝试执行此代码在调试器做出正确响应。 但是，当软件断点设置在数据的位置时，生成覆盖可能会导致数据损坏。 因此，数据位置上设置软件断点是仅当您确信此位置将仅用作可执行代码安全的。

**Bp**， **bu**，并**bm**命令由处理器指令替换为中断指令设置软件断点。 因此这些不能在只读的代码或任何其他不能被覆盖的代码中使用。 若要在此类代码中设置断点，必须使用[ **ba （中断的访问权限）** ](ba--break-on-access-.md)与**e** （执行） 选项。

不能在相同的区别只在于触发断点时自动执行该命令的位置来创建多个处理器断点。 但是，可以创建多个断点在相同的区别在于它们的其他限制的地址 (例如，您可以创建多个断点在相同的地址使用**ba** 的不同值的命令 **/p**， **/t**， **/c**，以及 **/C**选项)。

用户模式进程中的初始断点 (通常情况下设置上**主要**函数或其等效项) 不能为处理器断点。

支持的处理器断点数取决于目标处理器体系结构。

### <a name="span-idcontrollingsoftwarebreakpointsandprocessorbreakpointsspanspan-idcontrollingsoftwarebreakpointsandprocessorbreakpointsspancontrolling-software-breakpoints-and-processor-breakpoints"></a><span id="controlling_software_breakpoints_and_processor_breakpoints"></span><span id="CONTROLLING_SOFTWARE_BREAKPOINTS_AND_PROCESSOR_BREAKPOINTS"></span>控制软件断点和处理器断点

可用于创建软件断点[**最佳实践 （设置断点）**](bp--bu--bm--set-breakpoint-.md)， **bm （设置符号断点）**，和**bu （设置无法解析断点）** 命令。 可以使用创建处理器断点[ **ba （中断的访问权限）** ](ba--break-on-access-.md)命令。 禁用、 启用，并且修改断点的命令应用于所有种类的断点。 显示断点的列表的命令包括所有断点，并指示每个类型。 有关这些命令的列表，请参阅[控制断点方法](methods-of-controlling-breakpoints.md)。

WinDbg**断点**对话框的显示所有断点，指示处理器断点，带有表示法"e"、"r"、"w"或"我跟块的大小。 此对话框可以用于修改任何断点。 **命令**文本框中，在此对话框可用于创建任何类型的断点。如果需要处理器断点，开始使用"ba"的输入。 有关详细信息，请参阅[编辑 |断点](edit---breakpoints.md)。 当通过使用鼠标在 WinDbg 中设置断点[反汇编窗口](disassembly-window.md)或[源窗口](source-window.md)，调试器创建未解决的软件断点。

处理器断点存储在寄存器中处理器的调试。 若要设置通过手动编辑调试断点注册值，但这是强烈建议不要使用它。

 

 





