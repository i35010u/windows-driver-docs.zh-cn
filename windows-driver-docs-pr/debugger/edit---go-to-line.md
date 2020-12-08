---
title: 编辑行
description: 编辑行
keywords:
- 编辑行
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5511b6c81eb50a3dc1d603c6702bfe48df8d0bf8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828887"
---
# <a name="edit--go-to-line"></a>编辑 | 转到行


## <span id="ddk_edit_go_to_line_dbg"></span><span id="DDK_EDIT_GO_TO_LINE_DBG"></span>


在 "**编辑**" 菜单上单击 "**前往行**" 以在当前活动的 [源窗口](source-window.md)中搜索特定的行。 如果活动窗口不是源窗口，则此命令不起作用。

此命令等效于按 CTRL + L。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

单击 " **前往行**" 时，将显示 " **转为行** " 对话框。 在此对话框中，输入要查找的行号，然后单击 **"确定"**。 调试器会将插入符号 (^) 移动到该行。 如果行号大于文件中的最后一行，则光标将移至文件末尾。

" **中转到行** " 命令仅更改 WinDbg 显示。 此命令不会影响目标或任何其他调试器操作的执行。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关在调试信息窗口中查找文本的其他方法的详细信息，请参阅在 [窗口中移动](moving-through-a-window.md)。

 

 





