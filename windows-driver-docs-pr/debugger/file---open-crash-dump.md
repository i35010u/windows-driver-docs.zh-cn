---
title: 文件打开故障转储
description: 文件打开故障转储
keywords:
- 文件打开故障转储
- 启动调试程序，文件打开故障转储
- 转储文件，文件打开故障转储
ms.date: 08/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: 65637b1dc69a93ac65f138358397bb61accb4584
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827347"
---
# <a name="file--open-crash-dump"></a>文件 | 打开故障转储


## <span id="ddk_file_open_crash_dump_dbg"></span><span id="DDK_FILE_OPEN_CRASH_DUMP_DBG"></span>


单击 "**文件**" 菜单上的 "**打开故障转储**"，打开用户模式或内核模式故障转储文件并对其进行分析。

此命令等效于按 CTRL + D。 仅当 WinDbg 处于休眠模式时，才能使用此命令。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

单击 " **打开故障转储**" 时，将显示 " **打开故障转储** " 对话框。 在 **"文件名" 框** 中输入故障转储文件的完整路径，或使用 " **查找范围** " 列表查找并选择正确的路径和文件名。  (转储文件通常以 dmp 或 .mdmp 扩展名结尾。 ) 

选择了正确的文件后，单击 " **打开**"。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关分析故障转储文件的详细信息，请参阅 [分析 User-Mode 转储文件](analyzing-a-user-mode-dump-file.md) 或 [使用 WinDbg 分析 Kernel-Mode 转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)。

 

 





