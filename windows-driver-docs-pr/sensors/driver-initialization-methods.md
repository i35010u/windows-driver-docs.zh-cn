---
title: 驱动程序初始化方法
ms.assetid: CA8F6308-501D-47BC-902E-3259949A1D57
description: 传感器驱动程序支持的方法来初始化设备。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6b51c6f9daaada7997131f376d18000e941a9d1
ms.sourcegitcommit: a866b3470025d85b25a48857a81f893179698e7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92355971"
---
# <a name="driver-initialization-methods"></a>驱动程序初始化方法

传感器驱动程序必须支持客户端和设备初始化。 伪代码使用以下方法演示这一点：

- DriverClientInitialize ( # A1
- DeviceSensorInitialize ( # A1

## <a name="client-initialization"></a>客户端初始化

客户端初始化方法具有以下形式。

```cpp
DriverClientInitialize(sensorID)
{
    // the following properties can be set from the API
    CRI = defaultCRI
    CS[] = defaultCS[]
    LDA = default[LDA]

    // the following properties cannot be set from the API
    // the driver provides defaults for these properties
    // the defaults can be overridden by the device
    sensorCategory = defaultSensorCategory
    sensorType = defaultSensorType
    minCRI = defaultMinCRI
    persistentUniqueID = defaultPersistentUniqueID
    sensorManufacturer = defaultSensorManufacturer
    sensorModel = defaultSensorModel
    serialNumber = defaultSerialNumber
    friendlyName = defaultFriendlyName
    sensorDescription = defaultDescription
    connectionType = defaultConnectionType

    // the following values are internal to the driver
    clientCount = 0
    subscriberCount = 0

    flagCRI = false
    flagCS = false
    flagLDA = false

    deviceState = deviceStateDisconnected
}
```

## <a name="related-topics"></a>相关主题

[Windows 中的传感器和位置平台简介](/windows-hardware/drivers/sensors/)

[传感器驱动程序逻辑](/windows-hardware/drivers/sensors/driver-logic--pseudo-code-)
