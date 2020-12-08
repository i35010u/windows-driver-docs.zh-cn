---
title: 编辑 EFI 中的启动选项
description: 编辑 EFI 中的启动选项
keywords:
- NVRAM 启动选项 WDK，编辑
- EFI NVRAM 启动选项 WDK，编辑
- 编辑启动选项
- Bootcfg 工具
- Nvrboot 工具
- 编辑器 WDK 启动选项
- 查看启动选项
- NVRAM 启动选项 WDK，查看
- EFI NVRAM 启动选项 WDK，查看
- 启动选项 WDK，编辑
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 41bd056e31c3f79e03db7d09681f95ea4d0e0c03
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819787"
---
# <a name="editing-boot-options-in-efi"></a>编辑 EFI 中的启动选项


若要在运行 Windows Server 2003 或更早版本的基于 NT 的 Windows 的计算机上编辑启动选项，请使用 Bootcfg ( # A0) 、在 Windows 上运行的工具或 Nvrboot (Nvrboot) ，这是在 EFI 环境中运行的工具。 这两种工具都包含在 Windows XP 64 位版本和 Windows Server 2003 的64位版本中。

你还可以在 "系统" 下的 "控制面板" 中查看和更改某些启动选项。 在 "系统属性" 对话框中的 "高级" 选项卡上，选择 " **启动和恢复**" 下的设置。 由于此功能有限，本部分未对此进行讨论。 有关 " **启动和恢复** " 对话框的信息，请参阅帮助和支持中心。

## <a name="bootcfg"></a>Bootcfg

Bootcfg ( # A0) 是一个命令行工具，可使用相同的 Bootcfg 命令和过程在本地或远程计算机上编辑启动选项，可以在 EFI NVRAM 中编辑 Boot.ini 文件或启动选项。 Bootcfg 包含在 \\ WINDOWS XP 和 Windows Server 2003 中的% Systemroot% System32 目录中。 在 EFI NVRAM 中存储启动选项的系统上，Bootcfg 显示 (略有不同，但命令相同。 ) 

您可以使用 Bootcfg 来添加、删除和更改所有有效启动选项的值;但是，不能设置无限超时值。 你还可以在脚本或批处理文件中使用 Bootcfg 命令来设置启动选项或在替换或升级操作系统后重置这些选项。

在 EFI NVRAM 中存储启动选项的系统上，Bootcfg 还可以显示启动分区表、添加镜像驱动器的启动条目，以及更新系统分区的 Guid。

您必须是计算机上 Administrators 组的成员才能使用 Bootcfg。 有关使用 Bootcfg 的详细说明，请参阅帮助和支持中心。

## <a name="nvrboot"></a>Nvrboot

Nvrboot (Nvrboot) 是 Windows XP 64 位版本和64位版本的 Windows Server 2003 中包含的基于 EFI 的启动项编辑器。 Nvrboot 在 EFI 环境中运行。 操作系统正在运行时，无法运行 Nvrboot。

Nvrboot 仅编辑启动条目。 你不能使用它显示或更改启动菜单的超时值，不过，你可以使用 **push** 命令 (**Nvrboot p**) 来更改默认启动项。

Nvrboot 还包括用于导出启动项的备份副本以及将启动项的备份副本导入到 NVRAM 的命令。 此过程在 EFI 部分的 [备份启动选项](backing-up-boot-options-in-efi.md) 中进行了讨论。

Nvrboot 以用户友好的格式显示启动选项。 例如，它将操作系统文件路径和启动加载程序文件路径显示为分区 GUID 后跟 Windows 目录路径。

以下过程介绍了如何从 EFI shell 启动 Nvrboot，它是随多个基于 Itanium 的系统一起提供的工具。 因为 EFI shell 工具因制造商而异，所以本部分中的说明可能无法准确描述特定计算机上的 EFI shell 接口。

**运行 Nvrboot**

1.  重新启动计算机。

2.  从 " **启动** " 菜单中，选择 " **EFI Shell**"。

3.  在 shell 提示符下，键入系统分区的驱动器号或文件系统号，例如 C：或 **FS** n，其中 n 是系统分区的文件系统号。

4.  键入 **cd msutil** ，导航到 nvrboot 所在的 msutil 目录。

5.  若要启动 Nvrboot，请键入 **Nvrboot**。

若要查找 Nvrboot 的说明，请键入 **h**。
