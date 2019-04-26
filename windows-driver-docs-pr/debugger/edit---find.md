---
title: 编辑查找
description: 编辑查找
ms.assetid: 9e3a0095-1bce-4262-a22c-584de54113cc
keywords:
- 编辑查找
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40ed1c15d5a284ce65db2947cc4ca344b50212f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331411"
---
# <a name="edit--find"></a>编辑 | 查找


## <span id="ddk_edit_find_dbg"></span><span id="DDK_EDIT_FIND_DBG"></span>


单击**查找**上**编辑**菜单在活动的调试信息窗口中查找文本。

**请注意**  必须是活动窗口[调试器命令窗口](debugger-command-window.md)或[源窗口](source-window.md)。

 

此命令相当于按下 CTRL + F。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

当您单击**查找**，则**查找**对话框随即出现。 在此对话框中，在**查找内容**框中，输入你想要查找的文本。 如果已经选择的文本，此文本将自动显示在**查找内容**框。

在中**方向**区域中，单击**向上**或**下**指定你的搜索方向。 只要光标位于窗口开始执行搜索。 通过使用鼠标指针，可以将光标放在任何位置。

选择**仅全字匹配**如果你想要搜索整个单词。 （如果在多个字词搜索时选择此选项，您一定会收到搜索失败。））

选择**区分大小写**执行区分大小写的搜索。

**查找**命令只会更改 WinDbg 显示。 此命令不会影响目标或任何其他调试器操作的执行。

关闭后**查找**对话框中，您可以通过使用重复向前搜索[编辑 |查找下一个](edit---find-next.md)命令或按 f3 键。 您可以通过按 SHIFT + F3 重复向后的搜索。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关在调试信息窗口中查找文本的其他方法的详细信息，请参阅[移动到窗口](moving-through-a-window.md)。

 

 





