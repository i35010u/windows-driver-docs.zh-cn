---
title: 文件内核调试
description: 文件内核调试
keywords:
- 文件内核调试
- 启动调试程序，文件内核调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96a09ea16ce19d6c64084875fcf83c49136f9daa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840203"
---
# <a name="file--kernel-debug"></a>文件 | 内核调试


## <span id="ddk_file_kernel_debug_dbg"></span><span id="DDK_FILE_KERNEL_DEBUG_DBG"></span>


单击 "**文件**" 菜单上的 "**内核调试**" 以在内核模式下调试目标计算机。

此命令等效于按 CTRL + K。 仅当 WinDbg 处于休眠模式时，才能使用此命令。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

单击 " **内核调试**" 时，将显示 " **内核调试** " 对话框，其中包含以下选项卡：

- **Com** 选项卡指示连接将使用 COM 端口。 在 " **波特率** " 框中，输入波特率。 在 " **端口** " 框中，输入 COM 端口的名称。 有关详细信息，请参阅 [手动设置串行连接](setting-up-a-null-modem-cable-connection.md)。

  你还可以使用 "COM" 选项卡通过命名管道连接到虚拟机。 在 "**端口**" 框中，输入 **\\\\** <em>VMHost</em>**\\ pipe \\**<em>PipeName</em>。 *VMHost* 指定运行虚拟机的物理计算机的名称。 如果虚拟机运行在与内核调试器自身相同的计算机上，请使用单个句点 (. ) 用于 *VMHost*。 有关详细信息，请参阅 [设置与虚拟机的连接](attaching-to-a-virtual-machine--kernel-mode-.md)。

- **1394** 选项卡指示连接将使用1394。 在 " **频道** " 框中，输入1394频道号。 仅当主计算机和目标计算机都运行的是 Windows XP 或更高版本的 Windows 操作系统时，才支持调试。1394 有关详细信息，请参阅 [手动设置1394连接](setting-up-a-1394-cable-connection.md)。

- **Usb** 选项卡指示连接将使用 usb 2.0 或 usb 3.0。 在 " **目标名称** " 框中，输入在配置目标计算机时创建的目标名称。 有关详细信息，请参阅 [手动设置 usb 2.0 连接](setting-up-a-usb-2-0-debug-cable-connection.md) 和 [手动设置 usb 3.0 连接](setting-up-a-usb-3-0-debug-cable-connection.md)。

- **NET** 选项卡指示连接将使用以太网。 在 " **端口号** " 框中，输入在配置目标计算机时指定的端口号。 在 " **密钥** " 框中，输入为你 (生成的密钥，或者在配置目标计算机时) 创建的密钥。 有关详细信息，请参阅 [手动设置网络连接](setting-up-a-network-debugging-connection.md)。

- " **本地** " 选项卡指示 WinDbg 将执行本地内核调试。 仅在 Windows XP 和更高版本上支持本地内核调试。

有关开始内核调试会话的其他方法的详细信息，请参阅 [使用 WinDbg 进行实时 Kernel-Mode 调试](performing-kernel-mode-debugging-using-windbg.md)。

 

 





