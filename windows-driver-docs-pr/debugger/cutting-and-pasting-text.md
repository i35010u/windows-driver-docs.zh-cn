---
title: 剪切和粘贴文本
description: 剪切和粘贴文本
ms.assetid: efc62bee-ba35-4bff-b88b-3b287ededc38
keywords:
- 剪切文本
- 粘贴文本
- 复制文本
- 调试信息窗口，剪切和粘贴文本
- 文本
- 文本，编辑
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bff0bfa7a3e076a9cb311bb8f91b8b0a404324b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523588"
---
# <a name="cutting-and-pasting-text"></a>剪切和粘贴文本


## <span id="ddk_cutting_and_pasting_text_dbg"></span><span id="DDK_CUTTING_AND_PASTING_TEXT_DBG"></span>


WinDbg 使用许多常见的处理文本和几种方法不太常见的方法。

### <a name="span-idselectingtextspanspan-idselectingtextspanselecting-text"></a><span id="selecting_text"></span><span id="SELECTING_TEXT"></span>选择文本

若要选择中的文本[源窗口](source-window.md)，请在[反汇编窗口](disassembly-window.md)中的任一窗格[调试器命令窗口](debugger-command-window.md)，或在对话框中，依次指向一个末尾的文本，按和按住鼠标左键，并将指针拖到另一端的文本。

若要在窗口中选择的所有文本，还可以单击[全](edit---select-all.md)上**编辑**菜单或按 CTRL + A。

中[调用窗口](calls-window.md)，监视窗口[局部变量窗口](locals-window.md)，[寄存器窗口](registers-window.md)，以及[内存窗口](memory-window.md)，不能选择任意范围文本，但您可以选择整行或单元格。 单击所需的行或单元格以选择其文本。

在输入文本，按分别删除文本到右侧或左侧的游标，删除和 BACKSPACE 键。 如果选择文本，可以按这些键以删除所选内容。 如果你选择文本，然后键入的任何字符，则将为新字符所选择的内容。

### <a name="span-idcopyingtextspanspan-idcopyingtextspancopying-text"></a><span id="copying_text"></span><span id="COPYING_TEXT"></span>复制文本

若要复制文本，请选择该文本，然后执行以下项之一：

-   按鼠标右键。 （此方法适用仅在某些位置中。 有关如何使用鼠标右键按钮的详细信息，请参阅右侧鼠标按钮。）

-   按 CTRL + C。

-   按 CTRL + INSERT。

-   (仅限停靠和选项卡式 windows)单击**副本**上**编辑**菜单。

-   单击**复制 (Ctrl + C)** 按钮 (![复制按钮的屏幕截图](images/tbcopy.png)) 工具栏上。

### <a name="span-idcuttingtextspanspan-idcuttingtextspancutting-text"></a><span id="cutting_text"></span><span id="CUTTING_TEXT"></span>剪切文本

若要剪切文本并将其移动到剪贴板中，选择的文本，然后执行以下项之一：

-   按 CTRL + X。

-   按 SHIFT + DELETE。

-   (仅限停靠和选项卡式 windows)单击**剪切**上**编辑**菜单。

-   单击**剪切 (Ctrl + X)** 按钮 (![剪切按钮的屏幕截图](images/tbcut.png)) 工具栏上。

可以剪切文本从底部窗格的调试器命令窗口、 监视窗口的左侧列和任意对话框中 （即，从任何位置的支持文本输入）。

### <a name="span-idpastingtextspanspan-idpastingtextspanpasting-text"></a><span id="pasting_text"></span><span id="PASTING_TEXT"></span>粘贴文本

若要粘贴剪贴板中的文本，将你想要插入的文本 （或选择你想要替换的文本） 的游标，然后执行下列任一操作：

-   按鼠标右键。 （此方法适用于仅在某些位置，并不能使用此方法用于替换文本。 有关如何使用此方法的更多信息，请参阅右侧鼠标按钮。）

-   按 CTRL + V。

-   按 SHIFT + INSERT。

-   (仅限停靠和选项卡式 windows)单击**粘贴**上**编辑**菜单。

-   单击**粘贴 (Ctrl + V)** 按钮 (![粘贴按钮的屏幕截图](images/tbpaste.png)) tooblar 上。

可以将文本粘贴到调试器的命令窗口的底部窗格中，到监视窗口的左侧列和任意对话框中 （即，到任何位置的支持文本输入）。

### <a name="span-idrightmousebuttonspanspan-idrightmousebuttonspanright-mouse-button"></a><span id="right_mouse_button"></span><span id="RIGHT_MOUSE_BUTTON"></span>鼠标右按钮

鼠标右键按钮具有多种效果，可以进行复制和粘贴操作速度更快：

-   如果调试器命令窗口的任一窗格中、 在便笺、 在反汇编窗口中，或在任何源窗口中，选择文本，然后按下鼠标右键按钮，则将文本复制到剪贴板。 但是，如果**QuickEdit 模式**已取消选择中[视图 |选项](view---options.md)，两个位置中右键单击将弹出菜单与当前的位置最相关。

-   如果调试器命令窗口的任一窗格中，暂存器或文本条目空间的监视窗口中，将光标置于 （而不选择任何文本），然后按鼠标右键的剪贴板内容粘贴到窗口。 但是，如果**QuickEdit 模式**已取消选择中[视图 |选项](view---options.md)，两个位置中右键单击将弹出菜单与当前的位置最相关。

-   如果您将光标放在任何框，然后按鼠标右键按钮，使用菜单**撤消**，**剪切**，**复制**，**粘贴**，和**全选**选项会显示。 您可以选择上述任何选项。

 

 





