---
title: 驱动程序的初始化方法
ms.assetid: CA8F6308-501D-47BC-902E-3259949A1D57
description: 若要初始化设备传感器驱动程序支持的方法。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c538a27af08030c5ab44acbf17f4e0de27ef8541
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377812"
---
# <a name="driver-initialization-methods"></a>驱动程序的初始化方法


传感器驱动程序必须支持客户端和设备的初始化。 伪代码演示了这可以通过使用以下方法：

-   DriverClientInitialize()
-   DeviceSensorInitialize()

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
[传感器驱动程序开发的基础知识](sensor-driver-development-basics.md)



