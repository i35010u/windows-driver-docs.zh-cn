---
title: 使用 INF 文件卸载文件系统筛选器驱动程序
description: 使用 INF 文件卸载文件系统筛选器驱动程序
ms.assetid: e41deb65-7977-479c-ac42-c550aa6a3f1b
keywords:
- INF 文件系统, 卸载筛选器驱动程序
- 卸载筛选器驱动程序 WDK 文件系统
ms.date: 07/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 53511f98d83a7859e5f05769f287e0e90c46232f
ms.sourcegitcommit: f89a978ee23b9d2f925b13ea56b2c6cd48b4603a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2019
ms.locfileid: "68270228"
---
# <a name="using-an-inf-file-to-uninstall-a-file-system-filter-driver"></a>使用 INF 文件卸载文件系统筛选器驱动程序

可以通过使用命令行 PowerShell、INF 文件以及批处理文件或用户模式卸载应用程序来卸载驱动程序。

没有 "右键单击卸载" 选项。

## <a name="command-line-or-batch-file-uninstall"></a>命令行或批处理文件卸载

若要在命令行上执行 INF 文件的**DefaultUninstall**和**DefaultUninstall**部分, 请在命令提示符下键入以下命令, 或创建并运行包含以下命令的批处理文件:

```Command Line
RUNDLL32.EXE SETUPAPI.DLL,InstallHinfSection DefaultUninstall 132 path-to-uninstall-dir\infname.inf
```

Microsoft Windows SDK 文档的 "工具" 和 "设置" 和 "系统管理" 部分分别介绍了**rundll32.exe**和**InstallHinfSection** 。

## <a name="powershell-uninstall"></a>Powershell 卸载

在 Powershell 命令提示符下键入以下命令:

```PowerShell
Get-CimInstance Win32_SystemDriver -Filter "name='your_driver_name'" | Invoke-CimMethod -MethodName Delete
```

## <a name="uninstall-application"></a>卸载应用程序

你还可以从卸载应用程序执行 INF 文件的**DefaultUninstall**和**DefaultUninstall**部分, 如以下代码示例所示:

```cpp
InstallHinfSection(NULL,NULL,TEXT("DefaultUninstall 132 path-to-uninstall-dir\infname.inf"),0);
```

如果使用应用程序卸载驱动程序, 请遵循以下准则:

* 若要准备最终卸载, 安装应用程序应将驱动程序 INF 文件复制到卸载目录。
* 在 INF 文件的**DefaultUninstall**节中, **DelService**指令应始终指定 0x200 (SPSVCINST\_STOPSERVICE) 标志来停止服务, 然后再将其删除。
* 如果用户模式应用程序是使用驱动程序安装的, 则此应用程序应该列在 "控制面板" 的 "添加或删除程序" 中, 以便用户可以在需要时将其卸载。 只应列出一项, 表示应用程序和驱动程序。 有关如何在 "添加或删除程序" 中列出应用程序的详细信息, 请参阅 Microsoft Windows SDK 文档的 "设置和系统管理" 部分中的 "删除应用程序"。
* 卸载应用程序不应从 Windows inf 文件目录 ( *% windir%\\INF*) 中删除 INF 文件 (或其关联的 PNF 文件)。
* 卸载应用程序时, 不能安全地删除某些筛选器驱动程序文件。 不应在 INF 文件的**DefaultUninstall**节中列出这些文件。

有关卸载应用程序的详细信息, 请参阅[编写设备安装应用程序](https://docs.microsoft.com/windows-hardware/drivers/install/writing-a-device-installation-application)。
