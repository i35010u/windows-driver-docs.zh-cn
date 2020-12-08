---
title: 编辑打开/关闭日志文件
description: 编辑打开/关闭日志文件
keywords:
- 编辑打开/关闭日志文件
- 日志文件，编辑打开/关闭日志文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1128e3106e52a94b56320c73cd94d51f4febb21
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839161"
---
# <a name="edit--openclose-log-file"></a>编辑 | 打开/关闭日志文件


## <span id="ddk_edit_open_close_log_file_dbg"></span><span id="DDK_EDIT_OPEN_CLOSE_LOG_FILE_DBG"></span>


在 "**编辑**" 菜单上单击 "**打开/关闭日志文件**"，以写入新的日志文件，附加到现有日志文件，或关闭打开的日志文件。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

单击 " **打开/关闭日志文件**" 时，将显示 " **打开/关闭日志文件** " 对话框。 此对话框显示当前日志文件（如果已打开）。

如果 " **日志文件名称** " 框为空，则可以输入日志文件名。 如果此文件已存在，则 WinDbg 将覆盖现有文件，除非您选中 " **追加** " 复选框。 如果指定文件名而不指定路径，则 WinDbg 会将该文件放入您从 WinDbg 开始的默认目录中。

如果 " **日志文件名称** " 框中已显示文件名，则可以单击 " **关闭打开的日志文件** " 以关闭该文件。 如果清除 " **日志文件名** " 框并输入新的日志文件名称，则将关闭以前的日志文件。

单击 **"确定"** 以保存更改，或单击 " **取消** " 以放弃更改。

如果在 "**日志文件名称**" 框中未出现日志文件名时单击 **"确定"** ，则它不起作用。 也就是说，WinDbg 不会关闭日志文件或打开日志文件。

但是，如果某个日志文件已处于活动状态，而你在没有清除其名称或选择 "**追加**" 的情况下单击 **"确定"** ，则 WinDbg 将删除该日志文件并使用具有相同名称的新文件。

 

 





