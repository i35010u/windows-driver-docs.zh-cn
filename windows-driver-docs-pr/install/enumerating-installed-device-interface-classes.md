---
title: 枚举已安装的设备接口
description: 枚举已安装的设备接口
ms.assetid: 14A9E6DD-58A9-4af0-B469-7CCF4596BE27
keywords:
- 枚举已安装的设备接口 WDK
- 已安装的设备接口 WDK
- 已安装的设备接口 WDK，枚举
- 设备接口 WDK 设备安装，枚举
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01375fb5ce446b3f3e86ec481e495304dba31bfe
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095380"
---
# <a name="enumerating-installed-device-interfaces"></a>枚举已安装的设备接口


不能通过直接访问注册表项来枚举系统中的设备接口类。 与任何注册表项一样，在不同版本的 Windows 之间，密钥的位置、名称或格式可能会更改。

使用以下准则来安全发现设备接口的属性：

-   用户模式应用程序应遵循以下步骤：

    1.  使用 [**SetupDiGetClassDevs**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw) 或 [**SetupDiGetClassDevsEx**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa) 检索支持指定设备接口类的接口的设备。 必须在 *Flags* 参数中设置 DIGCF_DEVICEINTERFACE 标志，并且必须将 *枚举器* 参数设置为特定的设备实例标识符。

        若要仅包含系统中存在的设备接口，请在 *Flags* 参数中设置 DIGCF_PRESENT 标志。

    2.  使用 [**SetupDiEnumDeviceInterfaces**](/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces) 枚举为设备接口类注册的接口。 此接口类通过 *InterfaceClassGuid* 参数指定。

-   内核模式驱动程序应使用 [**IoGetDeviceInterfaces**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfaces) 来枚举系统中安装的设备接口类。

 

