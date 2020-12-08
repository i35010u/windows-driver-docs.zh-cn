---
title: 通过窗口移动
description: 通过窗口移动
keywords:
- 调试信息窗口，导航
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ce5372e2af8143443d86f33180249bd6b2d8f3e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837003"
---
# <a name="moving-through-a-window"></a>通过窗口移动


## <span id="ddk_moving_through_a_window_dbg"></span><span id="DDK_MOVING_THROUGH_A_WINDOW_DBG"></span>


可以通过多种方法在调试信息窗口中进行移动。

如果滚动条出现在窗口中，您可以使用它来显示窗口中的更多。

此外，某些 windows 支持 " **查找**"、" **中转到地址**" 或 " **中转到行** " 命令。 这些命令仅更改 WinDbg 显示。 它们不会影响目标或任何其他调试器操作的执行。

### <a name="span-idfind_commandspanspan-idfind_commandspanfind-command"></a><span id="find_command"></span><span id="FIND_COMMAND"></span>Find 命令

可以在 [调试器命令窗口](debugger-command-window.md)或 [源窗口](source-window.md)中使用 "**查找**" 命令。

如果其中一个窗口处于活动状态，请单击 "**编辑**" 菜单上的 "**查找**" 或按 CTRL + F。 " **查找** " 对话框将打开。

在对话框中输入要查找的文本，然后选择 " **向上** " 或 " **向下** " 来确定搜索的方向。 在光标位于窗口中的任何位置开始搜索。 您可以使用鼠标将光标置于任何位置。

如果要搜索单个单词，请选中 " **仅全字匹配** " 复选框。  (如果您选中此复选框，并且您输入了多个字词，则将忽略此复选框。 ) 选中 "区分 **大小写** " 复选框以执行区分大小写的搜索。

如果关闭 "**查找**" 对话框，则可以通过在 "**编辑**" 菜单上单击 "**查找下** 一个" 或按 F3，按向前方向重复上一个搜索。 可以通过按 SHIFT + F3 向后方向重复搜索。

### <a name="span-idgo_to_address_commandspanspan-idgo_to_address_commandspango-to-address-command"></a><span id="go_to_address_command"></span><span id="GO_TO_ADDRESS_COMMAND"></span>中转到 Address 命令

" **中转到地址** " 命令在要调试的应用程序中搜索地址。 若要使用此选项，请在 "**编辑**" 菜单上单击 "**前往地址**" 或按 CTRL + G。

当 " **查看代码偏移量** " 对话框出现时，请输入要搜索的地址。 您可以输入此地址作为表达式，如函数、符号或整数内存地址。 如果地址不明确，则会出现一个列表，其中包含所有不明确的项。

单击 **"确定**" 后，调试器会将光标移到 " [反汇编" 窗口](disassembly-window.md) 或 " [源" 窗口](source-window.md)中的函数或地址的开头。

无论打开哪个调试信息窗口，都可以使用 " **跳到地址** " 命令。 如果调试器处于反汇编模式，调试器将在 "反汇编" 窗口中找到要搜索的地址。 如果调试器处于源模式，则调试器将尝试在源窗口中查找该地址。 如果调试器在源窗口中找不到该地址，则调试器将在 "反汇编" 窗口中找到该地址。 如果需要的窗口未打开，调试器会将其打开。

### <a name="span-idmoving_to_a_specific_linespanspan-idmoving_to_a_specific_linespanmoving-to-a-specific-line"></a><span id="moving_to_a_specific_line"></span><span id="MOVING_TO_A_SPECIFIC_LINE"></span>移到特定行

" **中转到行** " 命令在 "活动源" 窗口中搜索行号。 如果活动窗口不是源窗口，则不能使用 " **前往行** " 命令。

若要激活此选项，请在 "**编辑**" 菜单上单击 "**前往行**" 或按 CTRL + L。

出现 " **转为行** " 对话框时，输入要查找的行号，然后单击 **"确定"**。 调试器将光标移到该行。 如果行号大于文件中的最后一行，则光标将移至文件末尾。

 

 





