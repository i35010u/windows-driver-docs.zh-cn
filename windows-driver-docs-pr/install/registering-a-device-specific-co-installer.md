---
title: 注册特定于设备的辅助安装程序
description: 注册特定于设备的辅助安装程序
keywords:
- 设备特定的共同安装程序 WDK 设备安装
- 注册特定于设备的共同安装程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1360290545810adca0c2927139b473a1f733dffe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819497"
---
# <a name="registering-a-device-specific-co-installer"></a>注册特定于设备的辅助安装程序





若要注册特定于设备的共同安装程序，请将以下部分添加到设备的 INF 文件中：

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

" **DestinationDirs** " 部分中的条目指定 *Xxx* CopyFilesSection 中列出的文件将复制到系统目录中。 *Xxx* 前缀标识 (例如 cdrom_CopyFilesSection) 的驱动程序、设备或设备组。 *Xxx* 前缀应是唯一的。

共同安装程序的 *安装节名称* 项可使用可选的 OS/体系结构扩展进行修饰 (例如 cdrom_install。NTx86. CoInstallers) 。 有关详细信息，请参阅 [**INF *DDInstall* 部分**](inf-ddinstall-section.md)。

<em>Xxx</em>**_AddReg** 部分中的条目在设备的 *驱动程序密钥* 中创建 **CoInstallers32** 值条目。 该条目包含共同安装程序 DLL 和（可选）特定入口点。 如果省略入口点，则默认值为 CoDeviceInstall。 十六进制标志参数 (0x00010000) 指定这是一个 [REG_MULTI_SZ](/windows/desktop/SysInfo/registry-value-types) 的值项。

若要为某个设备注册多个特定于设备的共同安装程序，请复制每个辅助安装程序的文件，并在注册表项中包含多个字符串。 例如，要注册两个共同安装程序，请创建如下所示的 INF 部分：

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

当处理 Coinstallers INF 部分时，将在安装设备的过程中注册特定于设备的共同安装程序。 然后，Setupapi.log 会在安装过程的每个后续步骤调用共同安装程序。 如果为某个设备注册了多个共同安装程序，则 Setupapi.log 会按照它们在注册表中列出的顺序调用它们。

 

