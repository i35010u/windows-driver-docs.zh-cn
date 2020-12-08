---
title: 剪切和粘贴文本
description: 剪切和粘贴文本
keywords:
- 剪切文本
- 粘贴文本
- 复制文本
- 调试信息窗口，剪切和粘贴文本
- text
- 文本，编辑
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a1bc90dcd853777384029c7de6b37bbf0e62d22
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787831"
---
# <a name="cutting-and-pasting-text"></a>剪切和粘贴文本


## <span id="ddk_cutting_and_pasting_text_dbg"></span><span id="DDK_CUTTING_AND_PASTING_TEXT_DBG"></span>


WinDbg 使用多种常用的方法来操作文本和几个不太熟悉的方法。

### <a name="span-idselecting_textspanspan-idselecting_textspanselecting-text"></a><span id="selecting_text"></span><span id="SELECTING_TEXT"></span>选择文本

若要在 [源窗口](source-window.md)中选择文本，请在 " [反汇编" 窗口](disassembly-window.md)中的任意一个窗格中 [命令窗口](debugger-command-window.md)，或在对话框中，指向文本的一端，按住鼠标左键，然后将指针拖到文本的另一端。

若要选择窗口中的所有文本，还可以在 "**编辑**" 菜单上单击 "全 [选](edit---select-all.md)"，或按 CTRL + a。

在 " [调用" 窗口](calls-window.md)、"监视窗口"、" [局部变量" 窗口](locals-window.md)、"寄存器" [窗口](registers-window.md)和 " [内存" 窗口](memory-window.md)中，您无法选择任意范围的文本，但您可以选择整行或单元格。 单击所需的行或单元格以选择其文本。

输入文本时，按 DELETE 键和 BACKSPACE 键可分别删除光标右侧或左侧的文本。 如果选择 "文本"，则可以按这些键来删除选定内容。 如果选择 "文本"，然后键入任何字符，则新字符将替换您选择的内容。

### <a name="span-idcopying_textspanspan-idcopying_textspancopying-text"></a><span id="copying_text"></span><span id="COPYING_TEXT"></span>复制文本

若要复制文本，请选择该文本，然后执行下列操作之一：

-   按鼠标右键。  (此方法仅适用于某些位置。 有关如何使用鼠标右键的详细信息，请参阅鼠标右键。 ) 

-   按 CTRL + C。

-   按 CTRL + INSERT。

-   仅) 在 "**编辑**" 菜单上单击 "**复制**" (固定和选项卡式窗口。

-   在工具栏 **Copy (Ctrl+C)** 上，单击 " ![ 复制" 按钮)  (屏幕截图中的 "复制 (") "按钮 ](images/tbcopy.png) 。

### <a name="span-idcutting_textspanspan-idcutting_textspancutting-text"></a><span id="cutting_text"></span><span id="CUTTING_TEXT"></span>剪切文本

若要剪切并将文本移动到剪贴板，请选择文本，然后执行下列操作之一：

-   按 CTRL + X。

-   按 SHIFT + DELETE。

-   仅) 单击 "**编辑**" 菜单上的 "**剪切**" (固定和选项卡式窗口。

-   单击工具栏上的 "剪切" 按钮) 的 "剪切 **(Ctrl + X)** " 按钮 (![ 屏幕截图 ](images/tbcut.png) 。

您可以从调试器的底部窗格中剪切文本，命令窗口，从监视窗口的左栏和任何对话框 (也就是说，从支持文本输入) 的任何位置。

### <a name="span-idpasting_textspanspan-idpasting_textspanpasting-text"></a><span id="pasting_text"></span><span id="PASTING_TEXT"></span>粘贴文本

若要从剪贴板粘贴文本，请将光标置于要插入文本的位置 (或选择要替换的文本) 然后执行以下操作之一：

-   按鼠标右键。  (此方法仅适用于某些位置，不能使用此方法替换文本。 有关如何使用此方法的详细更多信息，请参阅鼠标右键。 ) 

-   按 CTRL + V。

-   按 SHIFT + INSERT。

-   仅) 在 "**编辑**" 菜单上单击 "**粘贴**" (停靠和选项卡式窗口。

-   单击 " **粘贴" ("Ctrl + V)** " 按钮 (![ tooblar 上 "粘贴" 按钮) 屏幕截图 ](images/tbpaste.png) 。

您可以将文本粘贴到调试器的底部窗格中命令窗口，将文本粘贴到监视窗口的左侧列中，并粘贴到任何对话框 (也就是说，的任何位置都支持文本输入) 。

### <a name="span-idright_mouse_buttonspanspan-idright_mouse_buttonspanright-mouse-button"></a><span id="right_mouse_button"></span><span id="RIGHT_MOUSE_BUTTON"></span>鼠标右键

鼠标右键具有几个效果，可以更快地进行复制和粘贴：

-   如果在调试器的任一窗格中选择文本命令窗口，请在 "反汇编" 窗口中的 "反汇编" 窗口或任何源窗口中选择文本，然后按鼠标右键，将文本复制到剪贴板。 不过，如果已在视图中取消选择 " **快速编辑" 模式** [|选项](view---options.md)，在这些位置右键单击将弹出与当前位置最相关的菜单。

-   如果将光标置于 (而不在命令窗口调试器的任一窗格中) 选择任何文本，请在 "暂存" 面板中，或在监视窗口的 "文本" 项空间中，然后按鼠标右键，将剪贴板的内容粘贴到窗口中。 不过，如果已在视图中取消选择 " **快速编辑" 模式** [|选项](view---options.md)，在这些位置右键单击将弹出与当前位置最相关的菜单。

-   如果将光标放在任何框中，然后按鼠标右键，则会出现一个菜单，其中包含 " **撤消**"、" **剪切**"、" **复制**"、" **粘贴**" 和 " **全选** " 选项。 您可以选择这些选项中的任何一个。

 

 





