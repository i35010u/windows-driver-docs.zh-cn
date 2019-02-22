---
title: 使用监视窗口
description: 使用监视窗口
ms.assetid: 233adbcd-c712-4cbb-abe6-5d4e18fa6c27
keywords:
- 调试信息窗口，监视窗口
- 观察时段
- 内存中，监视窗口
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8dde55d8f5a09c94b01f8076f0975ac81634fc2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554044"
---
# <a name="using-the-watch-window"></a>使用监视窗口


## <span id="ddk_watch_window_dbg"></span><span id="DDK_WATCH_WINDOW_DBG"></span>


监视窗口显示有关全局变量、 本地变量和寄存器信息。 您可以自定义此窗口以显示您正在跟踪的项。

### <a name="span-idopeningthewatchwindowspanspan-idopeningthewatchwindowspanopening-the-watch-window"></a><span id="opening_the_watch_window"></span><span id="OPENING_THE_WATCH_WINDOW"></span>打开监视窗口

若要打开或切换到监视窗口在 WinDbg 窗口中，在**视图**菜单上，单击**监视**。

此外可以按 ALT + 2，或单击**Watch (ALT + 2)** 工具栏上的按钮：![监视按钮的屏幕截图](images/tbwatch.png)

ALT + SHIFT + 2 将关闭监视窗口。

下面的屏幕截图显示了监视窗口的示例。

![监视窗口的屏幕截图 ](images/window-watch.png)

监视窗口可以包含四个列。 **名称**并**值**始终显示列，并**类型**并**位置**列是可选的。 若要显示**类型**并**位置**列，单击**Typecast**并**位置**按钮，分别在工具栏上。

### <a name="span-idusingthewatchwindowspanspan-idusingthewatchwindowspanusing-the-watch-window"></a><span id="using_the_watch_window"></span><span id="USING_THE_WATCH_WINDOW"></span>使用监视窗口

在监视窗口中，可以执行以下操作：

- 若要将变量添加到监视窗口中，选择第一个空单元格**名称**列中，键入变量名称，然后按 ENTER。 一个带有感叹号变量从单独的模块名称 (**！**)。 如果未指定模块，则使用当前的模块。 若要输入中的地址**名称**字段中，该地址必须以具有十进制数字 (如有必要，使用该前缀**0x**)。

  如果您输入的变量名称当前函数的作用域中定义的其值将出现在**值**列。 如果未定义，**值**列将显示"错误：无法获取值"。

  即使未定义变量，它可将其添加到监视窗口。 如果程序计数器输入在其中定义此名称的变量的函数，其值将出现在窗口中在该时间。

- 要从监视窗口中删除变量，请双击其名称，按 DELETE 键，然后按 ENTER。 通过双击旧名称，键入新名称，然后按 ENTER，也可以使用新名称替换旧名称。

- 如果变量是一种数据结构，其名称旁边显示复选框。 若要展开和折叠结构成员的显示，请选择或清除该复选框。

- 类型的整数**int**显示为十进制值; 类型的整数**UINT**显示在当前的基数。 若要更改当前的基数，请使用[ **n (设置数量 Base)** ](n--set-number-base-.md)命令在调试器命令窗口中。

- 若要更改本地变量的值，请双击其**值**单元格。 输入新值，或编辑旧值。 （剪切、 复制和粘贴命令是可用来进行编辑。）您输入的值可以包含任何[c + + 表达式](c---numbers-and-operators.md)。 输入新值或编辑旧值后，您可以按 enter 键来存储新值或按 esc 键放弃它。 如果提交无效的值后按 ENTER,，将重新出现的旧值。

  类型的整数**int**显示为十进制值; 类型的整数**UINT**显示在当前的基数。 若要更改当前的基数，请使用[ **n (设置数量 Base)** ](n--set-number-base-.md)命令在调试器命令窗口中。

- **类型**列 （如果它显示在监视窗口中） 显示每个变量的当前数据类型。 每个变量显示在其自己的数据类型为正确的格式。 数据结构具有其类型名**类型**列。 其他变量的类型显示在此列中的"输入新的类型"。

  如果您双击"输入新类型"，您可以通过输入新的数据类型强制转换类型。 此强制转换更改仅在监视窗口中; 此变量的当前显示它不会更改任何内容在调试器中或在目标计算机上。 此外，如果输入中的新值**值**列中，你输入的文本将分析基于符号的实际类型而不是任何新型中输入**类型**列。 如果关闭并重新打开监视窗口，您将丢失的数据类型更改。

  您还可以输入中的扩展命令**类型**列。 调试器会将该符号的地址传递到此扩展插件，并将在一系列的当前行下方的可折叠行中显示生成的输出。 例如，如果在此行中的符号是有效的线程环境块的地址，则可以输入 **！ teb**中**类型**列来运行[ **！ teb** ](-teb.md)此符号的地址上的扩展。

- **位置**列 （如果它显示在监视窗口中） 显示了一种数据结构的每个成员的偏移量。

- 除了变量之外，还可以监视监视窗口中的以下项：
  - 注册。 当将寄存器添加到监视窗口中时，其名称加上前缀 at 符号 (**@**)。 与变量不同，不能更改寄存器值通过监视窗口。
  - 包含函数的指针的 Vtable。 当 Vtable 出现在监视窗口中时，您可以浏览表中的函数条目。 如果在指向派生的实现，表示法的基类中包含 Vtable  **\_vtcast\_**<em>类</em>显示来指示要添加的成员由于派生类中。 这些成员展开类似于派生的类类型。
  - 扩展插件的返回值函数，如\_EFN\_GetPoolData。

与不同[局部变量窗口](locals-window.md)，监视窗口未更改的影响[注册上下文](changing-contexts.md#register-context)。 在监视窗口中可以查看和修改当前的程序计数器的作用域中定义的变量。

如果您打开新的工作区，监视窗口内容是丢弃并替换为新的工作区中。

### <a name="span-idtoolbarandshortcutmenuspanspan-idtoolbarandshortcutmenuspantoolbar-and-shortcut-menu"></a><span id="toolbar_and_shortcut_menu"></span><span id="TOOLBAR_AND_SHORTCUT_MENU"></span>工具栏和快捷方式菜单

监视窗口有一个包含两个按钮的工具栏 (**Typecast**并**位置**) 以及一个具有其他命令的快捷菜单。 若要访问菜单，请右键单击该窗口的标题栏或单击窗口右上角附近的图标：![用于访问监视窗口工具栏上的快捷菜单的按钮图标的屏幕截图 ](images/window-watch-menu.png)

工具栏和菜单包含以下按钮和命令：

-   （工具栏和菜单）**Typecast**将显示**类型**列打开和关闭。

-   （工具栏和菜单）**位置**将显示**位置**列打开和关闭。

-   （仅限菜单）**显示 16 位值作为 Unicode**此窗口中显示的 Unicode 字符串。 此命令，开启和关闭全局设置，它会影响[局部变量窗口](locals-window.md)、 监视窗口和调试器命令输出。 此命令相当于使用[ **.enable\_unicode （启用 Unicode 显示器）** ](-enable-unicode--enable-unicode-display-.md)命令。

-   （仅限菜单）**始终显示在默认数字基数**导致要显示的默认基数中而不是始终显示它们以十进制格式的整数。 此命令将打开和关闭全局设置，它会影响局部变量窗口、 监视窗口和调试器命令输出。 此命令相当于使用[ **.force\_基数\_输出 （使用基数范围内的整数）** ](-force-radix-output--use-radix-for-integers-.md)命令。
    **请注意**   **始终显示在默认数字基数**命令不会影响长整数。 除非以十进制格式显示长整数[ **.enable\_长\_状态 （启用长整数的显示）** ](-enable-long-status--enable-long-integer-display-.md)使用命令。 **.Enable\_长\_状态**命令会影响在局部变量窗口中，监视窗口和调试器命令输出的显示。 为此命令的菜单中监视窗口中没有等效项。

     

-   （仅限菜单）**选定的值为打开内存窗口**将打开新的停靠的内存窗口，显示所选表达式的地址处开始的内存。

-   （仅限菜单）**调用所选的内存值的 dt**运行[ **dt （显示类型）** ](dt--display-type-.md)命令与所选符号作为其参数。 结果出现在[调试器命令窗口](debugger-command-window.md)。 **-N**选项自动用于将符号与十六进制地址区分开来。 未不使用任何其他选项。 请注意，使用此菜单选项生成的内容是与运行时生成的内容相同**dt**命令从命令行中，但格式会略有不同。

-   （仅限菜单）**工具栏**工具栏，开启和关闭。

-   （仅限菜单）**停靠**或**取消停靠**将使窗口进入或离开停靠的状态。

-   （仅限菜单）**移到新停靠**监视窗口将关闭，并将其打开新的平台中。

-   （仅限菜单）**设置为选项卡形式停靠为窗口中，键入目标**不可用于监视窗口。 此选项才可供[源](source-window.md)或[内存](memory-window.md)windows。

-   （仅限菜单）**始终浮点**将使窗口停靠，即使仍拖到停靠位置。

-   （仅限菜单）**移动与帧**将使窗口移动时移动的 WinDbg 帧，即使在窗口已解除固定。 停靠和浮动的选项卡式，windows 的详细信息，请参阅[定位 Windows](positioning-the-windows.md)。

-   （仅限菜单）**帮助**有关 Windows 调试工具文档中打开此主题。

-   （仅限菜单）**关闭**关闭此窗口。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关控制变量和其他与内存相关的命令的说明的详细信息，请参阅[读取和写入内存](reading-and-writing-memory.md)。 有关寄存器和其操作的详细信息，请参阅[查看和编辑注册在 WinDbg 中](registers-window.md)。 停靠和浮动的选项卡式，windows 的详细信息，请参阅[定位 Windows](positioning-the-windows.md)。 有关可以使用来控制调试信息 windows 的所有技术的详细信息，请参阅[使用调试信息 Windows](using-debugging-information-windows.md)。

 

 





