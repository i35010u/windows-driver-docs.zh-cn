---
title: 编辑转到行
description: 编辑转到行
ms.assetid: af7f2afc-95cb-4dcd-9b74-1bd46713239f
keywords:
- 编辑转到行
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8da4755023abac4168106b0c3329d47757d370be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547200"
---
# <a name="edit--go-to-line"></a>编辑 |转到行


## <span id="ddk_edit_go_to_line_dbg"></span><span id="DDK_EDIT_GO_TO_LINE_DBG"></span>


单击**转到行**上**编辑**菜单在当前活动中搜索的特定行[源窗口](source-window.md)。 如果活动窗口不是源窗口，则此命令无效。

此命令相当于按下 CTRL + L。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

当您单击**转到行**，则**转到行**对话框随即出现。 在此对话框中，输入你想要查找，然后单击的行号**确定**。 调试器会将插入符号 (^) 移动到该行。 如果大于文件中的最后一行的行号，光标将移动到文件末尾。

**转到行**命令只会更改 WinDbg 显示。 此命令不会影响目标或任何其他调试器操作的执行。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

在调试信息窗口中查找文本的其他方式的详细信息，请参阅[移动到窗口](moving-through-a-window.md)。

 

 





