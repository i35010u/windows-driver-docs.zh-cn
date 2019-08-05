---
title: 文件内核调试
description: 文件内核调试
ms.assetid: a80b3572-87a0-4a9d-9b62-67e1ca65fff4
keywords:
- 文件内核调试
- 正在启动调试器，文件内核调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2eefaac7ca95add2d332034c23d79a1c19d068ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369773"
---
# <a name="file--kernel-debug"></a>文件 | 内核调试


## <span id="ddk_file_kernel_debug_dbg"></span><span id="DDK_FILE_KERNEL_DEBUG_DBG"></span>


单击**内核调试**上**文件**菜单调试在内核模式下的目标计算机。

此命令相当于按下 CTRL + K。 仅当 WinDbg 处于休眠模式时，可以使用此命令。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

当您单击**内核调试**，则**内核调试**对话框将显示与这些选项卡：

- **COM**选项卡指示连接将使用的 COM 端口。 在中**波特率**框中，输入的波特率。 在中**端口**框中，输入的 COM 端口的名称。 有关详细信息，请参阅[设置启动串行连接手动](setting-up-a-null-modem-cable-connection.md)。

  COM 选项卡还可用于连接到虚拟机通过命名管道。 在中**端口**框中，输入 **\\ \\** <em>VMHost</em> **\\管道\\** <em>PipeName</em>。 *VMHost*指定在其运行虚拟机的物理计算机的名称。 如果内核调试器本身相同的计算机上运行虚拟机，使用单个句点 （.） 进行*VMHost*。 有关详细信息，请参阅[设置连接到虚拟机](attaching-to-a-virtual-machine--kernel-mode-.md)。

- **1394年**选项卡指示连接将使用 1394年。 在中**通道**框中，输入 1394年频道号。 仅当主计算机和目标计算机运行 Windows XP 或更高版本的 Windows 操作系统支持 1394年调试。 有关详细信息，请参阅[设置 1394年连接手动](setting-up-a-1394-cable-connection.md)。

- **USB**选项卡指示连接将使用 USB 2.0 或 USB 3.0。 在中**目标名称**框中，输入你配置目标计算机时创建的目标名称。 有关详细信息，请参阅[设置了 USB 2.0 连接手动](setting-up-a-usb-2-0-debug-cable-connection.md)并[设置了 USB 3.0 连接手动](setting-up-a-usb-3-0-debug-cable-connection.md)。

- **NET**选项卡指示连接将使用以太网。 在中**端口号**框中，输入目标计算机的配置时指定的端口号。 在中**密钥**框中，输入您为其生成的密钥 （或创建） 配置目标计算机时。 有关详细信息，请参阅[设置了网络连接手动](setting-up-a-network-debugging-connection.md)。

- **本地**选项卡指示 WinDbg 将执行本地内核调试。 支持本地内核调试，仅在 Windows XP 及更高版本。

有关详细信息和从内核调试会话的其他方法，请参阅[Live 内核模式调试使用 WinDbg](performing-kernel-mode-debugging-using-windbg.md)。

 

 





