---
title: 文件打开故障转储
description: 文件打开故障转储
ms.assetid: 0a398f9a-776b-4438-bde4-7654e1f813b7
keywords:
- 文件打开故障转储
- 正在启动调试器，文件打开故障转储
- 转储文件，文件打开故障转储
ms.date: 08/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: 997ec56fa1ebe7b5c784a61e43d5981e025893ad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361953"
---
# <a name="file--open-crash-dump"></a>文件 | 打开故障转储


## <span id="ddk_file_open_crash_dump_dbg"></span><span id="DDK_FILE_OPEN_CRASH_DUMP_DBG"></span>


单击**打开故障转储**上**文件**菜单以打开用户模式或内核模式崩溃转储文件，并对其进行分析。

此命令相当于按下 CTRL + D。 仅当 WinDbg 处于休眠模式时，可以使用此命令。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

当您单击**打开崩溃转储**，则**打开崩溃转储**对话框随即出现。 输入中的故障转储文件的完整路径**文件名**框中，或使用**查找**列表以查找并选择正确的路径和文件名称。 （转储文件通常具有.dmp 或.mdmp 扩展名结尾）。

选择适当的文件后，单击**打开**。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关分析故障转储文件的详细信息，请参阅[分析用户模式转储文件](analyzing-a-user-mode-dump-file.md)或[分析内核模式转储文件使用 WinDbg](analyzing-a-kernel-mode-dump-file-with-windbg.md)。

 

 





