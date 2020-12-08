---
title: 在 WinDbg 中输入调试器命令
description: 使用调试器在 WinDbg 中输入调试器命令命令窗口
keywords: 调试信息窗口，命令窗口，WinDbg
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 155778ef86e0e5671c37cd072c883930504c9063
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788805"
---
# <a name="entering-debugger-commands-in-windbg"></a>在 WinDbg 中输入调试器命令


## <span id="ddk_debugger_command_window_dbg"></span><span id="DDK_DEBUGGER_COMMAND_WINDOW_DBG"></span>


调试器命令窗口是 WinDbg 的主调试信息窗口。 您可以在此窗口中输入调试器命令并查看命令输出。

**注意**   此窗口在标题栏中显示 "命令"。 然而，本文档始终将此窗口称为 "调试器命令窗口"，以避免将其与用于发出 Microsoft MS-DOS 命令的命令提示符窗口混淆。

 

### <a name="span-idopening_the_debugger_command_windowspanspan-idopening_the_debugger_command_windowspanopening-the-debugger-command-window"></a><span id="opening_the_debugger_command_window"></span><span id="OPENING_THE_DEBUGGER_COMMAND_WINDOW"></span>打开调试器命令窗口

若要打开调试器命令窗口，请从 "**视图**" 菜单中选择 "**命令**"。  (您还可以按 ALT + 1，或在 **Command** ![ ](images/tbcmd.png) 工具栏上) 调试器命令窗口按钮 (屏幕截图中选择命令按钮。 ALT + SHIFT + 1 关闭调试器命令窗口。 ) 

下面的屏幕截图显示了一个命令窗口调试器的示例。

![调试器命令窗口示例的屏幕截图](images/window-command.png)

### <a name="span-idusing_the_debugger_command_windowspanspan-idusing_the_debugger_command_windowspanusing-the-debugger-command-window"></a><span id="using_the_debugger_command_window"></span><span id="USING_THE_DEBUGGER_COMMAND_WINDOW"></span>使用调试器命令窗口

调试器命令窗口拆分为两个窗格。 在窗口底部的 "命令条目" 窗格)  ("命令条目" 窗格中键入命令，然后在窗口顶部的较大窗格中查看输出。

在 "命令项" 窗格中，使用向上键和向下键滚动浏览命令历史记录。 显示命令时，你可以对其进行编辑或按 ENTER 运行该命令。

调试器命令窗口包含包含附加命令的快捷菜单。 若要访问此菜单，请选择并按住 (或右键单击窗口的标题栏) 或选择窗口右上角附近的图标 (![用于访问调试器命令窗口工具栏快捷菜单的按钮屏幕截图 ](images/tbcmd.png)). 以下列表描述了一些菜单命令：

-   "**添加到命令输出**" 向命令输出添加注释，类似于 "[编辑 |添加到命令输出](edit---add-to-command-output.md)命令。

-   **清除命令输出** 删除窗口中的所有文本。

-   **选择文本颜色和重新着色选择 ...** 打开一个对话框，您可以使用该对话框选择在调试器命令窗口中所选文本的显示文本颜色。

-   "**自动换行**" 打开和关闭 "自动换行" 状态。 此命令会影响整个窗口，而不仅是在选择此状态后使用的命令。 由于许多命令和扩展都生成格式化的显示，因此不建议使用自动换行。

-   **标记当前位置** 在命令窗口中的当前光标位置处设置标记。 标记的名称是光标右侧的行的内容。

-   "**跳到标记**" 会导致窗口滚动，使包含所选标记的行位于窗口顶部。

-   **始终浮动** 会导致窗口保持未停靠，即使将其拖动到停靠位置。

-   "**移动到帧**" 会导致在移动 WinDbg 帧时窗口移动，即使窗口未停靠也是如此。 有关停靠窗口、选项卡式窗口和浮动窗口的详细信息，请参阅 [定位窗口](positioning-the-windows.md)。

 

 





