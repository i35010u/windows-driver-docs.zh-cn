---
title: 在 WinDbg 中查看和编辑内存
description: 在 WinDbg 中，可以通过输入命令或使用 "内存" 窗口来查看和编辑内存。
ms.assetid: 4ac3b94c-5d92-4074-bf79-6da151ce52c8
keywords:
- 调试信息窗口，内存窗口
- “内存”窗口
- 内存，内存窗口
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f6f6cf4853d42caf94cf3190748e1993538dd19
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252878"
---
# <a name="viewing-and-editing-memory-in-windbg"></a>在 WinDbg 中查看和编辑内存


在 WinDbg 中，可以通过输入命令或使用 "内存" 窗口来查看和编辑内存。

## <a name="span-iddebugger_command_windowspanspan-iddebugger_command_windowspanspan-iddebugger_command_windowspandebugger-command-window"></a><span id="Debugger_Command_Window"></span><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>调试器命令窗口


可以通过在调试器命令窗口中输入其中一个 [**显示内存**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md) 命令来查看内存。 可以通过在调试器命令窗口中输入 " [**输入值**](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md) " 命令之一来编辑内存。 有关详细信息，请参阅 [按虚拟地址访问内存](accessing-memory-by-virtual-address.md) 和 [通过物理地址访问内存](accessing-memory-by-physical-address.md)。

## <a name="span-idddk_memory_window_dbgspanspan-idddk_memory_window_dbgspanopening-a-memory-window"></a><span id="ddk_memory_window_dbg"></span><span id="DDK_MEMORY_WINDOW_DBG"></span>打开 "内存" 窗口


若要打开 "内存" 窗口，请从 "**视图**" 菜单中选择 "**内存**"。  (还可以按 ALT + 5，或在**Memory** ![ ](images/tbmem.png) 工具栏上的 "内存" 按钮)  (屏幕截图中选择 "内存" 按钮。 ALT + SHIFT + 5 关闭 "活动内存" 窗口。 ) 

下面的屏幕截图显示了一个内存窗口示例。

!["内存" 窗口的屏幕截图](images/window-memory.png)

## <a name="span-idusing_a_memory_windowspanspan-idusing_a_memory_windowspanspan-idusing_a_memory_windowspanusing-a-memory-window"></a><span id="Using_a_Memory_Window"></span><span id="using_a_memory_window"></span><span id="USING_A_MEMORY_WINDOW"></span>使用内存窗口


"内存" 窗口显示多个列中的数据。 窗口左侧的列显示每行的起始地址。 其余列按从左到右的显示请求的信息。 如果在 "**显示格式**" 菜单中选择 "**字节**"，则与这些字节相对应的 ASCII 字符将显示在窗口的右侧。

**注意**   默认情况下，"内存" 窗口显示虚拟内存。 这种类型的内存是用户模式下唯一可用的内存类型。 在内核模式下，可以使用 " **内存选项** " 对话框显示物理内存和其他数据空间。 本主题后面将介绍 " **内存选项** " 对话框。

 

在 "内存" 窗口中，您可以执行以下操作：

-   若要写入内存，请在 "内存" 窗口中选择并键入 "新数据"。 仅可编辑十六进制数据，不能直接编辑 ASCII 和 Unicode 字符。 一旦键入新信息，更改就会生效。

-   若要查看内存的其他部分，请使用 "内存" 窗口工具栏上的 " **上一** 步" 和 " **下一步** " 按钮，或按 PAGE UP 或 page DOWN 键。 这些按钮和键显示紧前面或后面的内存部分。 如果请求的页无效，将显示一条错误消息。

-   若要在窗口内导航，请使用向右箭头、向左键、向上键和向下键。 如果你使用这些键来离开页面，则会显示一个新页。 使用这些密钥之前，应调整内存窗口的大小，使其不包含滚动条。 这种调整大小使您能够区分实际页面边缘和窗口截止时间。

-   若要更改正在查看的内存位置，请在 "内存" 窗口顶部的 "地址" 框中输入一个新地址。 请注意，当你输入地址时，"内存" 窗口将刷新其显示，因此在完成输入地址之前，你可能会收到错误消息。
    **注意**   您在框中输入的地址将在当前基数中解释。 如果当前基数不是16，则应使用 **0x**作为十六进制地址的前缀。 若要更改默认基数，请使用调试器命令窗口中的 [**n (Set Number Base) **](n--set-number-base-.md) 命令。 内存窗口本身中的显示不受当前基数的影响。

     

-   若要更改窗口用于显示内存的数据类型，请使用 "内存" 窗口工具栏中的 " **显示格式** " 菜单。 支持的数据类型包括短字、双字和四字;short、long 和四整数和无符号整数;10字节，16字节，32-字节和64字节实数;ASCII 字符;Unicode 字符;和十六进制字节。 十六进制字节的显示也包含 ASCII 字符。

"内存" 窗口包含一个工具栏，其中包含两个按钮：菜单和一个框，并且具有包含附加命令的快捷菜单。 若要访问菜单，请选择并按住 (或右键单击标题栏) ，或选择窗口右上角附近的图标 (![显示 "内存" 窗口工具栏快捷菜单的按钮屏幕截图](images/tbmem.png)). 工具栏和快捷菜单包含以下选项：

-    (工具栏仅) "地址" 框中，您可以指定新地址或偏移量。 此框的确切含义取决于您正在查看的内存类型。 例如，如果您正在查看虚拟内存，则使用该框可以指定新的虚拟地址或偏移量。

-    (工具栏仅) **显示格式** ，使您可以选择新的显示格式。

-    (工具栏和菜单) ) 工具栏上的 "上 **一** ("，而快捷菜单上的 " **上一页** () 导致显示前一部分内存。

-    (工具栏和菜单) ) 工具栏上的 " **下一步** " (，快捷菜单上的 " **下一页** (将导致显示下一部分内存。

-   仅 (菜单) **工具栏** 打开和关闭工具栏。

-   仅) **自动调整列** (菜单可确保在 "内存" 窗口中显示的列数适应 "内存" 窗口的宽度。

-   仅) **停靠** 或 **取消停靠 (菜单会导致** 窗口进入或离开停靠状态。

-   仅 (菜单) **移动到新的停靠** 将关闭内存窗口，并在新的停靠中打开它。

-   仅 (菜单) **"设置为" 窗口类型的选项卡停靠目标** "将所选内存窗口设置为其他内存窗口的选项卡停靠目标。 在选择了一个选项卡停靠目标后打开的所有内存窗口都将在选项卡式集合中自动与该窗口进行分组。

-    ("仅) " **始终浮动** "菜单会导致窗口保持未停靠，即使将其拖动到停靠位置。

-   仅 (菜单) **移动** 时，会导致在删除 WinDbg 帧时窗口移动，即使该窗口未停靠也是如此。 有关停靠窗口、选项卡式窗口和浮动窗口的详细信息，请参阅 [定位窗口](positioning-the-windows.md)。

-    (菜单 "仅) **属性** " 打开 " **内存选项** " 对话框，本主题中的以下部分对此进行了说明。

-   仅 (菜单) **帮助** 在 Windows 调试工具文档中打开此主题。

-   仅) 关闭 (菜单 **关闭** 此窗口。

### <a name="span-idmemory_options_dialog_boxspanspan-idmemory_options_dialog_boxspanmemory-options-dialog-box"></a><span id="memory_options_dialog_box"></span><span id="MEMORY_OPTIONS_DIALOG_BOX"></span>"内存选项" 对话框

在快捷菜单上选择 " **属性** " 时，将显示 " **内存选项** " 对话框。

在内核模式下，此对话框中有六种内存类型可用作选项卡： **虚拟内存**、 **物理内存**、 **总线数据**、 **控制数据**、 **i/o** (i/o 端口信息) 以及 **MSR** (特定于模型的寄存器信息) 。 选择与要访问的信息对应的选项卡。

在用户模式下，只有 " **虚拟内存** " 选项卡可用。

每个选项卡都允许您指定要显示的内存：

- 在 " **虚拟内存** " 选项卡上的 " **偏移量** " 框中，指定要查看的内存范围的起始地址或偏移量。

- 在 " **物理内存** " 选项卡的 " **偏移量** " 框中，指定要查看的内存范围开头的物理地址。 "内存" 窗口只能显示所述的可缓存物理内存。 如果要显示具有其他属性的物理内存，请使用[**d \* (显示内存) **](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令或[ **！ d \\ ** * ](-db---dc---dd---dp---dq---du---dw.md)扩展。

- 在 " **总线数据** " 选项卡上的 " **总线数据类型** " 菜单中，指定总线数据类型。 然后，使用 " **总线号**"、" **槽编号**" 和 " **偏移量** " 框指定要查看的总线数据。

- 在 " **控件数据** " 选项卡中，使用 " **处理器** " 和 " **偏移量** " 文本框指定要查看的控件数据。

- 在 " **i/o** " 选项卡上的 " **接口类型** " 菜单中，指定 i/o 接口类型。 使用 " **总线号**"、" **地址空间**" 和 " **偏移量** " 框指定要查看的数据。

- 在 " **msr** " 选项卡的 " **msr** " 框中，指定要查看的特定于模型的寄存器。

每个选项卡还包括 " **显示格式** " 菜单。 此菜单具有与 "内存" 窗口中 " **显示格式** " 菜单相同的效果。

选择 "**内存选项**" 对话框中的 **"确定"** 以使更改生效。

## <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息


有关内存操作的详细信息以及其他与内存相关的命令的说明，请参阅 [读取和写入内存](reading-and-writing-memory.md)。

 

 





