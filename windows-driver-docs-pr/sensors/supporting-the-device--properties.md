---
title: 设备属性支持
description: 设备属性支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7987add84da9106db98f4b02f63a8e47d69813e5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812139"
---
# <a name="support-for-device-properties"></a>设备属性支持


| 模块                  | 类/接口      |
|-------------------------|----------------------|
| AccelerometerDevice .cpp | CAccelerometerDevice |
| SensorDdi .cpp           | CSensorDdi           |
| SensorDevice .cpp        | CSensorDevice        |

 

Windows 传感器平台支持三种类别的传感器属性：

类别描述常规设备属性包括多个字符串，例如设备型号、制造商名称和序列号。 还包括设备数据，如当前传感器状态或最小报表间隔值。 此类别中的属性是只读的。
每个数据字段属性，适用于传感器的数据字段。 对于加速感应，这些是每个轴的最小值、最大值和分辨率。 此类别中的属性是只读的。
应用程序可以设置的可设置设备属性属性。 对于加速感应，这些是更改敏感度和报告间隔。
 

源文件 SensorDdi 具有三个 **PROPERTYKEY** 结构数组，它们对应于上表中的三个类别。

第一个阵列具有常规传感器属性-如制造商名称、设备型号和序列号等字符串。 此外，还存在类似于最小和最大范围的值、传感器分辨率和支持的最小报告时间间隔。

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

第二个数组包含三个每个数据字段属性-最小和最大范围以及传感器分辨率。

```cpp
const PROPERTYKEY g_SupportedPerDataFieldProperties[] =
{
    SENSOR_PROPERTY_RANGE_MINIMUM,
    SENSOR_PROPERTY_RANGE_MAXIMUM,
    SENSOR_PROPERTY_RESOLUTION,
};
```

第三个数组包含加速度的更改敏感度和当前报表间隔。

```cpp
const PROPERTYKEY g_SettableAccelerometerProperties[] =
{
    SENSOR_PROPERTY_CHANGE_SENSITIVITY,
    SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL,
};
```

## <a name="setting-the-general-and-per-data-field-properties"></a>设置常规和每个数据字段属性

示例驱动程序在初始化阶段设置一般和每个数据字段的属性。 处理此工作的代码可在 **CAccelerometerDevice：： SetDefaultProperties** 方法中找到。 有关设置这些属性的调用序列的信息，请参阅 [驱动程序初始化](driver-initialization.md)。

## <a name="setting-the-writeable-properties"></a>设置可写属性

当桌面或 WinRT 应用程序设置当前报表间隔，或更改敏感度属性时，传感器类扩展使用此方法序列进行更新。

| 方法                                    | 调用对象或方法         | 描述                                                                          |
|-------------------------------------------|----------------------------------|--------------------------------------------------------------------------------------|
| **CSensorDdi::OnSetProperties**           | SensorsClassExtension.dll        | 类扩展调用此方法以启动属性更新。                |
| **CSensorDevice：： SetProperties**          | **CSensorDdi::OnSetProperties**  | 使用应用提供的属性键和值应用新的属性。       |
| **CSensorDevice::ApplyUpdatedProperties** | **CSensorDevice：： SetProperties** | 重新应用新值，因为它可能会改变驱动程序存储的最小值。 |

 

 

 




