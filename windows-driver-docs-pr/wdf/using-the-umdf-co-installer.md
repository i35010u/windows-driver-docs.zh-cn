---
title: 使用 UMDF 辅助安装程序
description: 使用 UMDF 辅助安装程序
keywords:
- UMDF coinstallers WDK
- coinstallers WDK UMDF
- CoInstallers 部分 WDK UMDF
- 可配置的 coinstallers WDK UMDF
- 系统提供的 UMDF coinstallers WDK UMDF
- 可再发行 coinstallers WDK UMDF
- 更新 coinstallers WDK UMDF
- INF 文件 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9edd23c03c823e360b7e14042dfba1fdf652a2de
ms.sourcegitcommit: 76a7b604f13cf419ff21518337913820a703347f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2021
ms.locfileid: "104719498"
---
# <a name="using-the-umdf-co-installer"></a>使用 UMDF 辅助安装程序

> [!NOTE]
> 如果你的驱动程序仅面向 Windows 10，则无需重新分发 WDF 或在驱动程序包中提供 Coinstaller。 面向 Windows 10：
>1. 在 Visual Studio 的 "**项目设置**" 属性页的 "**驱动程序设置**  ->  **目标操作系统版本**" 下，选择 " **Windows 10 或更高** 版本"。  这等效于将以下内容添加到 .vcxproj 文件： 
>```xml
><PropertyGroup Label="Configuration">
><TargetVersion>Windows10</TargetVersion>
>```
>2. 在 " [INF 制造商" 部分](../install/inf-manufacturer-section.md)中，将10.0 指定为目标 OS 版本，如下所示：
>```inf
>[Manufacturer]
>%MyMfg% = MyMfg, NTamd64.10.0
>```
>
>你可能仍需要引用系统提供的 coinstaller，如下所示：
>
>```inf
>[Echo_Install.NT.CoInstallers] 
>AddReg=CoInstallers_AddReg
>
>[CoInstaller.AddReg]
>HKR,,CoInstallers32,0x00010000,WudfCoinstaller.dll
>```


共同安装程序会更新存储在计算机上的框架版本，并处理特定于框架的 INF 文件部分。 本主题介绍两个 UMDF 共同安装程序，以及何时需要将其包含在你的 [驱动程序安装包](/windows-hardware/drivers) 中，或者在 INF 文件中引用共同安装程序。

## <a name="getting-the-co-installer-package"></a>获取共同安装程序包


在 Windows 8.1 中，Microsoft 提供的可再发行框架更新作为 Windows 驱动程序工具包 (WDK) 的一部分包含在内。

有关共同安装程序目录内容的完整列表，请参阅 [KMDF 驱动程序的安装组件](installation-components-for-kmdf-drivers.md)。

在其他组件中，共同安装程序目录包含一个名为 WUDFUpdate 嗯的 *更新共同安装程序*， \_ 其中 *MM* 是主版本号， *mmm* 是次版本号。

更新共同安装程序会更新计算机上的 UMDF framework 版本。 例如，如果计算机具有 UMDF 版本1.9，并且共同安装程序包含版本1.11，则共同安装程序会将计算机的 framework 版本更新为1.11。

操作系统包括另一个共同安装程序（称为 *配置共同安装程序*）或 WudfCoinstaller.dll。 配置共同安装程序将处理驱动程序的 INF 文件的 UMDF 特定部分，并对注册表进行任何必要的更新。

## <a name="referencing-co-installers-from-your-inf-file"></a>从 INF 文件引用共同安装程序


如果要为 Windows 8.1 编写 UMDF 2.0 驱动程序，则 INF 文件必须引用配置共同安装程序。 由于操作系统中包含了配置共同安装程序，因此您无需重新分发它。

如果在 Windows 8.1 之前编写面向操作系统的 UMDF 1.11 驱动程序，则必须确保在使用驱动程序的计算机上安装 framework 的版本1.11。 下面是三种执行此操作的方法：

-   在 INF 文件中引用更新共同安装程序，并在 [驱动程序安装包](/windows-hardware/drivers)中包括更新共同安装程序。 当操作系统安装您的驱动程序时，它会运行共同安装程序。 如果你的驱动程序将通过 Windows 更新分发，则必须选择此选项。

-   重新分发相关的 MSU 包 (例如，1.11-Win-6.0) 连同调用它的安装程序。 可以在 \\ WDK 安装的 src general wdkinstall 子目录中找到此类应用程序的示例 \\ 。 如果要编写随设备一起提供的安装程序，则可以选择此选项，并且必须在使用设备之前运行。 如果选择此选项，则 INF 文件必须引用配置共同安装程序。

-   依靠 Windows 更新在使用驱动程序的计算机上安装所需的框架版本。 从 framework 版本1.11 开始，新版本的 UMDF 通过 Windows 更新分发。 如果选择此选项，则 INF 文件必须引用配置共同安装程序。

在 INF 文件中，必须始终引用 "更新共同安装程序" 或 "配置共同安装程序"。 但是，在 INF 中引用这两个共同安装程序将导致安装错误。

## <a name="inf-file-sections-for-the-co-installer"></a>共同安装程序的 INF 文件部分


驱动程序的 INF 文件必须包含 [**INF DDInstall. CoInstallers 部分**](../install/inf-ddinstall-coinstallers-section.md)。 如果重新分发更新共同安装程序，则 **DDInstall CoInstallers** 部分必须同时包含 [**inf AddReg 指令**](../install/inf-addreg-directive.md) 和 [**inf CopyFiles 指令**](../install/inf-copyfiles-directive.md)，如以下示例所示。

```cpp
[MyDriver_Install.CoInstallers]
AddReg = MyDriver_Install.CoInstallers_AddReg
CopyFiles = MyDriver_CoInstallers_CopyFiles
```

INF **AddReg** 指令标识创建 **CoInstallers32** 注册表项的 inf 部分。

```cpp
[MyDriver_Install.CoInstallers_AddReg]
HKR,,CoInstallers32,0x00010000,"WudfUpdate_01011.dll"
```

INF **CopyFiles** 指令标识将安装设备中的共同安装程序复制到系统设备的 inf 部分。

```cpp
[MyDriver_CoInstallers_CopyFiles]
WudfUpdate_01011.dll
```

如果重新分发 MSU 包，则 **DDInstall CoInstallers** 节必须指定一个引用配置共同安装程序的 **AddReg** 指令。

```cpp
[Echo_Install.NT.CoInstallers]
AddReg=CoInstallers_AddReg
[CoInstaller.AddReg]
HKR,,CoInstallers32,0x00010000,WudfCoinstaller.dll
```

驱动程序的 INF 文件必须始终包含共同安装程序在安装后读取的 **DDInstall 部分。** 有关驱动程序可在 **DDInstall** 中指定的指令的信息，请参阅 [在 INF 文件中指定 Wdf 指令](specifying-wdf-directives-in-inf-files.md)。

可以使用 INX 文件和 [Stampinf](../devtest/stampinf.md) 工具避免为多个版本的框架创建多个 INF 文件。 有关 INX 文件的详细信息，请参阅[使用 INX 文件创建 INF 文件](using-inx-files-to-create-inf-files.md)。

