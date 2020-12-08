---
title: 文件断开连接网络驱动器
description: 文件断开连接网络驱动器
keywords:
- 文件断开连接网络驱动器
- shell 命令，文件断开连接网络驱动器
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: bab1a6c7c941491c48b86a6593a5ac8ac691d96a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828205"
---
# <a name="file--disconnect-network-drive"></a>文件 | 断开与网络驱动器的连接


## <span id="ddk_file_disconnect_network_drive_dbg"></span><span id="DDK_FILE_DISCONNECT_NETWORK_DRIVE_DBG"></span>


单击 "**文件**" 菜单上的 "**断开网络驱动器**" 以删除网络连接。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

单击 " **断开网络驱动器**" 时，将显示 " **断开连接网络驱动器** " 对话框。 在 " **网络驱动器** " 框中，选择要删除的连接，然后单击 **"确定"**。

此对话框的工作方式与 Windows 资源管理器的相应功能完全相同。

**文件 |"断开连接网络驱动器**" 命令只影响 WinDbg 正在运行的计算机的网络连接。 如果在远程调试会话中使用 WinDbg 作为客户端，并且想要更改服务器的网络连接，则必须使用 **shell net use** 命令。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关访问命令行界面的详细信息，请参阅 [使用 Shell 命令](using-shell-commands.md)。

 

 





