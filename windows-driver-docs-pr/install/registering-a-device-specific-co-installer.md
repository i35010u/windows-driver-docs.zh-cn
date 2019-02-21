---
title: 注册的特定于设备的共同安装程序
description: 注册的特定于设备的共同安装程序
ms.assetid: 7a80bc60-e2f0-4447-bd73-4ce12fcfc2e3
keywords:
- 特定于设备的共同安装程序 WDK 设备安装
- 注册特定于设备的共同安装程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ab7e8a3ff040d26938a099d52b91ff6d58ad263
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525461"
---
# <a name="registering-a-device-specific-co-installer"></a>注册的特定于设备的共同安装程序





若要注册的特定于设备的共同安装程序，请将以下各节添加到设备的 INF 文件：

```cpp
;  :
;  :
[DestinationDirs]
XxxCopyFilesSection = 11                \\DIRID_SYSTEM
                                        \\ Xxx = driver or dev. prefix
;  :
;  :
[XxxInstall.OS-platform.CoInstallers]   \\ OS-platform is optional
CopyFiles = XxxCopyFilesSection
AddReg = Xxx.OS-platform.CoInstallers_AddReg
 
[XxxCopyFilesSection]
XxxCoInstall.dll
 
[Xxx.OS-platform.CoInstallers_AddReg]
HKR,,CoInstallers32,0x00010000,"XxxCoInstall.dll, \
 XxxCoInstallEntryPoint"
```

中的条目**DestinationDirs**部分指定文件中列出*Xxx*CopyFilesSection 将复制到系统目录。 *Xxx*前缀标识驱动程序、 设备或一组设备 (例如，cdrom_CopyFilesSection)。 *Xxx*前缀应是唯一的。

*安装部分名称*条目共同安装程序可以使用可选操作系统/体系结构扩展 (例如，cdrom_install 修饰。NTx86.CoInstallers)。 有关详细信息，请参阅[ **INF *DDInstall*部分**](inf-ddinstall-section.md)。

中的条目<em>Xxx</em>**_AddReg**部分创建**CoInstallers32**值中设备的条目*驱动程序键*。 该条目包含共同安装程序 DLL 和 （可选） 指定入口点。 如果省略的入口点，默认值为 CoDeviceInstall。 十六进制 flags 参数 (0x00010000) 指定，这是[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)值项目。

若要注册多个特定于设备的共同安装程序的设备，请将文件复制为每个共同安装程序并在注册表项中包含多个字符串。 例如，若要注册两个共同安装程序，创建 INF 部分如下所示：

```cpp
;   :
;   :
[DestinationDirs]
XxxCopyFilesSection = 11                \\DIRID_SYSTEM
                                        \\ Xxx = driver or dev. prefix
;   :
;   :
[XxxInstall.OS-platform.CoInstallers]   \\ OS-platform is optional
CopyFiles = XxxCopyFilesSection
AddReg = Xxx.OS-platform.CoInstallers_AddReg
 
[XxxCopyFilesSection]
XxxCoInstall.dll                         \\ copy 1st coinst. file
YyyCoInstall.dll                         \\ copy 2nd coinst. file
 
[Xxx.OS-platform.CoInstallers_AddReg]
HKR,,CoInstallers32,0x00010000,                 \
    "XxxCoInstall.dll, XxxCoInstallEntryPoint", \
    "YyyCoInstall.dll, YyyCoInstallEntryPoint"
                                         \\ add both to registry
```

特定于设备的共同安装程序会在过程中安装一台设备，共同安装程序 INF 部分处理时的注册。 SetupAPI 然后调用共同安装程序在安装过程的每个后续步骤。 如果多个共同安装程序已注册的设备，SetupAPI 的注册表中的列的顺序调用它们。

 

 





