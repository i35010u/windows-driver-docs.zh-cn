---
title: 支持的设备属性
description: 支持的设备属性
ms.assetid: ED9A67C4-DFD6-4CF1-B911-29570B3409A5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07792c72589abd9cc292b4c9d777a34ff4ce449b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563885"
---
# <a name="support-for-device-properties"></a>支持的设备属性


| 模块                  | 类/接口      |
|-------------------------|----------------------|
| AccelerometerDevice.cpp | CAccelerometerDevice |
| SensorDdi.cpp           | CSensorDdi           |
| SensorDevice.cpp        | CSensorDevice        |

 

Windows 传感器平台支持三种类别的传感器属性：

类别说明常规设备属性包括设备型号、 制造商名称和序列号等字符串的数目。 此外包括当前的传感器状态或最小报表间隔值等的设备数据。 此类别中的属性是只读的。
每个数据字段的属性应用于传感器的数据字段的属性。 对于加速感应器，这些是最小值、 最大值，并为每个轴的解决方法。 此类别中的属性是只读的。
可设置设备属性的应用程序可以设置属性。 对于加速感应器，这些是更改敏感度和报表时间间隔。
 

源文件 SensorDdi.cpp，已有三个数组**PROPERTYKEY**对应于上表中的三个类别的结构。

第一个数组具有常规传感器属性-例如制造商的名称、 设备型号、 序列号的字符串。 此外，有值，如最小和最大范围、 传感器解析，以及受支持的最小报表时间间隔。

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

第二个数组具有三个每个数据字段属性的最小值和最大范围，以及传感器解析。

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

## <a name="setting-the-general-and-per-data-field-properties"></a>设置一般和每个数据字段属性

示例驱动程序设置常规和每个数据字段属性在初始化阶段。 处理这项工作的代码中找到**CAccelerometerDevice::SetDefaultProperties**方法。 有关设置这些属性的调用的序列的信息，请参阅[驱动程序初始化](driver-initialization.md)。

## <a name="setting-the-writeable-properties"></a>设置可写属性

时桌面或 WinRT，应用程序设置当前报表的时间间隔内，或更改敏感度属性，传感器类扩展使用这一序列的方法来进行更新。

| 方法                                    | 调用对象或方法         | 描述                                                                          |
|-------------------------------------------|----------------------------------|--------------------------------------------------------------------------------------|
| **CSensorDdi::OnSetProperties**           | SensorsClassExtension.dll        | 类扩展调用此方法来启动属性更新。                |
| **CSensorDevice::SetProperties**          | **CSensorDdi::OnSetProperties**  | 应用使用的属性键和值由应用程序提供的新属性。       |
| **CSensorDevice::ApplyUpdatedProperties** | **CSensorDevice::SetProperties** | 重新应用新值，因为它可能已更改驱动程序存储的最小值。 |

 

 

 




