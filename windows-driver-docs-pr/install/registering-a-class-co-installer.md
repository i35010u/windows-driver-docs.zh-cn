---
title: 注册类辅助安装程序
description: 注册类辅助安装程序
keywords:
- 类共同安装程序 WDK
- 注册类共同安装程序
- 安装类-GUID WDK 设备安装
- CoDeviceInstallers
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 838f25f0df7017f1d193007b3730bbfe6d3b2bae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796005"
---
# <a name="registering-a-class-co-installer"></a>注册类辅助安装程序





若要为特定安装程序类的每个设备注册一个共同安装程序，请在 **HKLM \\ System \\ CurrentControlSet \\ Control \\ CoDeviceInstallers** 子项下创建类似于下面的注册表项：

```cpp
{setup-class-GUID}: REG_MULTI_SZ : "XyzCoInstall.dll,XyzCoInstallEntryPoint\0\0"
```

系统将创建 **CoDeviceInstallers** 键。 *安装程序类-guid* 指定 [设备安装程序类](./overview-of-device-setup-classes.md)的 guid。 如果共同安装程序适用于多个类的设备，请为每个安装程序类创建一个单独的值项。

不能覆盖之前已写入到 *安装程序类 GUID* 密钥的其他共同安装程序。 读取密钥，将你的共同安装程序字符串附加到 [REG_MULTI_SZ](/windows/desktop/SysInfo/registry-value-types) 列表，然后将该密钥写回注册表。

如果省略 *CoInstallEntryPoint*，则默认值为 CoDeviceInstall。

共同安装程序 DLL 也必须复制到系统目录中。

一旦复制了文件并创建了注册表项，就可以为相关设备和服务调用类共同安装程序。

您可以使用如下所示的 INF 文件来注册类共同安装程序，而不是手动创建注册表项：

```cpp
[version]
signature = "$Windows NT$"
 
[DestinationDirs]
DefaultDestDir = 11    // DIRID_SYSTEM
 
[DefaultInstall]
CopyFiles = @classXcoinst.dll
AddReg = CoInstaller_AddReg
 
[CoInstaller_AddReg]
HKLM,System\CurrentControlSet\Control\CoDeviceInstallers, \
 {setup-class-GUID},0x00010008, "classXcoinst.dll,classXCoInstaller"
; above line uses the line continuation character ()
```

此示例 INF 将文件 *classXcoinst.dll* 复制到系统目录，并在 **CoDeviceInstallers** 项下为 *安装程序类 GUID* 类生成一个条目。 *Xxx* _AddReg 部分中的条目指定两个标志： "00010000" 标志指定该条目是一个 [REG_MULTI_SZ](/windows/desktop/SysInfo/registry-value-types)，而 "00000008" 标志指定将新值追加到任何现有值 (如果该新值尚未出现在字符串) 中。

注册类共同安装程序的此类 INF 可以通过右键单击 "安装" 或通过调用 **SetupInstallFromInfSection** 的应用程序激活。

 

