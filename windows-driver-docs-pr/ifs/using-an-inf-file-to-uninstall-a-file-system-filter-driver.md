---
title: 使用 INF 文件卸载文件系统筛选器驱动程序
description: 描述卸载文件系统筛选器驱动程序的各种方法
keywords:
- INF 文件系统，卸载筛选器驱动程序
- 卸载筛选器驱动程序 WDK 文件系统
ms.date: 08/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7a29ed5ae0a95638561a6823662c14b9385552df
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841121"
---
# <a name="using-an-inf-file-to-uninstall-a-file-system-filter-driver"></a>使用 INF 文件卸载文件系统筛选器驱动程序

> [!NOTE]
>
> 从 Windows 10 版本1903开始， **DefaultUninstall** 和 **DefaultUninstall** INF 部分禁止 [ (例外)](../develop/creating-a-primitive-driver.md#legacy-compatibility)。

在1903版之前的 Windows 10 中， **DefaultUninstall** 和 **DefaultUninstall** 部分是可选的，但建议在卸载驱动程序时使用。 对于这些操作系统版本，你可以通过使用命令行、PowerShell 或批处理文件来卸载筛选器驱动程序，以执行这些 INF 文件部分或用户模式卸载应用程序。

没有 "右键单击卸载" 选项。

## <a name="command-line-or-batch-file-uninstall"></a>Command-Line 或批处理文件卸载

若要在命令行上执行 INF 文件的 **DefaultUninstall** 和 **DefaultUninstall** 部分，请在命令提示符下键入以下命令，或创建并运行包含以下命令的批处理文件：

```Command Line
RUNDLL32.EXE SETUPAPI.DLL,InstallHinfSection DefaultUninstall 132 path-to-uninstall-dir\infname.inf
```

有关详细信息，请参阅 [**rundll32.exe**](/windows-server/administration/windows-commands/rundll32) 和 [**InstallHinfSection**](/windows/win32/api/setupapi/nf-setupapi-installhinfsectiona) 。

## <a name="powershell-uninstall"></a>Powershell 卸载

在 Powershell 命令提示符下键入以下命令：

```PowerShell
Get-CimInstance Win32_SystemDriver -Filter "name='your_driver_name'" | Invoke-CimMethod -MethodName Delete
```

有关详细信息，请参阅 [CimCmdlets](/powershell/module/cimcmdlets/?view=powershell-7) 。

## <a name="uninstall-application"></a>卸载应用程序

你还可以从卸载应用程序执行 INF 文件的 **DefaultUninstall** 和 **DefaultUninstall** 部分，如以下代码示例所示：

```cpp
InstallHinfSection(NULL,NULL,TEXT("DefaultUninstall 132 path-to-uninstall-dir\infname.inf"),0);
```

如果使用应用程序卸载驱动程序，请遵循以下准则：

* 若要准备最终卸载，安装应用程序应将驱动程序 INF 文件复制到卸载目录。
* 在 INF 文件的 **DefaultUninstall** 节中， **DelService** 指令应始终指定 0x200 (SPSVCINST \_ STOPSERVICE) 标志，以便在服务删除之前将其停止。
* 如果用户模式应用程序是使用驱动程序安装的，则此应用程序应该列在 "控制面板" 的 "添加或删除程序" 中，以便用户可以在需要时将其卸载。 只应列出一项，表示应用程序和驱动程序。 有关如何在 "添加或删除程序" 中列出应用程序的详细信息，请参阅 Microsoft Windows SDK 文档的 "设置和系统管理" 部分中的 "删除应用程序"。
* 卸载应用程序不应从 Windows INF 文件目录 (*% windir% \\ INF*) 中删除 INF 文件 (或其关联的 PNF 文件) 。
* 卸载应用程序时，不能安全地删除某些筛选器驱动程序文件。 不应在 INF 文件的 **DefaultUninstall** 节中列出这些文件。

有关卸载应用程序的详细信息，请参阅 [编写设备安装应用程序](../install/writing-a-device-installation-application.md)。
