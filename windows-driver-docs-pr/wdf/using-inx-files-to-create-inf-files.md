---
title: 使用 INX 文件创建 INF 文件
description: 使用 INX 文件创建 INF 文件
ms.assetid: b49f8fed-c2b5-46e2-aeaf-e09231fa1578
keywords:
- INX 文件 WDK KMDF
- 生成实用工具 WDK KMDF
- Stampinf WDK KMDF
- KMDF WDK，INX 文件
- 内核模式驱动程序框架 WDK，INX 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bf772230b44f32610979f963d78e7ccc92d0d9f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191369"
---
# <a name="using-inx-files-to-create-inf-files"></a>使用 INX 文件创建 INF 文件


*INX 文件*是一个 INF 文件，其中包含表示版本信息的字符串变量。 使用 Microsoft Visual Studio 生成驱动程序时，生成过程将运行 [Stampinf](../devtest/stampinf.md) 工具，以将 INX 文件中的字符串变量替换为表示特定硬件体系结构或 framework 版本的文本字符串。 还可以手动运行 Stampinf 工具，该工具位于 WDK 的 *bin* 子目录中。

如果为驱动程序创建 INX 文件，则不必维护多个特定于版本的 INF 文件。 相反，你可以创建一个 INX 文件，并在需要时使用 Visual Studio 或 Stampinf 生成特定于版本的 INF 文件。

若要在 Visual Studio 中修改 Stampinf 属性，请打开驱动程序包项目的属性页。 在解决方案资源管理器中右键单击包项目，然后选择 " **属性**"。 在包的属性页中，单击 " **配置属性**"，然后单击 " **StampInf**"。

WDK 包含所有 KMDF 和 UMDF 示例驱动程序的 INX 文件。

INX 文件可以包含以下字符串变量：

<a href="" id="-arch-"></a>$ARCH $  
Stampinf 将此变量替换为特定于体系结构的字符串。 例如，如果你正在使用 x86 生成环境，则该工具会将 $ARCH $ 替换为 "x86"。 你可以在需要在 INF 文件中指定特定体系结构的任何位置（如 [**Inf 制造商部分**](../install/inf-manufacturer-section.md)中）使用 $ARCH $ 字符串，如下所示：

```cpp
[Manufacturer]
%StdMfg%=Standard,NT$ARCH$
```

<a href="" id="-kmdfcoinstallerversion-"></a>$KMDFCOINSTALLERVERSION $  
如果使用 [Stampinf](../devtest/stampinf.md) 工具的-*k* 选项，则 Stampinf 会将此变量替换为表示特定版本 KMDF 共同安装程序的字符串。 在 INF 文件中指定框架的共同安装程序（如 [**Inf DDInstall. CoInstallers 部分**](../install/inf-ddinstall-coinstallers-section.md)中）时，可以使用 $KMDFCOINSTALLERVERSION $ 变量，如下所示：

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
如果在 Visual Studio 中设置 **KMDF 版本号** 属性 (或使用 [Stampinf](../devtest/stampinf.md) 工具的-*k* 选项) ，则 Stampinf 会将此变量替换为表示特定版本 KMDF 的字符串。 在 INF 文件中指定框架版本时，可以使用 $KMDFVERSION $ 变量，如指定 [KmdfLibraryVersion](installing-the-framework-s-co-installer.md) 指令时，如下所示：

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

[Stampinf](../devtest/stampinf.md) 还支持-*u* 选项来替换 INX 文件中的 UMDF 字符串变量。 如果驱动程序包同时包含基于 UMDF 的驱动程序和基于 KMDF 的驱动程序，则可将-*k* 和-*u* 选项用于单个 STAMPINF 命令和单个 INX 文件。

 

