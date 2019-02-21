---
title: 文件映射网络驱动器
description: 文件映射网络驱动器
ms.assetid: 55a5523f-5735-4b44-8d98-ded9932e630a
keywords:
- 文件映射网络驱动器
- shell 命令，文件映射网络驱动器
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fc898edc99e4fee25e9f37e0b80f46d0e819a36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544666"
---
# <a name="file--map-network-drive"></a>文件 |映射网络驱动器


## <span id="ddk_file_map_network_drive_dbg"></span><span id="DDK_FILE_MAP_NETWORK_DRIVE_DBG"></span>


单击**映射网络驱动器**上**文件**菜单可添加的网络连接和将驱动器号分配给这些连接。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

当您单击**映射网络驱动器**，则**映射网络驱动器**对话框随即出现。 使用**驱动器**并**文件夹**菜单，然后选择服务器和共享并为其分配驱动器号。

此对话框中的工作方式完全相同的 Windows 资源管理器中相应的功能。

**文件 |映射网络驱动器**命令会影响仅在其运行 WinDbg 的计算机的网络连接。 如果在远程调试会话中作为客户端使用 WinDbg，并且你想要更改服务器的网络连接，必须使用 **.shell net 使用**命令。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关访问命令行界面的详细信息，请参阅[使用 Shell 命令](using-shell-commands.md)。

 

 





