---
title: 编辑转到地址
description: 编辑转到地址
ms.assetid: 152bdbb1-87e5-4a73-a1b7-1c4997f4a41c
keywords:
- 编辑转到地址
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 382806163042c46208aaeee42fade339070023e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331407"
---
# <a name="edit--go-to-address"></a>编辑 | 转到地址


## <span id="ddk_edit_go_to_address_dbg"></span><span id="DDK_EDIT_GO_TO_ADDRESS_DBG"></span>


单击**转到地址**上**编辑**菜单转到目标的虚拟地址空间中的地址。

此命令相当于按下 CTRL + G。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

当您单击**转到地址**，则**查看代码的偏移量**对话框随即出现。 在此对话框中，输入你想要将移动到的地址。 此地址可以是 （如函数、 符号或整数的内存地址） 的表达式或任何有效的地址的表达式。 如果地址是不明确，对话框将显示一个列表，其中包含所有不明确的项。

**请注意**  如果将光标放在行内[反汇编窗口](disassembly-window.md)或[源窗口](source-window.md)，然后使用**转到地址**命令，所选行的地址将出现在**视图代码偏移量**对话框。 可以使用此地址，也可以替换所选的任何地址。

 

单击后**确定**，调试器会插入符号 (^) 移动到开头的函数或在反汇编窗口或源窗口中的地址。

可以使用**转到地址**命令在当前处于活动状态的任何窗口中。 如果调试器在反汇编模式下，WinDbg 在反汇编窗口中查找的地址。 如果调试器在源文件模式下，WinDbg 在源窗口中查找的地址。 如果在源窗口中找不到该地址，WinDbg 将查找其在反汇编窗口中。 如果在相应的窗口未打开，WinDbg 将打开它。

**转到地址**命令只会更改 WinDbg 显示。 此命令不会影响目标或任何其他调试器操作的执行。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

在调试信息窗口中查找文本的其他方式的详细信息，请参阅[移动到窗口](moving-through-a-window.md)。

 

 





