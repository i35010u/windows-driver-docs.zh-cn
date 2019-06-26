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
ms.openlocfilehash: 3293b81b496c2607b9b02346f0686e73927c8d4a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379475"
---
# <a name="enumerating-installed-device-setup-classes"></a>枚举已安装的设备安装程序类


若要发现[设备安装程序类](device-setup-classes.md)，安装在系统中，通过直接访问注册表项不枚举设备安装程序类。 与任何注册表项，可能会更改的 Windows 不同版本之间的位置和格式的这些密钥。

若要安全地发现已安装的设备安装程序类，并以查询和修改安装程序类的属性，请执行以下步骤：

1.  使用[ **SetupDiBuildClassInfoList** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdibuildclassinfolist)或[ **SetupDiBuildClassInfoListEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdibuildclassinfolistexa)来检索的设备安装程序类的组当前安装在系统上。

2.  使用[ **SetupDiGetClassDescription** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdescriptiona)或[ **SetupDiGetClassDescriptionEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdescriptionexa)检索已安装的安装程序的说明类。

3.  使用[ **SetupDiGetClassRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassregistrypropertya)若要查询的安装程序类属性和[ **SetupDiSetDeviceRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)设置安装程序类属性。

4.  使用[ **SetupDiOpenClassRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkey)或[ **SetupDiOpenClassRegKeyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)访问自定义设备的永久注册表存储安装程序类设置。

 

 





