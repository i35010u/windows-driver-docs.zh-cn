---
title: 通过驱动程序包安装设备元数据包
description: 通过驱动程序包安装设备元数据包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ab8a834587974136d5500e99a77d1d65fa31165
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794879"
---
# <a name="installing-device-metadata-packages-through-a-driver-package"></a>通过驱动程序包安装设备元数据包


[驱动程序包](driver-packages.md)可以通过将设备元数据包复制到[设备元数据存储](device-metadata-store.md)来安装它们。 这是通过在驱动程序包的 [inf 文件](overview-of-inf-files.md)的 [**DestinationDirs**](inf-destinationdirs-section.md)和 [**DDInstall**](inf-ddinstall-section.md)部分中使用 [**inf CopyFiles 指令**](inf-copyfiles-directive.md)来完成的。

**注意**  我们强烈建议你从 WMIS 服务器而不是通过驱动程序包安装设备元数据包。 有关详细信息，请参阅 [从 WMIS 安装设备元数据包](installing-device-metadata-packages-from-wmis.md)。



若要通过 [驱动程序包](driver-packages.md)安装设备元数据包，必须遵循以下准则：

-   必须使用 INF 指令将设备元数据包复制到 [设备元数据存储](device-metadata-store.md) 。 [共同安装程序](writing-a-co-installer.md)不得复制元数据包。

-   如果你的驱动程序包用于在早于 Windows 7 的 Windows 版本上安装设备，则必须使用包含与元数据相关的 INF 指令的单独 [**INF *DDInstall* 部分**](inf-ddinstall-section.md) 。 必须通过使用为 Windows 7 或更高版本的 Windows 指定 *OSMajorVersion* 和 *OSMinorVersion* 值的 *TargetOSversion* 修饰，在 " [**INF *模型*" 部分**](inf-models-section.md)中指定此部分名称。

    **注意**  如果不使用为 Windows 7 或更高版本的 Windows 修饰的单独 INF *DDInstall* 部分，则在 windows 7 之前的 windows 版本上安装时，数字签名的 [驱动程序包](driver-packages.md) 将导致签名警报。




有关详细信息，请参阅将 [平台扩展与操作系统版本结合起来](combining-platform-extensions-with-operating-system-versions.md)。


-   驱动程序包中的所有元数据包都必须复制到 [设备元数据存储](device-metadata-store.md)中正确的特定于区域设置的文件夹。 这是为了支持对区域设置进行动态更改所必需的。

-   指定设备元数据包的 [**INF CopyFiles 指令**](inf-copyfiles-directive.md) 中需要 COPYFLG_NODECOMP 标志 (0x00000800) 。 此标志保证在安装驱动程序包时，保留设备元数据包的二进制完整性并避免设备元数据包的解压缩。

-   在对驱动程序包进行数字签名之前，必须先对设备元数据包进行数字签名。 有关数字签名的详细信息，请参阅 [驱动程序签名](driver-signing.md)。

-   安装元数据包安装过程中的任何故障都会导致驱动程序安装失败。

下面的示例演示如何使用 [**DestinationDirs 节**](inf-destinationdirs-section.md) 和 [**DDInstall**](inf-ddinstall-section.md) INF 部分中设备元数据存储的 inf 文件将设备元数据包复制到区域设置特定的目录路径：

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









