---
title: 编辑 EFI 中的启动选项
description: 编辑 EFI 中的启动选项
ms.assetid: 0fdd01b3-7475-4959-87d8-5ec8ae65fea0
keywords:
- WDK 的 NVRAM 引导选项编辑
- EFI NVRAM 启动选项 WDK，编辑
- 编辑启动选项
- Bootcfg 工具
- Nvrboot 工具
- 编辑器 WDK 启动选项
- 查看启动选项
- NVRAM 启动选项 WDK 中查看
- EFI NVRAM 启动选项 WDK 中查看
- 启动选项 WDK，编辑
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: d9dc5ea74b6d95452edce219253eef5a00aa45c9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344825"
---
# <a name="editing-boot-options-in-efi"></a>编辑 EFI 中的启动选项


若要编辑的启动选项的计算机上使用 EFI NVRAM 在运行 Windows Server 2003 或早期版本的基于 NT 的 Windows，请使用 Bootcfg (bootcfg.exe)，Windows 或 Nvrboot (nvrboot.efi)，在 EFI 环境中运行的工具运行的工具。 在 Windows XP 64-Bit Edition 和 Windows Server 2003 的 64 位版本中包含这两个工具。

您还可以查看和更改系统下的控制面板中的某些启动选项。 在系统属性对话框高级选项卡上，单击下的设置**启动和恢复**。 此功能会受到限制，因为它不是在本部分中讨论。 璝惠**启动和恢复**对话框框中，请参阅帮助和支持中心。

## <a name="bootcfg"></a>Bootcfg

Bootcfg (bootcfg.exe) 是编辑启动选项的命令行工具的本地或远程计算机上使用相同的 Bootcfg 命令和过程，您可以编辑 Boot.ini 文件或 EFI NVRAM 中的启动选项。 Bootcfg 包含在 %systemroot%\\Windows XP 和 Windows Server 2003 中的 System32 目录。 （Bootcfg 显示的内容存储在 EFI NVRAM 中的启动选项的系统上略有不同，但命令是相同）。

Bootcfg 可用于添加、 删除和更改的所有有效的启动选项; 值但是，不能设置无限超时值。 此外可以使用 Bootcfg 命令脚本或批处理文件中设置启动选项或重置密码后替换或升级操作系统。

在系统上存储在 EFI NVRAM 中的启动选项，Bootcfg 还可以还显示启动分区表、 添加镜像驱动器的启动项和更新的系统分区的 Guid。

您必须使用 Bootcfg 的计算机上的管理员组的成员。 有关使用 Bootcfg 详细说明，请参阅帮助和支持中心。

## <a name="nvrboot"></a>Nvrboot

Nvrboot (nvrboot.efi) 是基于 EFI 的启动项编辑器包含在 Windows XP 64 位版本和 Windows Server 2003 的 64 位版本。 Nvrboot 在 EFI 环境中运行。 运行操作系统时，不能运行 Nvrboot。

Nvrboot 编辑仅启动项。 您不能使用它来显示或更改超时值为启动菜单中，尽管可以使用**推送**命令 (**nvrboot p**) 更改默认启动项目。

Nvrboot 还包括命令来启动项的备份副本导出和导入的到 NVRAM 的启动项的备份副本。 中介绍了此过程[备份在 EFI 启动选项](backing-up-boot-options-in-efi.md)部分。

Nvrboot 用户友好格式显示启动选项。 例如，它显示的操作系统文件路径和启动加载程序文件路径作为分区跟 Windows 目录路径的 GUID。

以下过程说明如何启动 Nvrboot 从 EFI 外壳程序具有许多基于 Itanium 的系统提供的工具。 因为 EFI 外壳程序工具的制造商中不同，此部分中的说明可能不准确地描述 EFI shell 接口在特定计算机上。

**若要运行 Nvrboot**

1.  重新启动计算机。

2.  从**引导**菜单中，选择**EFI 外壳程序**。

3.  在 shell 提示符下，键入系统分区，如 c： 的驱动器号或文件系统编号或**FS**n，其中 n 是系统分区的文件系统编号。

4.  类型**cd msutil**以导航到 Msutil 目录 nvrboot.efi 所在的位置。

5.  若要启动 Nvrboot，键入**nvrboot**。

若要查找有关 Nvrboot 的说明，请键入**h**。
