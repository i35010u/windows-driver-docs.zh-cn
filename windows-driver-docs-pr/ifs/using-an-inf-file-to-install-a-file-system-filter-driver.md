---
title: 使用 INF 文件安装文件系统筛选器驱动程序
description: 使用 INF 文件安装文件系统筛选器驱动程序
keywords:
- INF 文件系统和安装步骤
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a210ceff479af62e555ee3b5c567d5b89f9b65af
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841123"
---
# <a name="using-an-inf-file-to-install-a-file-system-filter-driver"></a>使用 INF 文件安装文件系统筛选器驱动程序


## <span id="ddk_using_an_inf_file_to_install_a_file_system_filter_driver_if"></span><span id="DDK_USING_AN_INF_FILE_TO_INSTALL_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


创建 INF 文件后，可以使用它来安装、升级和卸载文件系统筛选器驱动程序。 您可以单独使用 INF 文件，或将其与批处理文件或用户模式安装应用程序一起使用。

### <a name="span-idright-click_installspanspan-idright-click_installspanspan-idright-click_installspanright-click-install"></a><span id="Right-Click_Install"></span><span id="right-click_install"></span><span id="RIGHT-CLICK_INSTALL"></span>右键单击 "安装"

若要执行 INF 文件的 [**DefaultInstall**](../install/inf-defaultinstall-section.md) 和 [**DefaultInstall**](../install/inf-defaultinstall-services-section.md) 部分，应执行以下操作：

1.  在 Windows 资源管理器中，选择并按住 (或右键单击) INF 文件名。 将显示一个快捷菜单。

2.  选择“安装”。

**注意**   仅当 INF 文件包含 **DefaultInstall** 部分时，才会显示快捷菜单。

 

### <a name="span-idcommand-line_or_batch_file_installspanspan-idcommand-line_or_batch_file_installspanspan-idcommand-line_or_batch_file_installspancommand-line-or-batch-file-install"></a><span id="Command-Line_or_Batch_File_Install"></span><span id="command-line_or_batch_file_install"></span><span id="COMMAND-LINE_OR_BATCH_FILE_INSTALL"></span>命令行或批处理文件安装

若要在命令行上执行 INF 文件的 **DefaultInstall** 和 **DefaultInstall** 部分或使用批处理文件安装，请在命令提示符下键入以下命令，或创建并运行包含此命令的批处理文件：

```cpp
RUNDLL32.EXE SETUPAPI.DLL,InstallHinfSection DefaultInstall 132 path-to-inf\infname.inf
```

"Rundll32.exe" 和 "InstallHinfSection" 分别在 Microsoft Windows SDK 文档的 "工具" 和 "设置" 和 "系统管理" 部分中进行了介绍。

### <a name="span-idsetup_applicationspanspan-idsetup_applicationspanspan-idsetup_applicationspansetup-application"></a><span id="Setup_Application"></span><span id="setup_application"></span><span id="SETUP_APPLICATION"></span>安装应用程序

[**InstallHinfSection**](/windows/win32/api/setupapi/nf-setupapi-installhinfsectiona) 也可以从安装应用程序调用，如下面的代码示例所示：

```cpp
InstallHinfSection(NULL,NULL,TEXT("DefaultInstall 132 path-to-inf\infname.inf"),0); 
```

如果使用安装应用程序来安装驱动程序，请遵循以下准则：

-   若要准备最终卸载，安装应用程序应将驱动程序 INF 文件复制到卸载目录。

-   如果安装应用程序使用驱动程序安装用户模式应用程序，则应在 "控制面板" 的 "添加或删除程序" 中列出此应用程序，以便用户可以在需要时将其卸载。 只应列出一项，表示应用程序和驱动程序。

    有关如何在 "添加或删除程序" 中列出应用程序的详细信息，请参阅 Windows SDK 文档的 "设置和系统管理" 部分中的 "删除应用程序"。

-   安装程序不应将驱动程序 INF 文件复制到 Windows INF 文件目录 (*% windir% \\ INF*) 。 Setupapi.log 会在 [**InstallHinfSection**](/windows/win32/api/setupapi/nf-setupapi-installhinfsectiona) 调用中自动复制其中的文件。

有关安装应用程序的详细信息，请参阅 [编写设备安装应用程序](../install/writing-a-device-installation-application.md)。

 

