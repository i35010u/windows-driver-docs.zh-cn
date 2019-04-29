---
title: 使用 INF 文件安装文件系统筛选器驱动程序
description: 使用 INF 文件安装文件系统筛选器驱动程序
ms.assetid: 0bc70cdb-d115-4329-9fcc-a085a57c5f78
keywords:
- INF 文件 WDK 文件系统、 安装步骤
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c72c415bcdf1a5651968b26392ad11a3d68346a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384660"
---
# <a name="using-an-inf-file-to-install-a-file-system-filter-driver"></a>使用 INF 文件安装文件系统筛选器驱动程序


## <span id="ddk_using_an_inf_file_to_install_a_file_system_filter_driver_if"></span><span id="DDK_USING_AN_INF_FILE_TO_INSTALL_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


您创建了一个 INF 文件后，可以使用它来安装、 升级和卸载你文件系统筛选器驱动程序。 可以单独或一起批处理文件或用户模式下安装应用程序使用 INF 文件。

### <a name="span-idright-clickinstallspanspan-idright-clickinstallspanspan-idright-clickinstallspanright-click-install"></a><span id="Right-Click_Install"></span><span id="right-click_install"></span><span id="RIGHT-CLICK_INSTALL"></span>右键单击安装

若要执行[ **DefaultInstall** ](https://msdn.microsoft.com/library/windows/hardware/ff547356)并[ **DefaultInstall.Services** ](https://msdn.microsoft.com/library/windows/hardware/ff547360)部分的 INF 文件中，您应执行以下操作：

1.  在 Windows 资源管理器中，右键单击的 INF 文件的名称。 将显示快捷菜单。

2.  单击“安装” 。

**请注意**  仅当 INF 文件包含，将出现快捷菜单**DefaultInstall**部分。

 

### <a name="span-idcommand-lineorbatchfileinstallspanspan-idcommand-lineorbatchfileinstallspanspan-idcommand-lineorbatchfileinstallspancommand-line-or-batch-file-install"></a><span id="Command-Line_or_Batch_File_Install"></span><span id="command-line_or_batch_file_install"></span><span id="COMMAND-LINE_OR_BATCH_FILE_INSTALL"></span>命令行或批处理文件安装

若要执行**DefaultInstall**并**DefaultInstall.Services** INF 文件在命令行上或通过使用批处理文件安装的部分在命令提示符下键入以下命令或创建并运行批处理文件，其中包含此命令：

```cpp
RUNDLL32.EXE SETUPAPI.DLL,InstallHinfSection DefaultInstall 132 path-to-inf\infname.inf
```

工具和安装程序和系统管理中所述"Rundll32"和"InstallHinfSection"部分，分别，Microsoft Windows SDK 文档。

### <a name="span-idsetupapplicationspanspan-idsetupapplicationspanspan-idsetupapplicationspansetup-application"></a><span id="Setup_Application"></span><span id="setup_application"></span><span id="SETUP_APPLICATION"></span>安装应用程序

[**InstallHinfSection** ](https://msdn.microsoft.com/library/windows/desktop/aa376957)也可以调用此从安装程序应用程序，如下面的代码示例中所示：

```cpp
InstallHinfSection(NULL,NULL,TEXT("DefaultInstall 132 path-to-inf\infname.inf"),0); 
```

如果使用安装程序应用程序来安装您的驱动程序，应遵守以下原则：

-   若要准备最终卸载，安装应用程序应将驱动程序 INF 文件复制到卸载目录。

-   如果在安装应用程序和驱动程序安装在用户模式应用程序，此应用程序应列出在添加或删除控制面板中的程序，以便用户可以在必要时卸载它。 应列出只有一项，它表示应用程序和驱动程序。

    有关如何列出你的应用程序中添加或删除程序的详细信息，Windows SDK 文档的安装程序和系统管理部分中看到"删除应用程序"。

-   安装应用程序应永远不会将驱动程序 INF 文件复制到 Windows INF 文件目录 (*%windir%\\INF*)。 安装程序 Api 自动复制那里的文件作为的一部分[ **InstallHinfSection** ](https://msdn.microsoft.com/library/windows/desktop/aa376957)调用。

有关安装应用程序的详细信息，请参阅[编写设备安装应用程序](https://msdn.microsoft.com/library/windows/hardware/ff554015)。

 

 




