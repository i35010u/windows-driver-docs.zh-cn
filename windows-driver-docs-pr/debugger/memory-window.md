---
title: 在 WinDbg 中查看和编辑内存
description: 在 WinDbg 中，可以查看和编辑内存，通过输入命令或通过使用内存窗口。
ms.assetid: 4ac3b94c-5d92-4074-bf79-6da151ce52c8
keywords:
- 调试信息窗口中，内存窗口
- 内存窗口
- 内存中，内存窗口
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc1f6a57867190c3144b344508ac07d70ed35279
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351815"
---
# <a name="viewing-and-editing-memory-in-windbg"></a>在 WinDbg 中查看和编辑内存


在 WinDbg 中，可以查看和编辑内存，通过输入命令或通过使用内存窗口。

## <a name="span-iddebuggercommandwindowspanspan-iddebuggercommandwindowspanspan-iddebuggercommandwindowspandebugger-command-window"></a><span id="Debugger_Command_Window"></span><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>调试器命令窗口


您可以通过输入之一查看内存[**显示内存**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)调试器命令窗口中的命令。 可以通过输入之一来编辑内存[**输入值**](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md)调试器命令窗口中的命令。 有关详细信息，请参阅[访问虚拟地址的内存](accessing-memory-by-virtual-address.md)和[访问内存的物理地址](accessing-memory-by-physical-address.md)。

## <a name="span-idddkmemorywindowdbgspanspan-idddkmemorywindowdbgspanopening-a-memory-window"></a><span id="ddk_memory_window_dbg"></span><span id="DDK_MEMORY_WINDOW_DBG"></span>打开一个内存窗口


若要打开内存窗口，请选择**内存**从**视图**菜单。 (还可以按 ALT + 5，或单击**内存**按钮 (![内存按钮的屏幕截图](images/tbmem.png)) 工具栏上。 ALT + SHIFT + 5 关闭活动内存窗口。）

下面的屏幕截图显示了内存窗口的一个示例。

![内存窗口的屏幕截图](images/window-memory.png)

## <a name="span-idusingamemorywindowspanspan-idusingamemorywindowspanspan-idusingamemorywindowspanusing-a-memory-window"></a><span id="Using_a_Memory_Window"></span><span id="using_a_memory_window"></span><span id="USING_A_MEMORY_WINDOW"></span>使用内存窗口


内存窗口显示多个列中的数据。 在窗口的左侧列显示每个行的开始地址。 其余列显示所需的信息，从左到右。 如果选择**字节**中**显示格式**菜单中，对应于这两个字节的 ASCII 字符将显示在窗口的右侧。

**请注意**  默认情况下，内存窗口显示虚拟内存。 这种类型是内存的内存的在用户模式下可用的唯一类型。 在内核模式下，可以使用**内存选项**对话框以显示物理内存和其他数据空间。 **内存选项**对话框进行了介绍本主题中的更高版本。

 

在内存窗口中，可以执行以下操作：

-   若要写入内存，请单击内存窗口并键入新数据。 您可以编辑仅十六进制数据，不能直接编辑 ASCII 和 Unicode 字符。 只要键入新的信息，更改才会生效。

-   若要查看的其他部分的内存，请使用**上一步**并**下一步**按钮上的内存窗口工具栏上或按 PAGE UP 或 PAGE DOWN 键。 这些按钮和密钥显示内存立即前面或后面的部分。 如果请求了无效的页面，将显示一条错误消息。

-   若要导航窗口中，使用向右键、 向左键、 向上键和向下箭头键。 如果使用这些密钥来离开页面时，会显示一个新页面。 在使用这些密钥之前，应调整大小内存窗口，以便它不会包含滚动条。 此大小调整，可区分的实际页边缘和截止窗口。

-   若要更改正在查看的内存位置，内存窗口顶部的地址框中输入新的地址。 请注意内存窗口刷新其显示，而您输入一个地址，因此之前已完成键入地址，可获得错误消息。
    **请注意**  中当前基数解释在框中输入的地址。 如果当前的基数不是 16，您应前缀与十六进制地址**0x**。 若要更改默认基数，请使用[ **n (设置数量 Base)** ](n--set-number-base-.md)命令在调试器命令窗口中。 内存窗口本身中的显示不受当前的基数。

     

-   若要更改窗口用于显示内存的数据类型，请使用**显示格式**内存窗口工具栏中的菜单。 支持的数据类型包括短单词、 双字和四字;short、 long，与四整数和无符号的整数;10 字节、 16 个字节，32 位和 64 字节实数;ASCII 字符;Unicode 字符;和十六进制字节。 十六进制字节的显示内容包括 ASCII 字符和。

内存窗口具有一个包含两个按钮、 菜单和一个框，但与其他命令的快捷菜单的工具栏。 若要访问菜单，请右键单击标题栏或单击窗口 （在右上角附近的图标![显示内存窗口工具栏上的快捷菜单按钮的屏幕截图](images/tbmem.png))。 工具栏和快捷菜单包含以下几种选择：

-   （仅工具栏）地址框中，可指定新的地址或偏移量。 此框的确切含义取决于正在查看的内存类型。 例如，如果您正在查看虚拟内存，框中，可指定新的虚拟地址或偏移量。

-   （仅工具栏）**显示格式**使您能够选择新的显示格式。

-   （工具栏和菜单）**上一步**（在工具栏上） 和**上一步页**（在快捷菜单上） 会导致内存要显示的上一节。

-   （工具栏和菜单）**下一步**（在工具栏上） 和**下一页**（在快捷菜单上） 会导致内存要显示的下一节。

-   （仅限菜单）**工具栏**工具栏，开启和关闭。

-   （仅限菜单）**自动调整列**可确保在内存窗口中显示的列数适合内存窗口的宽度。

-   （仅限菜单）**停靠**或**取消停靠**将使窗口进入或离开停靠的状态。

-   （仅限菜单）**移到新停靠**内存窗口将关闭，并将其打开新的平台中。

-   （仅限菜单）**设置为选项卡形式停靠为窗口中，键入目标**作为其他内存窗口的选项卡形式停靠目标设置所选的内存窗口。 与选项卡式的集合中该窗口将自动进行分组之后作为选项卡形式停靠目标中选择一个打开的所有内存窗口。

-   （仅限菜单）**始终浮点**将使窗口停靠，即使仍拖到停靠位置。

-   （仅限菜单）**移动与帧**将使窗口移动时移动的 WinDbg 帧，即使在窗口已解除固定。 停靠和浮动的选项卡式，windows 的详细信息，请参阅[定位 Windows](positioning-the-windows.md)。

-   （仅限菜单）**属性**会打开**内存选项**对话框中，在本主题中的以下部分中所述。

-   （仅限菜单）**帮助**有关 Windows 调试工具文档中打开此主题。

-   （仅限菜单）**关闭**关闭此窗口。

### <a name="span-idmemoryoptionsdialogboxspanspan-idmemoryoptionsdialogboxspanmemory-options-dialog-box"></a><span id="memory_options_dialog_box"></span><span id="MEMORY_OPTIONS_DIALOG_BOX"></span>内存选项对话框

当您单击**属性**快捷菜单上**内存选项**对话框随即出现。

在内核模式下，有六种内存类型可用作此对话框中选项卡：**虚拟内存**，**物理内存**，**总线数据**，**控制数据**， **I/O** （I/O 端口信息） 和**MSR** （特定于模型的注册信息）。 单击对应于你想要访问的信息的选项卡。

在用户模式下，仅**虚拟内存**选项卡才可用。

每个选项卡，可指定想要显示的内存：

- 在中**虚拟内存**选项卡上，在**偏移量**框中，指定的地址或你想要查看内存范围的开头的偏移量。

- 在中**物理内存**选项卡上，在**偏移量**框中，指定你想要查看内存范围的起始处的物理地址。 内存窗口可以显示仅所述，可缓存的物理内存。 如果你想要显示的物理内存具有其他特性，请使用[ **d\* （显示内存）** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令或[ **！ d\\**  * ](-db---dc---dd---dp---dq---du---dw.md)扩展。

- 在中**总线数据**选项卡上，在**总线数据类型**菜单中，指定总线数据类型。 然后，使用**总线编号**，**槽号**，并**偏移量**框以指定你想要查看的总线数据。

- 在中**控制数据**选项卡上，使用**处理器**并**偏移量**文本框以指定你想要查看的控件数据。

- 在中**I/O**选项卡上，在**接口类型**菜单中，指定的 I/O 接口类型。 使用**总线编号**，**地址空间**，并**偏移量**框以指定你想要查看的数据。

- 在中**MSR**选项卡上，在**MSR**框中，指定你想要查看的模型特定寄存器。

每个选项卡还包括**显示格式**菜单。 此菜单包含与相同的效果**显示格式**内存窗口中的菜单。

单击**确定**中**内存选项**对话框中，若要使所做的更改才会生效。

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息


有关内存操作和其他与内存相关的命令的说明的详细信息，请参阅[读取和写入内存](reading-and-writing-memory.md)。

 

 





