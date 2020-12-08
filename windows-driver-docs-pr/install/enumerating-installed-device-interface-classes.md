---
title: 枚举已安装的设备接口
description: 枚举已安装的设备接口
keywords:
- 枚举已安装的设备接口 WDK
- 已安装的设备接口 WDK
- 已安装的设备接口 WDK，枚举
- 设备接口 WDK 设备安装，枚举
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f075bde0337277b9be37f213772541b6b345c7ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813157"
---
# <a name="enumerating-installed-device-interfaces"></a>枚举已安装的设备接口


不能通过直接访问注册表项来枚举系统中的设备接口类。 与任何注册表项一样，在不同版本的 Windows 之间，密钥的位置、名称或格式可能会更改。

使用以下准则来安全发现设备接口的属性：

-   用户模式应用程序应遵循以下步骤：

    1.  使用 [**SetupDiGetClassDevs**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdevsw) 或 [**SetupDiGetClassDevsEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdevsexa) 检索支持指定设备接口类的接口的设备。 必须在 *Flags* 参数中设置 DIGCF_DEVICEINTERFACE 标志，并且必须将 *枚举器* 参数设置为特定的设备实例标识符。

        若要仅包含系统中存在的设备接口，请在 *Flags* 参数中设置 DIGCF_PRESENT 标志。

    2.  使用 [**SetupDiEnumDeviceInterfaces**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces) 枚举为设备接口类注册的接口。 此接口类通过 *InterfaceClassGuid* 参数指定。

-   内核模式驱动程序应使用 [**IoGetDeviceInterfaces**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfaces) 来枚举系统中安装的设备接口类。

 

