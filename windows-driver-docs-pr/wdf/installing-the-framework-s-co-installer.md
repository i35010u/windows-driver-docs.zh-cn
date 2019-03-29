---
title: INF 文件中指定 KMDF 共同安装程序
description: 如果驱动程序包中包含共同安装程序，阅读此主题的有关部分必须在您的驱动程序 INF 文件中提供的信息。
ms.assetid: e4f476ad-1ab5-44e3-9368-7467479bda85
keywords:
- 内核模式驱动程序框架 WDK，安装驱动程序
- 基于框架的驱动程序 WDK KMDF，安装
- INF 文件 WDK KMDF，共同安装程序
- 共同安装程序 WDK KMDF
- 共同安装程序部分 WDK KMDF
- DDInstall 部分 WDK KMDF
- Wdf INF 文件部分 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17d345625221a546ad4f612e3fb7b3b5fc33c7fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564470"
---
# <a name="specifying-the-kmdf-co-installer-in-an-inf-file"></a>INF 文件中指定 KMDF 共同安装程序


如果包括中的共同安装程序在[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff539954)，请阅读本主题有关必须在您的驱动程序 INF 文件中提供的两部分信息。 如果提供自己调用 Microsoft 提供.msu 可再发行组件的安装程序应用程序，此信息不适用于。

##  <a name="inf-file-sections-for-the-co-installer"></a>辅助安装程序的 INF 文件部分


驱动程序的 INF 文件必须包含 INF <em>DDInstall</em>**。共同安装程序**共同安装程序将安装的部分。 如本部分可能名为**MyDevice.ntx86.CoInstallers**。 有关在 INF 文件中指定共同安装程序的详细信息，请参阅[ **INF DDInstall.CoInstallers 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547321)。

此外，驱动程序的 INF 文件必须包含 INF <em>DDInstall</em>**。Wdf**部分共同安装程序，读取后已安装。 例如，本部分中可能会被命名为**MyDevice.ntx86.Wdf**。 已安装的 framework 共同安装程序后，它会安装您的驱动程序时读取本部分。

INF <em>DDInstall</em>**。Wdf**部分包含以下指令：

- **KmdfService =** <em>DriverService</em>**,**<em>Wdf-install-section</em>

*DriverService*表示操作系统会将分配给驱动程序的内核模式服务的名称和*Wdf 安装部分*表示共同安装程序读取以获得 INF 部分的名称您的驱动程序有关的信息。

INF 部分*Wdf 安装部分*标识必须包含以下指令：

-   **KmdfLibraryVersion =** *WdfLibraryVersion*

*WdfLibraryVersion*表示库版本号，例如"1.0"或"1.11"。

例如，以下 INF <em>DDInstall</em>**。Wdf**节指定**Echo\_wdfsect**作为*Wdf 安装部分*名称。

```cpp
[ECHO_Device.NT.Wdf]
KmdfService = Echo, Echo_wdfsect
[Echo_wdfsect]
KmdfLibraryVersion = 1.0
```

您可以避免使用 INX 文件创建多个版本的 framework 的多个 INF 文件和[Stampinf](https://msdn.microsoft.com/library/windows/hardware/ff552786)工具。 有关 INX 文件的详细信息，请参阅[使用 INX 文件转换为创建 INF 文件](using-inx-files-to-create-inf-files.md)。

### <a href="" id="sample-inf-ddinstall-coinstallers-and-ddinstall-wdf-sections"></a>**示例 INF** * **DDInstall *。共同安装程序和** * **DDInstall *。Wdf 部分**

下面的代码示例演示如何创建 INF <em>DDInstall</em>**。共同安装程序**部分和 INF <em>DDInstall</em>**。Wdf**部分即插即用驱动程序的 INF 文件。 该示例演示如何创建调用的 INF 文件*MyDevice.inf* ，并基于[ECHO](https://go.microsoft.com/fwlink/p/?linkid=256129)示例驱动程序*Echo.inf*文件。 Echo 示例驱动程序位于 WDK 示例目录中。

若要创建*MyDevice.inf*，则必须更改所有**ECHO\_设备**中的子字符串*Echo.inf*到适合于您的产品的名称。 下面的代码示例使用**MyDevice**。

应尝试匹配部分布局的*Echo.inf*示例使用。 换而言之，如果可能，一起共同 installer 相关各节更轻松地找出剪切和粘贴错误。

已修改之前*echo.inf*，安装共同安装程序的部分是按如下所示：

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

更改所有后**ECHO\_设备**子字符串，你*MyDevice.inf*文件应如下显示：

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

[MyDevice_Device.NT.Wdf]
KmdfService = MyDevice, MyDevice_wdfsect
[MyDevice_wdfsect]
KmdfLibraryVersion = 1.0
....
....
=============== End of MyDevice.inf ===============
```

 

 





