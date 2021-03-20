---
title: 在 INF 文件中指定 KMDF 的共同安装程序
description: 如果你的驱动程序包中包含共同安装程序，请阅读本主题，了解你必须在驱动程序的 INF 文件中提供的部分。
keywords:
- Kernel-Mode Driver Framework WDK，安装驱动程序
- 基于框架的驱动程序 WDK KMDF，安装
- INF 文件 WDK KMDF，coinstallers
- coinstallers WDK KMDF
- CoInstallers 部分 WDK KMDF
- DDInstall 部分 WDK KMDF
- Wdf INF 文件部分 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb3cd7a2477bcfd08ae41e51065ea1679287a315
ms.sourcegitcommit: 76a7b604f13cf419ff21518337913820a703347f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2021
ms.locfileid: "104719504"
---
# <a name="specifying-the-kmdf-co-installer-in-an-inf-file"></a>在 INF 文件中指定 KMDF 的共同安装程序

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

如果你的 [驱动程序包](../install/components-of-a-driver-package.md)中包含共同安装程序，请阅读本主题，了解你必须在驱动程序的 INF 文件中提供的部分。 如果您提供自己的安装程序应用程序，该应用程序调用 Microsoft 提供的 msu 可再发行组件，则此信息不适用。

##  <a name="inf-file-sections-for-the-co-installer"></a>共同安装程序的 INF 文件部分


驱动程序的 INF 文件必须包含 INF <em>DDInstall</em>**。** 安装共同安装程序的 CoInstallers 部分。 例如，此部分可能名为 **MyDevice. ntx86. CoInstallers**。 有关在 INF 文件中指定共同安装程序的详细信息，请参阅 [**Inf DDInstall. CoInstallers 部分**](../install/inf-ddinstall-coinstallers-section.md)。

此外，驱动程序的 INF 文件必须包含 INF <em>DDInstall</em>**。** 安装后，共同安装程序读取的 Wdf 部分。 例如，此部分可能名为 **MyDevice. ntx86**。 安装框架的共同安装程序后，它将在安装驱动程序时读取此部分。

INF <em>DDInstall</em>**。Wdf** 部分包含以下指令：

- **KmdfService =** <em>DriverService</em>**，**<em>项安装-部分</em>

*DriverService* 表示操作系统将分配给驱动程序的内核模式服务的名称， *Wdf-安装部分* 表示 INF 部分的名称，共同安装程序读取此部分以获取有关驱动程序的信息。

*Wdf 安装节* 标识的 INF 部分必须包含以下指令：

-   **KmdfLibraryVersion =** *WdfLibraryVersion*

*WdfLibraryVersion* 表示库版本号，如 "1.0" 或 "1.11"。

例如，以下 INF <em>DDInstall</em>**。Wdf** 部分指定 **回显 \_ wdfsect** 作为 *Wdf 安装节* 名称。

```cpp
[ECHO_Device.NT.Wdf]
KmdfService = Echo, Echo_wdfsect
[Echo_wdfsect]
KmdfLibraryVersion = 1.0
```

可以使用 INX 文件和 [Stampinf](../devtest/stampinf.md) 工具避免为多个版本的框架创建多个 INF 文件。 有关 INX 文件的详细信息，请参阅[使用 INX 文件创建 INF 文件](using-inx-files-to-create-inf-files.md)。

### <a name="sample-inf-_ddinstall_coinstallers-and-_ddinstall_wdf-sections"></a><a href="" id="sample-inf-ddinstall-coinstallers-and-ddinstall-wdf-sections"></a>**示例 INF** **_DDInstall_。CoInstallers 和** **_DDInstall_。Wdf 部分**

下面的代码示例演示如何创建 INF <em>DDInstall</em>**。CoInstallers** 部分和 INF <em>DDInstall</em>**。** PnP 驱动程序的 INF 文件的 Wdf 部分。 该示例演示如何创建一个名为 *MyDevice* 的 inf 文件，该文件基于 [echo](/samples/browse/) 示例驱动程序的 *echo* 文件。 回显示例驱动程序位于 WDK 的示例目录中。

若要创建 *MyDevice*，必须将 *echo* 中的所有 **echo \_ 设备** 子字符串更改为适用于你的产品的名称。 下面的代码示例使用 **MyDevice**。

应尝试匹配 *Echo* 示例使用的部分布局。 换句话说，如有可能，请将与联合安装程序相关的部分结合在一起，以便更轻松地发现剪切和粘贴错误。

在修改了 *echo* 之前，安装共同安装程序的部分如下所示：

```cpp
=============== Top of Echo.inf ====================
....
....
[DestinationDirs]
DefaultDestDir = 12
ECHO_Device_CoInstaller_CopyFiles = 11
....
....
;
;--- ECHO_Device Co-installer installation ------
;
[ECHO_Device.NT.CoInstallers]
AddReg=ECHO_Device_CoInstaller_AddReg
CopyFiles=ECHO_Device_CoInstaller_CopyFiles

[ECHO_Device_CoInstaller_AddReg]
HKR,,CoInstallers32,0x00010000, "WdfCoInstaller01000.dll,WdfCoInstaller"

[ECHO_Device_CoInstaller_CopyFiles]
WdfCoInstaller01000.dll

[ECHO_Device.NT.Wdf]
KmdfService = Echo, Echo_wdfsect
[Echo_wdfsect]
KmdfLibraryVersion = 1.0

===============  End of Echo.inf ===============
```

更改所有 **ECHO \_ 设备** 子字符串后， *MyDevice* 文件应如下所示：

```cpp
=============== Top of MyDevice.inf ===============
....
....
[DestinationDirs]
DefaultDestDir = 12
MyDevice_CoInstaller_CopyFiles = 11
....
....
;
;--- MyDevice Co-installer installation ------
;
[MyDevice.NT.CoInstallers]
AddReg=MyDevice_CoInstaller_AddReg
CopyFiles=MyDevice_CoInstaller_CopyFiles

[MyDevice_CoInstaller_AddReg]
HKR,,CoInstallers32,0x00010000, "WdfCoInstaller01000.dll,WdfCoInstaller"

[MyDevice_CoInstaller_CopyFiles]
WdfCoInstaller01000.dll

[MyDevice.NT.Wdf]
KmdfService = MyDevice, MyDevice_wdfsect
[MyDevice_wdfsect]
KmdfLibraryVersion = 1.0
....
....
=============== End of MyDevice.inf ===============
```