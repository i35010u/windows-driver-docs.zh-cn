---
title: 使用 UMDF 辅助安装程序
description: 使用 UMDF 辅助安装程序
ms.assetid: e5ec2122-1602-487b-baad-4a3d9e47cf58
keywords:
- UMDF 共同安装程序 WDK
- 共同安装程序 WDK UMDF
- 共同安装程序部分 WDK UMDF
- 可配置共同安装程序 WDK UMDF
- 系统提供 UMDF 共同安装程序 WDK UMDF
- 可再发行组件共同安装程序 WDK UMDF
- 更新共同安装程序 WDK UMDF
- INF 文件 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 264d49d80852a5635ed6fd8bac37e55034f28e32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391829"
---
# <a name="using-the-umdf-co-installer"></a>使用 UMDF 辅助安装程序


辅助安装程序更新存储在计算机上的 framework 版本，并处理特定于框架的 INF 文件部分。 本主题介绍两种 UMDF 共同安装程序以及何时需要包括一个具有您[驱动程序安装包](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_package)或引用 INF 文件中的共同安装程序。

## <a name="getting-the-co-installer-package"></a>获取辅助安装程序包


在 Windows 8.1 中 Microsoft 提供的可再发行框架更新作为一部分包括在内的 Windows Driver Kit (WDK)。

有关辅助安装程序目录的内容的完整列表，请参阅[KMDF 驱动程序的安装组件](installation-components-for-kmdf-drivers.md)。

辅助安装程序目录包含的其他组件之间*更新共同安装程序*，调用 WUDFUpdate\_*MMmmm*.dll，其中*MM*依次为主版本号版本号，并*mmm*是次版本号。

更新共同安装程序更新的计算机上的 UMDF framework 版本。 例如，如果计算机具有 UMDF 1.9 版，辅助安装程序包含版本 1.11 共同安装程序更新计算机的 framework 版本为 1.11。

操作系统包括另一个共同安装程序中，调用*配置辅助安装程序*，或 WudfCoinstaller.dll。 配置辅助安装程序处理驱动程序的 INF 文件的特定于 UMDF 的部分，并会对注册表进行任何必要的更新。

## <a name="referencing-co-installers-from-your-inf-file"></a>引用共同安装程序的 INF 文件


如果要为 Windows 8.1 编写 UMDF 2.0 驱动程序，您的 INF 文件必须引用配置共同安装程序。 由于配置共同安装程序包括在操作系统中，您不需要将其重新分发。

如果你正在编写使用您的驱动程序的计算机上安装了 Windows 8.1 之前的目标操作系统，必须确保该版本 1.11 framework UMDF 1.11 驱动程序。 以下是三种方法可以执行此操作：

-   引用在 INF 文件中，更新共同安装程序并包括更新共同安装程序中的您[驱动程序安装包](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_package)。 在操作系统安装您的驱动程序，它将运行辅助安装程序。 如果将通过 Windows Update 分发驱动程序，必须选择此选项。

-   重新分发的相关 MSU 包 (例如 umdf-1.11-Win-6.0.msu) 以及调用它的安装程序应用程序。 您可以找到这样的应用程序的示例中的 src\\常规\\WDK 安装 wdkinstall 子目录。 如果你正在编写附带了设备，并且必须运行才可使用设备的安装程序，可以选择此选项。 如果选择此选项，您的 INF 文件必须引用配置共同安装程序。

-   依赖于 Windows 更新，以便使用您的驱动程序的计算机上安装所需的框架版本。 从版本 1.11 的 framework 开始，通过 Windows Update 分发 UMDF 的新版本。 如果选择此选项，您的 INF 文件必须引用配置共同安装程序。

在 INF 文件中，必须始终引用更新共同安装程序或配置辅助安装程序。 但是，引用 INF 中的这两个共同安装程序将导致安装错误。

## <a name="inf-file-sections-for-the-co-installer"></a>辅助安装程序的 INF 文件部分


驱动程序的 INF 文件必须包括[ **INF DDInstall.CoInstallers 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547321)。 如果你重新分发更新共同安装程序中，你**DDInstall.CoInstallers**部分必须同时包含[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)和[ **INF CopyFiles 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546346)，如下面的示例所示。

```cpp
[MyDriver_Install.CoInstallers]
AddReg = MyDriver_Install.CoInstallers_AddReg
CopyFiles = MyDriver_CoInstallers_CopyFiles
```

INF **AddReg**指令标识创建一个 INF 部分**CoInstallers32**注册表项。

```cpp
[MyDriver_Install.CoInstallers_AddReg]
HKR,,CoInstallers32,0x00010000,"WudfUpdate_01011.dll"
```

INF **CopyFiles**指令标识将从安装设备的共同安装程序复制到系统设备 INF 部分。

```cpp
[MyDriver_CoInstallers_CopyFiles]
WudfUpdate_01011.dll
```

如果你重新分发的 MSU 包，你**DDInstall.CoInstallers**部分必须指定**AddReg**指令，它引用配置共同安装程序。

```cpp
[Echo_Install.NT.CoInstallers]
AddReg=CoInstallers_AddReg
[CoInstaller.AddReg]
HKR,,CoInstallers32,0x00010000,WudfCoinstaller.dll
```

驱动程序的 INF 文件必须始终包含**DDInstall.Wdf**部分共同安装程序，读取后已安装。 为您的驱动程序可以在中指定的指令的信息**DDInstall.Wdf**，请参阅[INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)。

您可以避免使用 INX 文件创建多个版本的 framework 的多个 INF 文件和[Stampinf](https://msdn.microsoft.com/library/windows/hardware/ff552786)工具。 有关 INX 文件的详细信息，请参阅[使用 INX 文件转换为创建 INF 文件](using-inx-files-to-create-inf-files.md)。

 

 





