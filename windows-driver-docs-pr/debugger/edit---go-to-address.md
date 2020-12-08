---
title: 编辑中转到地址
description: 编辑中转到地址
keywords:
- 编辑中转到地址
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40e29d61d30412671e079eb38d048ef3dcd69a9d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839163"
---
# <a name="edit--go-to-address"></a>编辑 | 转到地址


## <span id="ddk_edit_go_to_address_dbg"></span><span id="DDK_EDIT_GO_TO_ADDRESS_DBG"></span>


单击 "**编辑**" 菜单上的 "**定位到地址**"，以跳到目标虚拟地址空间中的某个地址。

此命令等效于按 CTRL + G。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

单击 " **前往地址**" 时，将显示 " **查看代码偏移量** " 对话框。 在此对话框中，输入要移动到的地址。 此地址可以是表达式 (如函数、符号或整数内存地址) 或任意有效的地址表达式。 如果地址不明确，则对话框将显示一个列表，其中包含所有不明确的项。

**注意**   如果将光标放在 " [反汇编" 窗口](disassembly-window.md) 或 [源窗口](source-window.md) 中的某一行上，然后使用 "**中转到地址** " 命令，则所选行的地址将显示在 " **查看代码偏移量** " 对话框中。 可以使用此地址，也可以将其替换为所选的任何地址。

 

单击 **"确定**" 后，调试器将在 "反汇编" 窗口或源窗口中的插入符号 (^) 移动到函数或地址的开头。

您可以使用当前处于活动状态的任何窗口中的 " **中转到地址** " 命令。 如果调试器处于反汇编模式，则 WinDbg 将在 "反汇编" 窗口中找到该地址。 如果调试器处于源模式，则 WinDbg 会在源窗口中查找该地址。 如果在源窗口中找不到该地址，则 WinDbg 将在 "反汇编" 窗口中找到该地址。 如果未打开适当的窗口，则 WinDbg 会将其打开。

" **中转到地址** " 命令仅更改 WinDbg 显示。 此命令不会影响目标或任何其他调试器操作的执行。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关在调试信息窗口中查找文本的其他方法的详细信息，请参阅在 [窗口中移动](moving-through-a-window.md)。

 

 





