---
title: 编辑打开/关闭日志文件
description: 编辑打开/关闭日志文件
ms.assetid: f63549f7-1516-48a0-8af8-38cca103215c
keywords:
- 编辑打开/关闭日志文件
- 日志文件，编辑打开/关闭日志文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fa0901060663ed5f1484d6d2b5bdd99ff67903d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331404"
---
# <a name="edit--openclose-log-file"></a>编辑 | 打开/关闭日志文件


## <span id="ddk_edit_open_close_log_file_dbg"></span><span id="DDK_EDIT_OPEN_CLOSE_LOG_FILE_DBG"></span>


单击**打开/关闭日志文件**上**编辑**菜单写入到新的日志文件、 附加到现有的日志文件，或关闭打开的日志文件。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

当您单击**打开/关闭日志文件**，则**打开/关闭日志文件**对话框随即出现。 此对话框显示当前的日志文件，如果已打开。

如果**日志文件名称**框为空，则可以输入日志文件名称。 如果此文件已存在，WinDbg 将覆盖现有文件，除非已选择**追加**复选框。 如果指定文件名称，但没有路径，WinDbg 将文件放在开始从 WinDbg 的默认目录中。

如果**日志文件名称**框中已显示文件名称，可以单击**关闭打开的日志文件**关闭此文件。 如果清除**日志文件名称**框并输入新的日志文件名称，将关闭以前的日志文件。

单击**确定**以保存更改，或单击**取消**放弃更改。

如果单击**确定**任何日志文件名称中出现时**日志文件名称**框中，它不起作用。 也就是说，WinDbg 不关闭日志文件或打开日志文件。

但是，如果日志文件已处于活动状态并且单击**确定**而无需清除其名称或选择**追加**，WinDbg 中删除日志文件，并使用具有相同名称的新文件。

 

 





