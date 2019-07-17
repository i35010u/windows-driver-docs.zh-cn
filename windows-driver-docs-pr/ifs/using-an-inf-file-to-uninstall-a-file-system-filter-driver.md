---
title: 使用 INF 文件卸载文件系统筛选器驱动程序
description: 使用 INF 文件卸载文件系统筛选器驱动程序
ms.assetid: e41deb65-7977-479c-ac42-c550aa6a3f1b
keywords:
- INF 文件 WDK 文件系统，卸载筛选器驱动程序
- 卸载筛选器驱动程序 WDK 文件系统
ms.date: 07/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 53511f98d83a7859e5f05769f287e0e90c46232f
ms.sourcegitcommit: 6790f79bafb69c53e655b40810e24a11081e5038
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68270228"
---
# <a name="using-an-inf-file-to-uninstall-a-file-system-filter-driver"></a>使用 INF 文件卸载文件系统筛选器驱动程序

您可以通过使用命令行、 PowerShell，以及批处理文件中，一个 INF 文件卸载您的驱动程序或用户模式下卸载应用程序。

没有"右键单击卸载"选项。

## <a name="command-line-or-batch-file-uninstall"></a>命令行或批处理文件卸载

若要执行**DefaultUninstall**并**DefaultUninstall.Services**节的命令行上的 INF 文件在命令提示符下键入以下命令或创建并运行批处理文件包含此命令：

'' 命令行 RUNDLL32。EXE 安装程序 API。DLL，InstallHinfSection DefaultUninstall 132 路径-到-卸载-dir\infname.inf
```

**Rundll32** and **InstallHinfSection** are described in the Tools and Setup and System Administration sections, respectively, of the Microsoft Windows SDK documentation.

## Powershell Uninstall

Type the following command at the Powershell command prompt:

```PowerShell
Get-CimInstance Win32_SystemDriver -Filter "name='your_driver_name'" | Invoke-CimMethod -MethodName Delete
```

## <a name="uninstall-application"></a>卸载应用程序

此外可以执行**DefaultUninstall**并**DefaultUninstall.Services**部分你 INF 文件卸载应用程序，如下面的代码示例中所示：

```cpp
InstallHinfSection(NULL,NULL,TEXT("DefaultUninstall 132 path-to-uninstall-dir\infname.inf"),0);
```

如果您使用应用程序以卸载您的驱动程序，应遵守以下原则：

* 若要准备最终卸载，安装应用程序应将驱动程序 INF 文件复制到卸载目录。
* 在中**DefaultUninstall.Services** INF 文件的部分**DelService**指令应始终指定 0x200 (SPSVCINST\_STOPSERVICE) 标志时才停止服务已删除。
* 如果在用户模式应用程序安装的驱动程序，此应用程序应列出添加或删除控制面板中的程序中，以便用户可以在必要时卸载它。 应列出只有一项，它表示应用程序和驱动程序。 有关如何列出你的应用程序中添加或删除程序的详细信息，Microsoft Windows SDK 文档的安装程序和系统管理部分中看到"删除应用程序"。
* 卸载应用程序不应删除的 INF 文件 （或其关联的 PNF 文件） 从 Windows INF 文件目录 ( *%windir%\\INF*)。
* 卸载应用程序时，不能安全地删除一些筛选器驱动程序文件。 这些文件不应列入**DefaultUninstall.Services** INF 文件部分。

有关详细信息卸载应用程序，请参阅[编写设备安装应用程序](https://docs.microsoft.com/windows-hardware/drivers/install/writing-a-device-installation-application)。
