---
title: 注册类共同安装程序
description: 注册类共同安装程序
ms.assetid: a86a4302-ec37-4117-aa5c-4fa84fbb7902
keywords:
- 类共同安装程序 WDK
- 注册类共同安装程序
- 安装程序类 GUID WDK 设备安装
- CoDeviceInstallers
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db8f5fd54dfac5dd5b0f4f7e9d5fcded5d177a69
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547675"
---
# <a name="registering-a-class-co-installer"></a>注册类共同安装程序





若要注册特定的安装程序类的每个设备的共同安装程序，创建如下所示的下一个注册表项**HKLM\\系统\\CurrentControlSet\\控制\\CoDeviceInstallers**子项：

```cpp
{setup-class-GUID}: REG_MULTI_SZ : "XyzCoInstall.dll,XyzCoInstallEntryPoint\0\0"
```

系统会创建**CoDeviceInstallers**密钥。 *安装程序类 GUID*指定的 GUID[设备安装程序类](device-setup-classes.md)。 如果共同安装程序适用于多个设备的类，创建每个安装程序类的单独值项。

您一定不能覆盖以前写入到其他共同安装程序*安装程序类 GUID*密钥。 读取注册表项，你共同安装程序将字符串追加到[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)列表，并将密钥返回写入注册表。

如果省略*CoInstallEntryPoint*，默认值是 CoDeviceInstall。

此外必须将共同安装程序 DLL 复制到系统目录。

类共同安装程序是可复制文件并将注册表条目后调用相关设备和服务。

而不是手动创建注册表条目以注册类共同安装程序，则可以注册使用 INF 文件如下所示：

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

此示例 INF 会将文件复制*classXcoinst.dll*到系统目录，并进行条目*安装程序类 GUID*类下**CoDeviceInstallers**密钥。 中的条目*Xxx*_AddReg 节指定两个标记:"00010000"标志指定的项是[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)，并"00000008"标志指定是要追加到任何新值（如果新值已不在字符串中存在） 的现有值。

右键单击安装或通过调用的应用程序，可以激活此类注册类共同安装程序的 INF **SetupInstallFromInfSection**。

 

 





