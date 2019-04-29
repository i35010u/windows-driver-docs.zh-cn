---
title: 文件断开连接的网络驱动器
description: 文件断开连接的网络驱动器
ms.assetid: 65d78f9b-0c3c-4ec8-906d-afdfa64beebb
keywords:
- 文件断开连接的网络驱动器
- shell 命令，文件断开网络驱动器
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: bae2d0bcfd8ddd61417d5ca3a406085669ddb604
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366821"
---
# <a name="file--disconnect-network-drive"></a>文件 | 断开与网络驱动器的连接


## <span id="ddk_file_disconnect_network_drive_dbg"></span><span id="DDK_FILE_DISCONNECT_NETWORK_DRIVE_DBG"></span>


单击**断开网络驱动器**上**文件**菜单，删除网络连接。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

当您单击**断开网络驱动器**，则**断开网络驱动器**对话框随即出现。 在中**网络驱动器**框中，选择你想要删除，然后单击的连接**确定**。

此对话框中的工作方式完全相同的 Windows 资源管理器中相应的功能。

**文件 |断开网络驱动器的连接**命令会影响仅在其运行 WinDbg 的计算机的网络连接。 如果在远程调试会话中作为客户端使用 WinDbg，并且你想要更改服务器的网络连接，必须使用 **.shell net 使用**命令。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关访问命令行界面的详细信息，请参阅[使用 Shell 命令](using-shell-commands.md)。

 

 





