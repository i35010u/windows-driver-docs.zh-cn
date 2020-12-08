---
title: 枚举已安装的设备安装程序类
description: 枚举已安装的设备安装程序类
keywords:
- 枚举已安装的设备安装程序类 WDK
- 已安装的设备安装程序类 WDK
- 已安装的设备安装程序类 WDK，枚举
- 设备安装程序类 WDK 设备安装，枚举
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 716f2cc298a1cd5155de6473cc9c0d73d7bafcb7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813159"
---
# <a name="enumerating-installed-device-setup-classes"></a>枚举已安装的设备安装程序类


若要发现系统中安装的 [设备安装程序类](./overview-of-device-setup-classes.md) ，请不要通过直接访问注册表项来枚举设备安装程序类。 与任何注册表项一样，这些密钥的位置和格式可能在不同版本的 Windows 之间发生变化。

若要安全发现已安装的设备安装程序类，并查询和修改安装程序类的属性，请执行以下步骤：

1.  使用 [**SetupDiBuildClassInfoList**](/windows/win32/api/setupapi/nf-setupapi-setupdibuildclassinfolist) 或 [**SetupDiBuildClassInfoListEx**](/windows/win32/api/setupapi/nf-setupapi-setupdibuildclassinfolistexa) 检索当前安装在系统上的设备安装程序类集。

2.  使用 [**SetupDiGetClassDescription**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdescriptiona) 或 [**SetupDiGetClassDescriptionEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdescriptionexa) 检索已安装的安装程序类的说明。

3.  使用 [**SetupDiGetClassRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassregistrypropertya) 查询安装程序类属性和 [**SetupDiSetDeviceRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya) ，以设置安装程序类属性。

4.  使用 [**SetupDiOpenClassRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopenclassregkey) 或 [**SetupDiOpenClassRegKeyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa) 访问永久性注册表存储，以获取自定义的设备安装程序类设置。

 

