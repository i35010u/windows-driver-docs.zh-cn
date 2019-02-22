---
title: 编辑断点
description: 编辑断点
ms.assetid: ca55ee25-aef3-42b1-b628-0a0e849103eb
keywords:
- 编辑断点
- 编辑断点的断点
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97f5f14b9e3c202527160cd1534ee29011f131a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555556"
---
# <a name="edit--breakpoints"></a>编辑 |断点


## <span id="ddk_edit_breakpoints_dbg"></span><span id="DDK_EDIT_BREAKPOINTS_DBG"></span>


单击**断点**上**编辑**菜单来显示或控制断点。

此命令相当于按 ALT + F9。 如果[源窗口](source-window.md)或[反汇编窗口](disassembly-window.md)是未处于活动状态，还可以按 f9 或单击**插入或删除断点 (f9)** 按钮 (![屏幕截图插入或删除断点按钮的](images/tbbp.png)) 工具栏上。

但是，如果源窗口或反汇编窗口打开，请**插入或删除断点 (F9)** 按钮和 F9 键的当前行上设置断点。 （如果已经在当前行设置断点，此按钮或键将删除断点。）

如果语句或调用跨多个行，WinDbg 在语句或调用的最后一行上设置断点。 应插入脱字号 (^)，或要为整个语句设置断点的语句之前。 如果调试器无法在当前插入符号位置设置断点，它将在下一步允许位置的向下方向中搜索和插入断点存在。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

当您单击**断点**，则**断点**对话框随即出现。 此对话框中显示所有当前断点信息，并且显示在以下列中：

-   断点数。 此数字是可用于后续命令中的断点是指一个十进制数。

-   断点的状态。 此状态可以是**e** （启用） 或**d** （禁用）。

-   （仅未解析的断点）以字母**u**。 如果断点是无法解析的会出现此字母 （即，它不匹配任何当前加载的模块地址）。 有关详细信息，请参阅[无法解析断点 (bu 断点)](unresolved-breakpoints---bu-breakpoints-.md)。

-   断点虚拟地址。 如果已启用的源行号的加载，显示内容包括文件和行号信息而不是地址的偏移量。 如果无法解析该断点，该地址会出现在末尾而不是此处的列表。

-   （仅适用于处理器断点）类型和大小的信息。 此信息可以是**e** （执行）， **r** （读/写）， **w** （写入） 或**我**（输入/输出）。 这些类型后面带有块，以字节为单位的大小。 有关详细信息，请参阅[处理器断点 (ba 断点)](processor-breakpoints---ba-breakpoints-.md)。

-   将该断点处于活动状态，直到剩余传递数后跟在括号中传递的初始数量。 程序计数器传递但不会中断的断点的次数是一个小于此数值的值。 因此，此数字是永远不会小于 1。 另请注意此数计数只能通过此点的应用程序执行的时间。 换而言之，不会计逐过程执行此点。 已达到最大计数后，您可以重置计数仅清除和重置断点。

-   关联的进程和线程。 如果线程提供有三个星号 (\*\*\*)，此断点不是特定于线程的断点。

-   模块和函数，使用的偏移量，对应于断点地址。 如果无法解析该断点，断点地址显示在这里，在括号中。 如果是有效的地址上设置断点，但缺少的符号信息，此列将为空。

-   命中此断点时自动执行的命令字符串。 此命令字符串显示在引号中。 如果到达断点时，此命令字符串中的命令执行，直到恢复应用程序执行的位置。 任一命令继续执行程序 (如**g**或**t**) 将停止执行命令列表。

如果选择任何断点，然后可以单击**删除**，**禁用**，或**启用**按钮。 **删除**按钮中永久删除的断点。 **禁用**按钮暂时停用断点。 **启用**按钮将重新启用已禁用的断点。

**全部删除**按钮会将永久删除所有断点。

您还可以输入中的命令**命令**框中的以下方法：

-   如果输入[**最佳实践 （设置断点）**](bp--bu--bm--set-breakpoint-.md)， **bu （设置无法解析断点）**， **bm （设置符号断点）**， [ **ba （中断的访问权限）**](ba--break-on-access-.md)， [ **bc （清除断点）**](bc--breakpoint-clear-.md)， [ **bd （禁用断点）**](bd--breakpoint-disable-.md)，或[**是 （启用断点）** ](be--breakpoint-enable-.md)命令**命令**框工作起来就好像你正在输入中的命令[调试器命令窗口](debugger-command-window.md)。 但是，命令本身必须以小写字母。 该命令不能以一个线程说明符开头。 如果你想要使用的线程说明符中, 输入**线程**不初始颚化符 （~）。

-   如果输入的任何其他文本，文本视为的参数字符串[ **bu （设置无法解析断点）** ](bp--bu--bm--set-breakpoint-.md)命令。 也就是说，调试器前缀与你的参赛**bu**和一个空格，然后执行它作为命令。

时输入的新断点，还可以执行以下操作：

-   通过输入中的线程说明符创建一个特定于线程的断点**线程**框。 不包括通常为前缀的线程说明符的波形符 （~） 字符。

-   输入中的条件创建条件断点**条件**框。 条件可以是任何 evaluable 表达式，并且它将评估根据当前的表达式语法 (请参阅[评估表达式](evaluating-expressions.md))。 有关这些类型的断点的详细信息，请参阅[设置条件断点](setting-a-conditional-breakpoint.md)。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关如何使用断点、 其他断点的命令和控制断点，并从内核调试程序的用户空间中设置断点的方法的详细信息，请参阅[使用断点](using-breakpoints.md)。 有关条件断点的详细信息，请参阅[设置条件断点](setting-a-conditional-breakpoint.md)。

 

 





