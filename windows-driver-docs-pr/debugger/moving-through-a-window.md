---
title: 通过窗口移动
description: 通过窗口移动
ms.assetid: c164a446-1f6c-4d37-8ad6-aa254d3268bc
keywords:
- 调试信息窗口中导航
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45f14eadd827386e503aca77ebddb6f2669f1fab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524505"
---
# <a name="moving-through-a-window"></a>通过窗口移动


## <span id="ddk_moving_through_a_window_dbg"></span><span id="DDK_MOVING_THROUGH_A_WINDOW_DBG"></span>


有几种方法的经过调试的信息窗口。

如果在窗口中显示滚动条，可用于显示的窗口的详细信息。

此外，某些 windows 支持**查找**，**转到地址**，或**转到行**命令。 这些命令仅更改 WinDbg 显示。 它们不会影响目标或任何其他调试器操作的执行。

### <a name="span-idfindcommandspanspan-idfindcommandspanfind-command"></a><span id="find_command"></span><span id="FIND_COMMAND"></span>查找命令

可以使用**查找**命令，在[调试器命令窗口](debugger-command-window.md)中或在[源窗口](source-window.md)。

当一个这些窗口处于活动状态时，单击**查找**上**编辑**菜单或按 CTRL + F。 **查找**对话框随即打开。

输入你想要在对话框中，找到并选择的文本**向上**或**向下**来确定您的搜索方向。 只要光标位于窗口开始执行搜索。 您可以使用鼠标将光标放在任意位置。

选择**仅全字匹配**复选框，如果你想要搜索整个单词。 （如果选中此复选框，并输入多个单词，此复选框则忽略。）选择**区分大小写**复选框，执行区分大小写的搜索。

如果关闭**查找**对话框中，可以通过单击重复执行上一个搜索向前**查找下一步**上**编辑**菜单或按 F3。 您可以通过按 SHIFT + F3 重复向后的搜索。

### <a name="span-idgotoaddresscommandspanspan-idgotoaddresscommandspango-to-address-command"></a><span id="go_to_address_command"></span><span id="GO_TO_ADDRESS_COMMAND"></span>转到地址命令

**转到地址**命令正在调试的应用程序中的地址的搜索。 若要使用此选项，请单击**转到地址**上**编辑**菜单或按 CTRL + G。

当**视图代码偏移量**出现对话框，请输入你想要搜索的地址。 您可以输入此地址作为表达式，如函数、 符号或整数内存地址。 如果地址是不明确，列表会显示所有不明确的项。

单击后**确定**，调试器将光标移到开头的函数或中的地址[反汇编窗口](disassembly-window.md)或[源窗口](source-window.md)。

可以使用**转到地址**命令而不考虑哪些调试的信息窗口处于打开状态。 如果调试器在反汇编模式下，调试器将查找你要搜索在反汇编窗口中的地址。 如果调试器在源文件模式下，调试器会尝试在源窗口中查找的地址。 如果调试器无法在源窗口中查找的地址，调试器在反汇编窗口中查找的地址。 如果所需的窗口未打开，调试器将打开它。

### <a name="span-idmovingtoaspecificlinespanspan-idmovingtoaspecificlinespanmoving-to-a-specific-line"></a><span id="moving_to_a_specific_line"></span><span id="MOVING_TO_A_SPECIFIC_LINE"></span>将移动到的特定行

**转到行**命令搜索活动的源窗口中的行号。 如果活动窗口不是源窗口，则无法使用**转到行**命令。

若要激活此选项，请单击**转到行**上**编辑**菜单或按 CTRL + L。

当**转到行**出现对话框，请输入你想要查找，然后单击的行号**确定**。 调试器会将光标移动到该行。 如果大于文件中的最后一行的行号，光标将移到文件末尾。

 

 





