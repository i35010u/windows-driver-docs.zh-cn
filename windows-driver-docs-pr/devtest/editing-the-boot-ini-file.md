---
title: 编辑 Boot.ini 文件
description: 在 Windows Vista 之前运行 Windows 的基于 BIOS 的计算机将启动选项存储在 Boot.ini 文本文件。
ms.assetid: 9edbbd5e-36b5-4a80-925d-a007a4469984
keywords:
- Bootcfg 工具
- Boot.ini 文件 WDK，编辑
- 编辑启动选项
- 记事本 WDK 启动选项
- 文本编辑器 WDK 启动选项
- 手动编辑 WDK 启动选项
- 启动入口参数 WDK
- 引导参数 WDK
- 无限期启动超时值 WDK
- 启动 WDK 的超时值
- 超时 WDK 启动选项
- Boot.ini 文件 WDK，属性删除
- 删除 Boot.ini 属性
- 查看启动选项
- Boot.ini 文件 WDK、 查看
- 编辑器 WDK 启动选项
- 启动选项 WDK，编辑
ms.date: 07/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8db413aeebdde2e1c135717876544e0147ef6d9c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344857"
---
# <a name="editing-the-bootini-file"></a>编辑 Boot.ini 文件


> [!IMPORTANT] 
> 本主题介绍支持 Windows XP 和 Windows Server 2003 中的启动选项。 如果要更改的最新版本的 Windows 启动选项，请参阅[Windows Vista 和更高版本中的启动选项](boot-options-in-windows-vista-and-later.md)。

在 Windows Vista 之前运行 Windows 的基于 BIOS 的计算机将启动选项存储在 Boot.ini 文本文件。 您可以编辑使用 Bootcfg Boot.ini (`bootcfg.exe`)，这个工具包含在 Windows XP 和 Windows Server 2003，也可以使用诸如记事本之类的文本编辑器。 Bootcfg 记录在 Windows 帮助和支持。 您还可以查看和更改系统下的控制面板中的某些启动选项。 在系统属性对话框高级选项卡上，单击下的设置**启动和恢复**。 此功能会受到限制，因为它不是在本部分中讨论。 璝惠**启动和恢复**对话框框中，请参阅帮助和支持中心。

## <a name="bootcfg"></a>Bootcfg

Bootcfg 是一个命令行工具，可以编辑本地和远程计算机上的启动选项。 使用相同的 Bootcfg 命令和过程，可以编辑 Boot.ini，以及可扩展固件接口非易失性随机存取内存 (EFI NVRAM) 中的启动选项。 中包含 Bootcfg`%Systemroot%\\System32`目录中 Windows XP 和 Windows Server 2003。 （Bootcfg 显示的内容存储在 EFI NVRAM 中的启动选项的系统上略有不同，但命令是相同）。

Bootcfg 可用于添加、 删除和更改所有引导条目参数和启动选项;但是，您不能使用它将无限期启动超时值。 此外可以使用 Bootcfg 命令脚本或批处理文件中设置启动选项或重置密码后替换或升级操作系统。

与手动编辑 Bootcfg 编辑启动选项而无需更改 Boot.ini 的保护性属性。 它还可帮助您避免键入错误，可能会阻止在操作系统启动。

您必须使用 Bootcfg 的计算机上的管理员组的成员。 有关使用 Bootcfg 详细说明，请参阅帮助和支持中心。

## <a name="editing-in-notepad"></a>在记事本中编辑

您可以使用文本编辑器，（如记事本） 编辑 Boot.ini。 但是，此方法很容易出现错误，因为它仅当使用 Bootcfg 不可用。

在编辑 Boot.ini，必须删除 Windows 使用来保护该文件进行意外的更改的文件属性。 当 Boot.ini NTFS 卷上时，你必须在计算机上管理员组，若要更改其属性的成员。

使用以下过程来准备要进行手动编辑 Boot.ini。 此过程将删除系统、 文件隐藏，和只读属性。

**若要配置以进行编辑的 Boot.ini 属性**

1.  打开**Windows 命令提示符下**。 

2.  导航到系统卷的根目录。

3.  在命令行键入以下文本：

    ```
    attrib -s -h -r Boot.ini
    ```

    从文件中删除隐藏、 系统和只读属性。
    
4.  在记事本中打开该文件进行编辑。 由于是在 Windows 命令提示符下，以下命令都可以快速达到目的：

    ```
    notepad.exe Boot.ini
    ```

5.  在编辑完成后，可以还原文件属性来保护 Boot.ini。 但是，Ntldr 可以设置任何特性使用 Boot.ini。 若要还原的属性，请在 Windows 命令提示符下键入以下内容：

    ```
    attrib +s +h +r Boot.ini
    ```

    这将还原保护 Boot.ini 文件的属性。
