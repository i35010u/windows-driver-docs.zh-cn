---
title: 编辑 Boot.ini 文件
description: 在 Windows Vista 之前，在 Boot.ini 文本文件中运行 Windows 应用商店启动选项的基于 BIOS 的计算机。
ms.assetid: 9edbbd5e-36b5-4a80-925d-a007a4469984
keywords:
- Bootcfg 工具
- Boot.ini 文件 WDK，编辑
- 编辑启动选项
- 记事本 WDK 启动选项
- 文本编辑器 WDK 启动选项
- 手动编辑 WDK 启动选项
- 启动项参数 WDK
- 启动参数 WDK
- 无限启动超时值 WDK
- 启动超时值 WDK
- 超时 WDK 启动选项
- Boot.ini 文件 WDK，属性删除
- 删除 Boot.ini 特性
- 查看启动选项
- Boot.ini 文件 WDK，查看
- 编辑器 WDK 启动选项
- 启动选项 WDK，编辑
ms.date: 07/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7378a002cb5c37e9aed8e8624d2433e3dec26c5b
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383245"
---
# <a name="editing-the-bootini-file"></a>编辑 Boot.ini 文件


> [!IMPORTANT] 
> 本主题介绍 Windows XP 和 Windows Server 2003 中支持的启动选项。 如果要更改 Windows 的新式版本的启动选项，请参阅 [Windows Vista 和更高版本中的启动选项](./boot-options-in-windows.md)。

在 Windows Vista 之前，在 Boot.ini 文本文件中运行 Windows 应用商店启动选项的基于 BIOS 的计算机。 您可以使用 Bootcfg (`bootcfg.exe`) 、WINDOWS XP 和 Windows Server 2003 中包含的工具或使用记事本之类的文本编辑器来编辑 Boot.ini。 Windows 帮助和支持中介绍了 Bootcfg。 你还可以在 "系统" 下的 "控制面板" 中查看和更改某些启动选项。 在 "系统属性" 对话框中的 "高级" 选项卡上，选择 " **启动和恢复**" 下的设置。 由于此功能有限，本部分未对此进行讨论。 有关 " **启动和恢复** " 对话框的信息，请参阅帮助和支持中心。

## <a name="bootcfg"></a>Bootcfg

Bootcfg 是一个命令行工具，可在本地和远程计算机上编辑启动选项。 使用相同的 Bootcfg 命令和过程，你可以在可扩展固件接口的非易失性随机存取内存中编辑 Boot.ini，以及 (EFI NVRAM) 的启动选项。 Bootcfg 包含在 `%Systemroot%\\System32` WINDOWS XP 和 Windows Server 2003 中的目录中。 在 EFI NVRAM 中存储启动选项的系统上，Bootcfg 显示 (略有不同，但命令相同。 ) 

您可以使用 Bootcfg 来添加、删除和更改所有启动项参数和启动选项;但是，不能使用它来设置无限启动超时值。 你还可以在脚本或批处理文件中使用 Bootcfg 命令来设置启动选项或在替换或升级操作系统后重置这些选项。

与手动编辑不同，Bootcfg 会编辑启动选项，而无需更改 Boot.ini 上的保护属性。 它还可帮助你避免键入可能会阻止操作系统启动的错误。

您必须是计算机上 Administrators 组的成员才能使用 Bootcfg。 有关使用 Bootcfg 的详细说明，请参阅帮助和支持中心。

## <a name="editing-in-notepad"></a>在记事本中编辑

可以使用文本编辑器（如记事本）编辑 Boot.ini。 但是，因为此方法容易出错，所以仅当 Bootcfg 不可用时才使用它。

在编辑 Boot.ini 之前，必须删除 Windows 用于保护文件免遭意外更改的文件属性。 当 Boot.ini 在 NTFS 卷上时，您必须是计算机上 Administrators 组的成员才能更改其属性。

使用以下过程为手动编辑准备 Boot.ini。 此过程将删除文件的系统、隐藏和只读属性。

**配置 Boot.ini 特性以进行编辑**

1.  打开 **Windows 命令提示符**。 

2.  导航到系统卷的根目录。

3.  在命令行中键入以下文本：

    ```
    attrib -s -h -r Boot.ini
    ```

    将从文件中删除 "系统"、"隐藏" 和 "只读" 属性。
    
4.  在记事本中打开文件进行编辑。 由于你在 Windows 命令提示符下，因此以下命令应快速完成此技巧：

    ```
    notepad.exe Boot.ini
    ```

5.  完成编辑后，可以还原文件属性以保护 Boot.ini。 但是，Ntldr 可以将 Boot.ini 与任何属性集一起使用。 若要还原属性，请在 Windows 命令提示符下键入以下命令：

    ```
    attrib +s +h +r Boot.ini
    ```

    这会还原保护 Boot.ini 文件的属性。