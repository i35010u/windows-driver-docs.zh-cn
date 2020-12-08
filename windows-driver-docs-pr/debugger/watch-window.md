---
title: 使用监视窗口
description: 使用监视窗口
keywords:
- 调试信息窗口，监视窗口
- 监视窗口
- 内存，监视窗口
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 034842459f670687d3c084c0be828be771e14d1a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787705"
---
# <a name="using-the-watch-window"></a>使用监视窗口


## <span id="ddk_watch_window_dbg"></span><span id="DDK_WATCH_WINDOW_DBG"></span>


监视窗口显示有关全局变量、局部变量和寄存器的信息。 您可以自定义此窗口以显示您正在跟踪的项。

### <a name="span-idopening_the_watch_windowspanspan-idopening_the_watch_windowspanopening-the-watch-window"></a><span id="opening_the_watch_window"></span><span id="OPENING_THE_WATCH_WINDOW"></span>打开 "监视" 窗口

若要打开或切换到监视窗口，请在 "WinDbg" 窗口的 " **视图** " 菜单上，单击 " **监视**"。

还可以按 ALT + 2，或单击工具栏上的 "监视" **(ALT + 2)** 按钮： ![ "监视" 按钮的屏幕截图](images/tbwatch.png)

ALT + SHIFT + 2 将关闭监视窗口。

下面的屏幕截图显示了一个监视窗口的示例。

!["监视" 窗口的屏幕截图 ](images/window-watch.png)

监视窗口可以包含四列。 " **名称** " 和 " **值** " 列始终显示，" **类型** " 和 " **位置** " 列是可选的。 若要显示 " **类型** " 和 " **位置** " 列，请分别单击工具栏上的 " **转换** " 和 " **位置** " 按钮。

### <a name="span-idusing_the_watch_windowspanspan-idusing_the_watch_windowspanusing-the-watch-window"></a><span id="using_the_watch_window"></span><span id="USING_THE_WATCH_WINDOW"></span>使用 "监视" 窗口

在监视窗口中，你可以执行以下操作：

- 若要将变量添加到监视窗口，请选择 " **名称** " 列中的第一个空单元格，键入变量名称，然后按 enter。 用感叹号将模块名称与 (**！**) 的感叹号分隔开。 如果未指定模块，则使用当前模块。 若要在 " **名称** " 字段中输入一个地址，该地址必须以十进制数字开头 (如有必要，请使用前缀 **0x**) 。

  如果在当前函数的作用域中定义了您输入的变量名称，则它的值将出现在 " **值** " 列中。 如果未定义此值，则 " **值**" 列将显示 "错误：无法获取值"。

  即使未定义某个变量，将其添加到监视窗口也非常有用。 如果程序计数器输入一个函数，该函数定义了此名称的变量，则其值此时会出现在窗口中。

- 若要从监视窗口中删除变量，请双击其名称，再按 DELETE，然后按 ENTER。 还可以通过双击旧名称并键入新名称，然后按 ENTER 来替换旧名称和新名称。

- 如果变量是数据结构，则其名称旁边会出现一个复选框。 若要展开和折叠结构成员的显示，请选中或清除相应的复选框。

- **Int** 类型的整数显示为十进制值;**UINT** 类型的整数显示在当前基数中。 若要更改当前基数，请使用调试器命令窗口中的 [**n (Set Number Base)**](n--set-number-base-.md) 命令。

- 若要更改本地变量的值，请双击其 **值** 单元。 输入新值，或编辑旧值。  ("剪切"、"复制" 和 "粘贴" 命令可用于编辑。 ) 输入的值可以包含任何 [c + + 表达式](c---numbers-and-operators.md)。 输入新值或编辑旧值后，可以按 ENTER 来存储新值，或按 ESC 将其丢弃。 如果提交的值无效，则按 ENTER 后，旧值将再次出现。

  **Int** 类型的整数显示为十进制值;**UINT** 类型的整数显示在当前基数中。 若要更改当前基数，请使用调试器命令窗口中的 [**n (Set Number Base)**](n--set-number-base-.md) 命令。

- 如果 "类型" 列显示在 "监视窗口") 显示每个变量的当前数据类型，则该 **类型** 列 (。 每个变量显示为其自身数据类型的正确格式。 数据结构的类型名称在 **类型** 列中。 其他变量类型在此列中显示 "输入新类型"。

  如果双击 "输入新类型"，则可以通过输入新数据类型来强制转换类型。 此强制转换仅在监视窗口中更改此变量的当前显示。它不会更改调试器或目标计算机上的任何内容。 此外，如果在 " **值** " 列中输入新值，则将根据符号的实际类型（而不是您在 " **类型** " 列中输入的任何新类型）来分析输入的文本。 如果关闭再重新打开监视窗口，则会丢失数据类型更改。

  您还可以在 " **类型** " 列中输入扩展命令。 调试器会将符号地址传递到此扩展，并将生成的输出显示在当前行下一系列可折叠行中。 例如，如果此行中的符号是线程环境块的有效地址，则可以在 "**类型**" 列中输入 **！ teb** ，在该符号的地址上运行 [**！ teb**](-teb.md)扩展。

- **Location** 列 (如果它显示在监视窗口中) 显示数据结构中每个成员的偏移量。

- 除了变量外，还可以监视监视窗口中的以下各项：
  - 寄存器. 向监视窗口添加注册时，请使用 at 符号 () 为其名称添加前缀 **@** 。 与变量不同，你不能通过监视窗口更改寄存器值。
  - 包含函数指针的 Vtables。 当监视窗口中出现 Vtable 时，可以浏览表中的函数条目。 如果 Vtable 包含在指向派生实现的基类中，则会显示 notation **\_ \_ vtcast**<em>类</em>，以指示由于派生类而添加的成员。 这些成员扩展为派生类类型。
  - 扩展函数的返回值，例如 \_ EFN \_ GetPoolData。

与 " [局部变量" 窗口](locals-window.md)不同，监视窗口不受对 [寄存器上下文](changing-contexts.md#register-context)的更改的影响。 在监视窗口中，只可以查看和修改在当前程序计数器的作用域中定义的那些变量。

如果打开新工作区，则会丢弃监视窗口内容，并将其替换为新工作区中的内容。

### <a name="span-idtoolbar_and_shortcut_menuspanspan-idtoolbar_and_shortcut_menuspantoolbar-and-shortcut-menu"></a><span id="toolbar_and_shortcut_menu"></span><span id="TOOLBAR_AND_SHORTCUT_MENU"></span>工具栏和快捷菜单

监视窗口包含一个工具栏，其中包含两个按钮 (**转换** 和 **位置**) 以及包含其他命令的快捷菜单。 若要访问菜单，请右键单击窗口的标题栏，或单击窗口右上角附近的图标： ![ 用于访问 "监视" 窗口工具栏快捷菜单的按钮图标的屏幕截图 ](images/window-watch-menu.png)

工具栏和菜单包含以下按钮和命令：

-    (工具栏和菜单) **转换** 打开和关闭 **类型** 列的显示。

-    (工具栏和菜单) **位置** 将打开和关闭 **Location** 列的显示。

-    (菜单仅) **显示16位值，因为 unicode** 在此窗口中显示 unicode 字符串。 此命令打开和关闭影响 " [局部变量" 窗口](locals-window.md)、"监视窗口" 和 "调试器" 命令输出的全局设置。 此命令等效于使用 [**. enable \_ Unicode (Enable unicode Display)**](-enable-unicode--enable-unicode-display-.md) 命令。

-    (菜单仅) **始终在默认基数中显示数字** 会导致整数在默认基数中显示，而不是始终以十进制格式显示。 此命令打开和关闭影响 "局部变量" 窗口、"监视窗口" 和 "调试器" 命令输出的全局设置。 此命令等效于使用 [**. force \_ 基数 \_ 输出 (对整数使用基数)**](-force-radix-output--use-radix-for-integers-.md) 命令。
    **注意**   " **始终在默认基数中显示数字** " 命令不会影响长整数。 长整数以十进制格式显示，除非 [**. 启用 \_ 长 \_ 整型状态 (启用长整数显示)**](-enable-long-status--enable-long-integer-display-.md) 使用命令。 **. 启用 \_ 长 \_ 状态** 命令会影响 "局部变量" 窗口、"监视窗口" 和 "调试器" 命令输出中的显示。 监视窗口的菜单中没有此命令的等效项。

     

-    (菜单 "仅) **所选值的" 打开内存 "窗口** 打开一个新的停靠内存窗口，该窗口显示从所选表达式的地址开始的内存。

-   仅 (菜单) **为所选内存值调用 dt** 会运行 [**Dt (显示类型)**](dt--display-type-.md) 命令，并将所选符号作为其参数。 结果将显示在 [调试器命令窗口](debugger-command-window.md)中。 自动使用 **-n** 选项来区分十六进制地址中的符号。 不使用其他选项。 请注意，使用此菜单选项生成的内容与从命令行运行 **dt** 命令时生成的内容相同，但格式略有不同。

-   仅 (菜单) **工具栏** 打开和关闭工具栏。

-   仅) **停靠** 或 **取消停靠 (菜单会导致** 窗口进入或离开停靠状态。

-   仅 (菜单) **移动到新的 dock** 会关闭监视窗口，并在新的停靠中打开它。

-   仅 (菜单) " **设置为" 窗口类型的 "选项卡停靠目标** " 对于监视窗口不可用。 此选项仅适用于 [源](source-window.md) 或 [内存](memory-window.md) 窗口。

-    ("仅) " **始终浮动** "菜单会导致窗口保持未停靠，即使将其拖动到停靠位置。

-   仅 (菜单) **移动** 时，会导致在删除 WinDbg 帧时窗口移动，即使该窗口未停靠也是如此。 有关停靠窗口、选项卡式窗口和浮动窗口的详细信息，请参阅 [定位窗口](positioning-the-windows.md)。

-   仅 (菜单) **帮助** 在 Windows 调试工具文档中打开此主题。

-   仅) 关闭 (菜单 **关闭** 此窗口。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关控制变量的详细信息以及其他与内存相关的命令的说明，请参阅 [读取和写入内存](reading-and-writing-memory.md)。 有关寄存器及其操作的详细信息，请参阅 [在 WinDbg 中查看和编辑寄存器](registers-window.md)。 有关停靠窗口、选项卡式窗口和浮动窗口的详细信息，请参阅 [定位窗口](positioning-the-windows.md)。 有关可用于控制调试信息窗口的所有方法的详细信息，请参阅 [使用调试信息窗口](using-debugging-information-windows.md)。

 

 





