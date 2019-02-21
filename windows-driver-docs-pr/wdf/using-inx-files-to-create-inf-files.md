---
title: 使用 INX 文件创建 INF 文件
description: 使用 INX 文件创建 INF 文件
ms.assetid: b49f8fed-c2b5-46e2-aeaf-e09231fa1578
keywords:
- INX 文件 WDK KMDF
- 生成实用工具 WDK KMDF
- Stampinf WDK KMDF
- KMDF WDK，INX 文件
- 内核模式驱动程序框架 WDK INX 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 469dd5eb5d5d463b4296e2ba8c7d3ee4c2a46461
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526999"
---
# <a name="using-inx-files-to-create-inf-files"></a>使用 INX 文件创建 INF 文件


*INX 文件*是一个 INF 文件，包含表示版本信息的字符串变量。 生成过程生成您的驱动程序使用 Microsoft Visual Studio 时，运行[Stampinf](https://msdn.microsoft.com/library/windows/hardware/ff552786)工具来替换的字符串变量中 INX 文件与表示特定硬件体系结构或 framework 版本的文本字符串。 您也可以手动运行 Stampinf 工具，它位于*bin* WDK 的子目录。

如果为您的驱动程序创建 INX 文件，您无需维护多个特定于版本的 INF 文件。 相反，您可以创建单个 INX 文件并使用 Visual Studio 或 Stampinf 在需要时生成特定于版本的 INF 文件。

若要修改 Stampinf 属性在 Visual Studio 中的，打开您的驱动程序的包项目属性页。 右键单击解决方案资源管理器中的包项目并选择**属性**。 在包的属性页中，单击**配置属性**，然后**StampInf**。

您也可以手动运行 Stampinf 工具，它位于*bin* WDK 的子目录。

WDK 包括用于所有的 KMDF 和 UMDF 示例驱动程序 INX 文件。

INX 文件可以包含以下字符串变量：

<a href="" id="-arch-"></a>$ARCH $  
Stampinf 此变量替换为特定于体系结构的字符串。 例如，如果您使用的 x86 生成环境中，工具将替换 $ARCH$ 具有"x86"。 需要指定特定的体系结构中的 INF 文件，如内的任何位置，可以使用 $ARCH$ 字符串[ **INF 制造商部分**](https://msdn.microsoft.com/library/windows/hardware/ff547454)，按如下所示：

```cpp
[Manufacturer]
%StdMfg%=Standard,NT$ARCH$
```

<a href="" id="-kmdfcoinstallerversion-"></a>$KMDFCOINSTALLERVERSION $  
如果您使用[Stampinf](https://msdn.microsoft.com/library/windows/hardware/ff552786)工具-*k*选项，Stampinf 替换此变量表示 KMDF 共同安装程序的特定版本的字符串。 中，如指定框架的 INF 文件中的辅助安装程序时，可以使用 $KMDFCOINSTALLERVERSION$ 变量[ **INF DDInstall.CoInstallers 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547321)，按如下所示：

```cpp
[ECHO_Device.NT.CoInstallers]
AddReg=ECHO_Device_CoInstaller_AddReg
CopyFiles=ECHO_Device_CoInstaller_CopyFiles

[ECHO_Device_CoInstaller_AddReg]
HKR,,CoInstallers32,0x00010000, "WdfCoInstaller$KMDFCOINSTALLERVERSION$.dll,WdfCoInstaller"

[ECHO_Device_CoInstaller_CopyFiles]
WdfCoInstaller$KMDFCOINSTALLERVERSION$.dll
```

<a href="" id="-kmdfversion-"></a>$KMDFVERSION $  
如果您设置**KMDF 版本号**Visual Studio 中的属性 (或使用[Stampinf](https://msdn.microsoft.com/library/windows/hardware/ff552786)工具-*k*选项)，Stampinf 替换一个字符串，表示此变量KMDF 特定版本。 指定在 INF 文件中，例如当您指定的框架的版本时，可以使用 $KMDFVERSION$ 变量[KmdfLibraryVersion](installing-the-framework-s-co-installer.md)指令，如下所示：

```cpp
KmdfLibraryVersion = $KMDFVERSION$
```

<a href="" id="-umdfcoinstallerversion-"></a>$UMDFCOINSTALLERVERSION $  
```cpp
[SourceDisksFiles]
WudfUpdate_$UMDFCOINSTALLERVERSION$.dll=1

[CoInstallers_CopyFiles]
WudfUpdate_$UMDFCOINSTALLERVERSION$.dll

[CoInstallers_AddReg]
HKR,,CoInstallers32,0x00010000,"WUDFUpdate_$UMDFCOINSTALLERVERSION$.dll"
```

<a href="" id="-umdfversion-"></a>$UMDFVERSION $  
```cpp
[UMDFYourDriver_Install]
UmdfLibraryVersion=$UMDFVERSION$
```

[Stampinf](https://msdn.microsoft.com/library/windows/hardware/ff552786)还支持-*u*选项替换 UMDF INX 文件中的字符串变量。 如果驱动程序包中包含基于 UMDF 驱动程序和基于 KMDF 驱动程序，可以使用-*k*和-*u*与单个 Stampinf 命令和一个 INX 文件的选项。

 

 





