---
title: 修改设备属性的规则
description: 修改设备属性的规则
ms.assetid: EB554B5C-310A-4b2c-A2D5-22A113415400
keywords:
- 设备属性 WDK 设备安装，修改规则
- 设备属性 WDK 设备安装，修改
- 修改设备属性 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0123e13d64fbdb02cb35859cc5fe57a97c4a0035
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095021"
---
# <a name="rules-for-modifying-device-properties"></a>修改设备属性的规则


许多 [设备属性](device-properties.md) 都具有对其他属性或设备状态的复杂依赖关系。 例如， [**DEVPKEY_Device_Class**](./devpkey-device-class.md) 和 [**DEVPKEY_Device_ClassGuid**](./devpkey-device-classguid.md) 的值必须彼此保持一致。

直接修改保留属性可能会使设备安装状态无效。 例如，如果更改了 [**DEVPKEY_Device_DeviceDesc**](./devpkey-device-devicedesc.md) ，则系统功能 (如备份、驱动程序回滚和 Windows 更新) 可能会中断。

以下属性是只读的，绝不能用 [**SetupDiSetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)设置：

-   [**DEVPKEY_Device_Address**](./devpkey-device-address.md)

-   [**DEVPKEY_Device_BusNumber**](./devpkey-device-busnumber.md)

-   [**DEVPKEY_Device_BusTypeGuid**](./devpkey-device-bustypeguid.md)

-   [**DEVPKEY_Device_Capabilities**](./devpkey-device-capabilities.md)

-   [**DEVPKEY_Device_EnumeratorName**](./devpkey-device-enumeratorname.md)

-   [**DEVPKEY_Device_LegacyBusType**](./devpkey-device-legacybustype.md)

-   [**DEVPKEY_Device_PDOName**](./devpkey-device-pdoname.md)

-   [**DEVPKEY_Device_PowerData**](./devpkey-device-powerdata.md)

-   [**DEVPKEY_Device_RemovalPolicy**](./devpkey-device-removalpolicy.md)

-   [**DEVPKEY_Device_RemovalPolicyDefault**](./devpkey-device-removalpolicydefault.md)

-   [**DEVPKEY_Device_UINumber**](./devpkey-device-uinumber.md)

以下属性是可写的。 但是，它们是为供操作系统使用而保留的，不能直接设置：

-   [**DEVPKEY_Device_Class**](./devpkey-device-class.md)

-   [**DEVPKEY_Device_ClassGuid**](./devpkey-device-classguid.md)

-   [**DEVPKEY_Device_Driver**](./devpkey-device-driver.md)

-   [**DEVPKEY_Device_DriverDesc**](./devpkey-device-driverdesc.md)

-   [**DEVPKEY_Device_Manufacturer**](./devpkey-device-manufacturer.md)

**注意**  *类安装*程序和*共同安装*程序不得更改设备属性 ([**DEVPKEY_Device_FriendlyName**](./devpkey-device-friendlyname.md)) 的友好名称，以及设备 ([**DEVPKEY_Device_UpperFilters**](./devpkey-device-upperfilters.md)和 DEVPKEY_Device_LowerFilters) 和[**DEVPKEY_Device_LowerFilters**](./devpkey-device-lowerfilters.md)的筛选器驱动程序的上部和下部筛选器驱动程序。 有关详细信息，请参阅 [访问设备实例属性](accessing-device-instance-properties--windows-vista-and-later-.md)。

 

 

