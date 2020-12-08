---
title: 文件映射网络驱动器
description: 文件映射网络驱动器
keywords:
- 文件映射网络驱动器
- shell 命令，文件映射网络驱动器
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb9cfa4a935de264a7e6020895cd1aac62e5321e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816371"
---
# <a name="file--map-network-drive"></a>文件 | 映射网络驱动器


## <span id="ddk_file_map_network_drive_dbg"></span><span id="DDK_FILE_MAP_NETWORK_DRIVE_DBG"></span>


在 "**文件**" 菜单上单击 "**映射网络驱动器**"，以添加网络连接并为这些连接分配驱动器号。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

单击 " **映射网络驱动器**" 时，将显示 " **映射网络驱动器** " 对话框。 使用 " **驱动器** " 和 " **文件夹** " 菜单选择服务器并共享并为其分配驱动器号。

此对话框的工作方式与 Windows 资源管理器的相应功能完全相同。

**文件 |Map Network Drive** 命令只影响运行 WinDbg 的计算机的网络连接。 如果在远程调试会话中使用 WinDbg 作为客户端，并且想要更改服务器的网络连接，则必须使用 **shell net use** 命令。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关访问命令行界面的详细信息，请参阅 [使用 Shell 命令](using-shell-commands.md)。

 

 





