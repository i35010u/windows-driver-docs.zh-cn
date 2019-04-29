---
title: 枚举已安装的设备安装程序类
description: 枚举已安装的设备安装程序类
ms.assetid: 24F7600B-AA61-484a-83E9-E4C3FD2EAF17
keywords:
- 枚举已安装的设备安装程序类 WDK
- 已安装的设备安装程序类 WDK
- 安装设备安装程序类 WDK，枚举
- 设备安装程序类 WDK 设备安装，枚举
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73cf7ac20435bb3cd91edc88e7b1b22c433620eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386988"
---
# <a name="enumerating-installed-device-setup-classes"></a>枚举已安装的设备安装程序类


若要发现[设备安装程序类](device-setup-classes.md)，安装在系统中，通过直接访问注册表项不枚举设备安装程序类。 与任何注册表项，可能会更改的 Windows 不同版本之间的位置和格式的这些密钥。

若要安全地发现已安装的设备安装程序类，并以查询和修改安装程序类的属性，请执行以下步骤：

1.  使用[ **SetupDiBuildClassInfoList** ](https://msdn.microsoft.com/library/windows/hardware/ff550909)或[ **SetupDiBuildClassInfoListEx** ](https://msdn.microsoft.com/library/windows/hardware/ff550911)来检索的设备安装程序类的组当前安装在系统上。

2.  使用[ **SetupDiGetClassDescription** ](https://msdn.microsoft.com/library/windows/hardware/ff551053)或[ **SetupDiGetClassDescriptionEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551058)检索已安装的安装程序的说明类。

3.  使用[ **SetupDiGetClassRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551097)若要查询的安装程序类属性和[ **SetupDiSetDeviceRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552169)设置安装程序类属性。

4.  使用[ **SetupDiOpenClassRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552065)或[ **SetupDiOpenClassRegKeyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552067)访问自定义设备的永久注册表存储安装程序类设置。

 

 





