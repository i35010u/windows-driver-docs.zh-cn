---
title: 修改设备属性的规则
description: 修改设备属性的规则
ms.assetid: EB554B5C-310A-4b2c-A2D5-22A113415400
keywords:
- 设备属性 WDK 设备安装，用于修改规则
- 设备属性 WDK 设备安装，修改
- 修改设备属性 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67d00b231a9ee0ee8b6812c4cf10e925634e5b39
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377663"
---
# <a name="rules-for-modifying-device-properties"></a>修改设备属性的规则


许多[设备属性](device-properties.md)复杂的依赖关系对其他属性或设备的状态。 例如，值[ **DEVPKEY_Device_Class** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-class)并[ **DEVPKEY_Device_ClassGuid** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-classguid)必须在与另一个保持一致。

保留属性的直接修改可能使设备安装状态无效。 例如，如果[ **DEVPKEY_Device_DeviceDesc** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-devicedesc)已更改，系统可能会中断 （例如备份、 驱动程序回滚和 Windows Update） 的功能。

以下属性是只读的可永远不会设置与[ **SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw):

-   [**DEVPKEY_Device_Address**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-address)

-   [**DEVPKEY_Device_BusNumber**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-busnumber)

-   [**DEVPKEY_Device_BusTypeGuid**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-bustypeguid)

-   [**DEVPKEY_Device_Capabilities**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-capabilities)

-   [**DEVPKEY_Device_EnumeratorName**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-enumeratorname)

-   [**DEVPKEY_Device_LegacyBusType**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-legacybustype)

-   [**DEVPKEY_Device_PDOName**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-pdoname)

-   [**DEVPKEY_Device_PowerData**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-powerdata)

-   [**DEVPKEY_Device_RemovalPolicy**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-removalpolicy)

-   [**DEVPKEY_Device_RemovalPolicyDefault**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-removalpolicydefault)

-   [**DEVPKEY_Device_UINumber**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-uinumber)

以下属性是可写。 但是，它们仅用于操作系统，不能直接设置：

-   [**DEVPKEY_Device_Class**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-class)

-   [**DEVPKEY_Device_ClassGuid**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-classguid)

-   [**DEVPKEY_Device_Driver**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-driver)

-   [**DEVPKEY_Device_DriverDesc**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-driverdesc)

-   [**DEVPKEY_Device_Manufacturer**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-manufacturer)

**请注意**  *类的安装程序*并*共同安装程序*不得更改设备属性的友好名称除外 ([**DEVPKEY_Device_FriendlyName**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-friendlyname)) 和设备的上限和下限的筛选器驱动程序 ([**DEVPKEY_Device_UpperFilters** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-upperfilters)并[ **DEVPKEY_Device_LowerFilters**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-lowerfilters)). 有关详细信息，请参阅[访问设备实例属性](accessing-device-instance-properties--windows-vista-and-later-.md)。

 

 

 





