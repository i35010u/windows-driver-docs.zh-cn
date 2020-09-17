---
title: 枚举已安装的设备安装程序类
description: 枚举已安装的设备安装程序类
ms.assetid: 24F7600B-AA61-484a-83E9-E4C3FD2EAF17
keywords:
- 枚举已安装的设备安装程序类 WDK
- 已安装的设备安装程序类 WDK
- 已安装的设备安装程序类 WDK，枚举
- 设备安装程序类 WDK 设备安装，枚举
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0687f39fc22d19881ecb2c654cf91a9c7600aef0
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717400"
---
# <a name="enumerating-installed-device-setup-classes"></a>枚举已安装的设备安装程序类


若要发现系统中安装的 [设备安装程序类](./overview-of-device-setup-classes.md) ，请不要通过直接访问注册表项来枚举设备安装程序类。 与任何注册表项一样，这些密钥的位置和格式可能在不同版本的 Windows 之间发生变化。

若要安全发现已安装的设备安装程序类，并查询和修改安装程序类的属性，请执行以下步骤：

1.  使用 [**SetupDiBuildClassInfoList**](/windows/win32/api/setupapi/nf-setupapi-setupdibuildclassinfolist) 或 [**SetupDiBuildClassInfoListEx**](/windows/win32/api/setupapi/nf-setupapi-setupdibuildclassinfolistexa) 检索当前安装在系统上的设备安装程序类集。

2.  使用 [**SetupDiGetClassDescription**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdescriptiona) 或 [**SetupDiGetClassDescriptionEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdescriptionexa) 检索已安装的安装程序类的说明。

3.  使用 [**SetupDiGetClassRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassregistrypropertya) 查询安装程序类属性和 [**SetupDiSetDeviceRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya) ，以设置安装程序类属性。

4.  使用 [**SetupDiOpenClassRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopenclassregkey) 或 [**SetupDiOpenClassRegKeyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa) 访问永久性注册表存储，以获取自定义的设备安装程序类设置。

 

