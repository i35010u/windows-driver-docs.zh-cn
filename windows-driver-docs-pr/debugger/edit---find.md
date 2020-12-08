---
title: 编辑查找
description: 编辑查找
keywords:
- 编辑查找
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25ef238652423d224ec4d9029a25138821a3aa1b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815213"
---
# <a name="edit--find"></a>编辑 | 查找


## <span id="ddk_edit_find_dbg"></span><span id="DDK_EDIT_FIND_DBG"></span>


单击 "**编辑**" 菜单上的 "**查找**"，在 "活动调试信息" 窗口中查找文本。

**注意**  活动窗口必须是 [调试器命令窗口](debugger-command-window.md) 或 [源窗口](source-window.md)。

 

此命令等效于按 CTRL + F。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

单击 " **查找**" 时，将显示 " **查找** " 对话框。 在此对话框的 " **查找内容** " 框中，输入要查找的文本。 如果已选择文本，则该文本会自动显示在 " **查找内容** " 框中。

在 " **方向** " 区域中，单击 " **向上** " 或 " **向下** " 以指定搜索的方向。 在光标位于窗口中的任何位置开始搜索。 您可以使用鼠标指针将光标置于任何位置。

仅当要搜索单个单词时，选择 " **全字匹配** "。  (如果您在搜索多个字词时选择此选项，则始终会收到失败的搜索。 ) # A2

选择 "区分 **大小写** " 以执行区分大小写的搜索。

" **查找** " 命令仅更改 WinDbg 显示。 此命令不会影响目标或任何其他调试器操作的执行。

关闭 " **查找** " 对话框后，可以通过使用 " [编辑 |查找下一个](edit---find-next.md) 命令或按 F3。 可以通过按 SHIFT + F3 向后方向重复搜索。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关在调试信息窗口中查找文本的其他方法的详细信息，请参阅在 [窗口中移动](moving-through-a-window.md)。

 

 





