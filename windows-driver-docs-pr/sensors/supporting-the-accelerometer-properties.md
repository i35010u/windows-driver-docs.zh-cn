---
title: 支持加速感应器属性
description: 源文件 SensorDdi.cpp，包含有三个用于定义支持加速感应器设备的属性的 PROPERTYKEY 结构数组。
ms.assetid: A1196CFD-9A90-479A-859E-6F9850867AC6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de24efa4a5a01149edacd664939c8aa7619865a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378569"
---
# <a name="supporting-the-accelerometer-properties"></a>支持加速感应器属性


源文件 SensorDdi.cpp，包含有三个用于定义支持加速感应器设备的属性的 PROPERTYKEY 结构数组。

第一个数组包含常规传感器属性。 其中包括制造商的名称、 设备型号、 其序列号等，依此类推。 此外，有值，如最小和最大范围、 传感器解析，以及受支持的最小报表时间间隔。

```cpp
const PROPERTYKEY g_SupportedAccelerometerProperties[] =
{
    WPD_OBJECT_ID,
    SENSOR_PROPERTY_TYPE,
    SENSOR_PROPERTY_PERSISTENT_UNIQUE_ID,
    SENSOR_PROPERTY_MANUFACTURER,
    SENSOR_PROPERTY_MODEL,
    SENSOR_PROPERTY_SERIAL_NUMBER,
    SENSOR_PROPERTY_FRIENDLY_NAME,
    SENSOR_PROPERTY_DESCRIPTION,
    SENSOR_PROPERTY_CONNECTION_TYPE,
    SENSOR_PROPERTY_RANGE_MINIMUM,
    SENSOR_PROPERTY_RANGE_MAXIMUM,
    SENSOR_PROPERTY_RESOLUTION,
    SENSOR_PROPERTY_STATE,
    SENSOR_PROPERTY_MIN_REPORT_INTERVAL,
    WPD_FUNCTIONAL_OBJECT_CATEGORY,
};
```

第二个数组包含三个特定设备属性： 最小值和最大范围，以及传感器解析。

```cpp
const PROPERTYKEY g_SupportedPerDataFieldProperties[] =
{
    SENSOR_PROPERTY_RANGE_MINIMUM,
    SENSOR_PROPERTY_RANGE_MAXIMUM,
    SENSOR_PROPERTY_RESOLUTION,
};
```

第三个数组包含加速感应器的变化敏感度和当前报告间隔。

```cpp
const PROPERTYKEY g_SettableAccelerometerProperties[] =
{
    SENSOR_PROPERTY_CHANGE_SENSITIVITY,
    SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL,
};
```

## <a name="related-topics"></a>相关主题
[SpbAccelerometer 驱动程序示例](spbaccelerometer-driver-sample.md)



