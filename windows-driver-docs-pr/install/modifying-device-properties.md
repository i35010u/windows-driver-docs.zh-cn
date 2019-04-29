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
ms.openlocfilehash: 6bedb78dec0465b00360a87a216ec4d0933d0c50
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378356"
---
# <a name="rules-for-modifying-device-properties"></a>修改设备属性的规则


许多[设备属性](device-properties.md)复杂的依赖关系对其他属性或设备的状态。 例如，值[ **DEVPKEY_Device_Class** ](https://msdn.microsoft.com/library/windows/hardware/ff542385)并[ **DEVPKEY_Device_ClassGuid** ](https://msdn.microsoft.com/library/windows/hardware/ff542388)必须在与另一个保持一致。

保留属性的直接修改可能使设备安装状态无效。 例如，如果[ **DEVPKEY_Device_DeviceDesc** ](https://msdn.microsoft.com/library/windows/hardware/ff542407)已更改，系统可能会中断 （例如备份、 驱动程序回滚和 Windows Update） 的功能。

以下属性是只读的可永远不会设置与[ **SetupDiSetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552163):

-   [**DEVPKEY_Device_Address**](https://msdn.microsoft.com/library/windows/hardware/ff542359)

-   [**DEVPKEY_Device_BusNumber**](https://msdn.microsoft.com/library/windows/hardware/ff542364)

-   [**DEVPKEY_Device_BusTypeGuid**](https://msdn.microsoft.com/library/windows/hardware/ff542371)

-   [**DEVPKEY_Device_Capabilities**](https://msdn.microsoft.com/library/windows/hardware/ff542373)

-   [**DEVPKEY_Device_EnumeratorName**](https://msdn.microsoft.com/library/windows/hardware/ff542489)

-   [**DEVPKEY_Device_LegacyBusType**](https://msdn.microsoft.com/library/windows/hardware/ff542541)

-   [**DEVPKEY_Device_PDOName**](https://msdn.microsoft.com/library/windows/hardware/ff542580)

-   [**DEVPKEY_Device_PowerData**](https://msdn.microsoft.com/library/windows/hardware/ff542586)

-   [**DEVPKEY_Device_RemovalPolicy**](https://msdn.microsoft.com/library/windows/hardware/ff542597)

-   [**DEVPKEY_Device_RemovalPolicyDefault**](https://msdn.microsoft.com/library/windows/hardware/ff542603)

-   [**DEVPKEY_Device_UINumber**](https://msdn.microsoft.com/library/windows/hardware/ff542660)

以下属性是可写。 但是，它们仅用于操作系统，不能直接设置：

-   [**DEVPKEY_Device_Class**](https://msdn.microsoft.com/library/windows/hardware/ff542385)

-   [**DEVPKEY_Device_ClassGuid**](https://msdn.microsoft.com/library/windows/hardware/ff542388)

-   [**DEVPKEY_Device_Driver**](https://msdn.microsoft.com/library/windows/hardware/ff542427)

-   [**DEVPKEY_Device_DriverDesc**](https://msdn.microsoft.com/library/windows/hardware/ff542436)

-   [**DEVPKEY_Device_Manufacturer**](https://msdn.microsoft.com/library/windows/hardware/ff542558)

**请注意**  *类的安装程序*并*共同安装程序*不得更改设备属性的友好名称除外 ([**DEVPKEY_Device_FriendlyName**](https://msdn.microsoft.com/library/windows/hardware/ff542502)) 和设备的上限和下限的筛选器驱动程序 ([**DEVPKEY_Device_UpperFilters** ](https://msdn.microsoft.com/library/windows/hardware/ff542667)并[ **DEVPKEY_Device_LowerFilters**](https://msdn.microsoft.com/library/windows/hardware/ff542554)). 有关详细信息，请参阅[访问设备实例属性](accessing-device-instance-properties--windows-vista-and-later-.md)。

 

 

 





