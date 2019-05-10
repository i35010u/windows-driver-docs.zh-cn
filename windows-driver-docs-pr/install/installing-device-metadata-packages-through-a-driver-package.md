---
title: 通过驱动程序包安装设备元数据包
description: 通过驱动程序包安装设备元数据包
ms.assetid: fd140583-d4f9-4817-8edc-5bc3c6a2a1d7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32a1fe740a5bcfdc9876a75cd49479b1910a72fa
ms.sourcegitcommit: 3a51ae8db61be0e25549a5527ea3143e3025e82f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65455795"
---
# <a name="installing-device-metadata-packages-through-a-driver-package"></a>通过驱动程序包安装设备元数据包


一个[驱动程序包](driver-packages.md)可以通过将其复制到安装设备元数据包[设备元数据存储区](device-metadata-store.md)。 这通过使用实现[ **INF CopyFiles 指令**](inf-copyfiles-directive.md)内[ **DestinationDirs** ](inf-destinationdirs-section.md)和[ **DDInstall** ](inf-ddinstall-section.md)的部分[INF 文件](overview-of-inf-files.md)驱动程序包。

**请注意**我们强烈建议您从 WMIS 服务器而不是通过驱动程序包安装设备元数据包。 有关详细信息，请参阅[WMIS 从安装设备元数据包](installing-device-metadata-packages-from-wmis.md)。



若要安装通过设备元数据包[驱动程序包](driver-packages.md)，您必须遵循以下准则：

-   设备元数据包必须复制到[设备元数据存储区](device-metadata-store.md)使用 INF 指令。 不得通过复制元数据包[共同安装程序](writing-a-co-installer.md)。

-   如果驱动程序包使用早于 Windows 7 的 Windows 版本上安装的设备，则必须使用单独[ **INF *DDInstall*部分**](inf-ddinstall-section.md) ，其中包含你元数据相关 INF 指令。 必须指定在此节名称[ **INF*模型*部分**](inf-models-section.md)通过*TargetOSversion*指定修饰*OSMajorVersion*并*OSMinorVersion* Windows 7 或更高版本 Windows 的值。

    **请注意**如果不使用单独的 INF *DDInstall*修饰的 Windows 7 或更高版本的 Windows，安装数字签名的部分[驱动程序包](driver-packages.md)将导致在签名警报，如果安装在早于 Windows 7 的 Windows 版本上。




有关详细信息，请参阅[结合使用的操作系统版本的平台扩展](combining-platform-extensions-with-operating-system-versions.md)。


-   必须将驱动程序包中的所有元数据包复制到正确的区域设置特定的文件夹中[设备元数据存储区](device-metadata-store.md)。 为了支持对区域设置动态更改需要此项。

-   COPYFLG_NODECOMP 标志 (0x00000800) 中必需[ **INF CopyFiles 指令**](inf-copyfiles-directive.md) ，用于指定设备元数据包。 此标志可保证设备元数据包的二进制完整性保留和安装驱动程序包时可避免设备元数据包的解压缩。

-   您必须首先进行数字签名的设备元数据包之前进行数字签名的驱动程序包。 有关数字签名的详细信息，请参阅[驱动程序签名](driver-signing.md)。

-   元数据的包安装在安装过程中任何失败导致驱动程序安装失败。

下面的示例演示如何为设备元数据存储区中使用的 INF 文件复制到特定于区域设置的目录路径设备元数据包[ **DestinationDirs 部分**](inf-destinationdirs-section.md)并[**DDInstall** ](inf-ddinstall-section.md) INF 部分：

```cpp
[SourceDisksNames]
1 = %Media_Description%,,,\MetadataPackage ;

[SourceDisksFiles.NTx86]
GUID1.devicemetadata-ms= 1,, ;A metadata package file for EN-US
GUID2.devicemetadata-ms= 1,, ;A metadata package file for AR-SA
GUID3.devicemetadata-ms= 1,, ;A metadata package file for JA-JP

[DestinationDirs]
COPYMETADATA_EN-US = 24, \ProgramData\Microsoft\Windows\DeviceMetadataStore\EN-US ;
COPYMETADATA_AR-SA = 24, \ProgramData\Microsoft\Windows\DeviceMetadataStore\AR-SA ;
COPYMETADATA_JA-JP = 24, \ProgramData\Microsoft\Windows\DeviceMetadataStore\JA-JP ;
. . .

[DeviceInstall.ntx86]
CopyFiles=COPYMETADATA_EN-US
CopyFiles=COPYMETADATA_AR-SA
CopyFiles=COPYMETADATA_JA-JP

[COPYMETADATA_EN-US]
GUID1.devicemetadata-ms,,,0x00000800 ;COPYFLG_NODECOMP
[COPYMETADATA_AR-SA]
GUID2.devicemetadata-ms,,,0x00000800 ;COPYFLG_NODECOMP
[COPYMETADATA_JA-JP]
GUID3.devicemetadata-ms,,,0x00000800 ;COPYFLG_NODECOMP
```









