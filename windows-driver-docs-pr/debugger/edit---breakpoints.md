---
title: 编辑断点
description: 编辑断点
keywords:
- 编辑断点
- 断点，编辑断点
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcc4f6c1a438d9ce811aef117a5aea0ff6837f51
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838645"
---
# <a name="edit--breakpoints"></a>编辑 | 断点


## <span id="ddk_edit_breakpoints_dbg"></span><span id="DDK_EDIT_BREAKPOINTS_DBG"></span>


在 "**编辑**" 菜单上单击 "**断点**" 可显示或控制断点。

此命令等效于按 ALT + F9。 如果 [源窗口](source-window.md) 或 " [反汇编" 窗口](disassembly-window.md) 未处于活动状态，还可以按 f9，或单击工具栏上的 "插入或删除断点") 按钮 (屏幕截图 **(f9)** 按钮 ![ ](images/tbbp.png) 。

但是，如果 "源" 窗口或 "反汇编" 窗口处于打开状态，则 **插入或删除断点 (F9)** 按钮，f9 键在当前行上设置一个断点。  (如果在当前行上已设置了一个断点，此按钮或键将删除该断点。 ) 

如果某个语句或调用跨多行，则 WinDbg 在该语句或调用的最后一行上设置断点。 应在语句前面或前面插入插入符号 (^) ，以设置整个语句的断点。 如果调试器无法在当前插入符号位置设置断点，则会在下一次允许的位置向下搜索，并在该处插入断点。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

单击 " **断点**" 时，将显示 " **断点** " 对话框。 此对话框将显示所有当前断点信息，并以下列各列显示：

-   断点号。 此数字是一个十进制数，可用于在以后的命令中引用该断点。

-   断点状态。 此状态可以为 **e** (启用) 或 **d** (禁用) 。

-   只有字母 **u**)  (未解析的断点。 如果无法解析断点，则会显示此字母 (也就是说，它与任何当前加载的模块地址) 都不匹配。 有关详细信息，请参阅 [)  (Bu 断点的未解析断点 ](unresolved-breakpoints---bu-breakpoints-.md)。

-   断点的虚拟地址。 如果启用了源行号加载，则显示内容将包括文件和行号信息，而不是地址偏移量。 如果未解析断点，则地址将显示在列表的末尾，而不是显示在此处。

-    (处理器断点仅) 类型和大小信息。 此信息可以是 **e** (执行) 、 **r** (读/写) 、 **w** (写入) 或 (输入/**输出) 。** 这些类型后跟块的大小（以字节为单位）。 有关详细信息，请参阅 [ (Ba 断点) 处理器断点 ](processor-breakpoints---ba-breakpoints-.md)。

-   在断点变为活动状态之前剩余的传递数，后跟用括号括起的初始数目。 程序计数器在不中断的情况下通过断点的次数小于此数字的值。 因此，此数字从不小于1。 另请注意，此数字只计算应用程序在此点执行的时间。 换句话说，单步执行此点不会计数。 达到完整计数后，可以通过清除并重置断点来重置计数。

-   关联的进程和线程。 如果为线程提供了 () 三个星号 \* \* \* ，则该断点不是特定于线程的断点。

-   与断点地址相对应的模块和函数，具有偏移量。 如果未解析断点，则断点地址显示在此处的括号中。 如果对有效地址设置了断点，但缺少符号信息，则此列将为空。

-   命中此断点时自动执行的命令字符串。 此命令字符串用引号引起来。 如果命中断点，则执行此命令字符串中的命令，直到应用程序执行恢复。 任何恢复程序执行 (如 **g** 或 **t**) 的命令都将停止命令列表的执行。

如果选择任何断点，则可以单击 " **删除**"、" **禁用**" 或 " **启用** " 按钮。 " **移除** " 按钮将永久移除断点。 " **禁用** " 按钮暂时停用该断点。 " **启用** " 按钮会重新启用已禁用的断点。

" **全部删除** " 按钮会永久删除所有断点。

还可以通过以下方式在 " **命令** " 框中输入命令：

-   如果输入了 [**最佳实践 (设置断点)**](bp--bu--bm--set-breakpoint-.md)、 **Bu (设置未解析的断点)**、 **Bm.exe (设置的符号断点)**、 [**ba (访问) 中断**](ba--break-on-access-.md)、 [**Bc (断点清除)**](bc--breakpoint-clear-.md)、 [**bd (断点禁用)**](bd--breakpoint-disable-.md)或 [**(断点启用)**](be--breakpoint-enable-.md) 命令，则 **命令** 框的工作方式就像在 [调试器命令窗口](debugger-command-window.md)中输入命令一样。 但是，该命令本身必须是小写字母。 此命令不能以线程说明符开头。 如果要使用线程说明符，请在 " **线程** " 框中输入它，不带初始波形符 (~) 。

-   如果输入任何其他文本，则该文本将被视为 bu 的参数字符串 [**() 命令设置未解析的断点**](bp--bu--bm--set-breakpoint-.md) 。 也就是说，调试器使用 **bu** 和空格作为条目的前缀，然后将其作为命令执行。

输入新断点时，还可以执行以下操作：

-   通过在 " **线程** " 框中输入线程说明符来创建线程特定的断点。 不要包含颚化符 (~ 通常作为线程说明符的前缀) 字符。

-   通过在 " **条件** " 框中输入条件来创建条件断点。 条件可以是任何 evaluable 表达式，并将根据当前表达式语法进行计算 (参阅) [计算表达式](evaluating-expressions.md) 。 有关这些类型的断点的详细信息，请参阅 [设置条件断点](setting-a-conditional-breakpoint.md)。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

若要详细了解如何使用断点、其他断点命令和控制断点的方法，以及如何从内核调试器设置用户空间中的断点，请参阅 [使用断点](using-breakpoints.md)。 有关条件断点的详细信息，请参阅 [设置条件断点](setting-a-conditional-breakpoint.md)。

 

 





