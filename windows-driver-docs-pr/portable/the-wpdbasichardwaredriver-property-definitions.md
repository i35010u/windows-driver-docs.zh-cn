---
description: 定义传感器属性
title: 定义传感器属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c324357ecdf8d7358e572b7935d62d95b0ae9a29
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969156"
---
# <a name="defining-the-sensor-properties"></a>定义传感器属性


 (WPD) 属性的 Windows 便携式设备是对象描述元数据。 本部分介绍了示例驱动程序支持的属性。 设备对象支持18个属性，单独的传感器对象支持10个属性。 驱动程序功能需要某些对象属性，如 WPD \_ 对象 \_ ID 和 WPD \_ 对象持久的 \_ \_ 唯一 \_ ID。 存在其他属性以提供描述对象的信息，如 WPD \_ 设备 \_ 制造商。

WDK 包含用于 WPD 驱动程序开发人员的多个工具。 *WpdInfo.exe*使用其中一种工具，开发人员可以检查由给定驱动程序公开的对象和属性。 以下 *WpdInfo.exe* 工具的屏幕截图显示了驱动程序中设备对象支持的属性。

![wpd 信息工具](images/wpdinfo_device_object.png)

在上图中，最左侧窗格中的最左侧列列出了驱动程序支持的对象。 中间窗格列出设备对象的驱动程序支持的18个属性。 此窗格中的第一列列出属性名称，第二列列出属性的值，第三列列出类型，依此类推。 下窗格显示了驱动程序支持的事件返回的信息。

以下 *WpdInfo.exe* 工具的屏幕截图显示了 TempHumidity 对象支持的属性。

![wpd 信息工具](images/wpdinfo_temphumidity_object.png)

此对象支持10个属性。 其中的传感器 \_ 读取和传感器 \_ 更新 \_ 间隔是由 WpdBasicHardwareDriver 定义的自定义属性，表示传感器固件发出的数据。 在此示例中，传感器 \_ 读数属性标识传感器 (2 = Sensiron 温度和湿度传感器) ，元素计数 (1) ，元素大小 (7 字节) ，当前温度 (74.4 F) ，相对湿度 (37.3% ) 。 传感器 \_ 更新 \_ 间隔属性指定设备触发事件的频率。 此值为02000，以毫秒为单位指定，这表示更新间隔为2秒。 固件支持将更新间隔配置为2到60秒。

在 WPD 中，属性由 PROPERTYKEY 数据结构表示。 此结构由两部分组成： GUID 和 DWORD。 全局唯一标识符 (GUID) 标识属性类别，而 DWORD 标识该类别中的特定属性。 有关 PROPERTYKEY 结构的详细信息，请参阅 Windows 驱动程序工具包 (WDK) 文档中的 WPD 中的 [PROPERTYKEYs 和 guid](propertykeys-and-guids-in-windows-portable-devices.md) 。

通过使用 DECLARE \_ PROPERTYKEY 宏，可以在驱动程序中声明新属性的 PROPERTYKEY 结构。 下面的示例演示了传感器读取属性的 PROPERTYKEY 声明 \_ 。 此示例显示在 *WpdObjectProperties* 文件中。

```cpp
DECLARE_PROPERTYKEY(SENSOR_READING, 0xa7ef4367, 0x6550, 0x4055, 0xb6, 0x6f, 0xbe, 0x6f, 0xda, 0xcf, 0x4e, 0x9f, 2);
```

除了声明 PROPERTYKEY 外，还必须定义键。 传感器读取密钥的定义 \_ 将出现在 *stdafx.h* 文件中。

```cpp
DEFINE_PROPERTYKEY(SENSOR_READING, 0xa7ef4367, 0x6550, 0x4055, 0xb6, 0x6f, 0xbe, 0x6f, 0xda, 0xcf, 0x4e, 0x9f, 2);
```

*WpdObjectProperties*文件包含 PROPERTKEY 结构的三个数组的定义。 这些阵列标识相关的、支持的属性的集合。 第一种是标识设备和传感器对象共有的属性的 PROPERTYKEYs 数组。

```cpp
const PROPERTYKEY g_SupportedCommonProperties[] =
{
    WPD_OBJECT_ID,
    WPD_OBJECT_PERSISTENT_UNIQUE_ID,
    WPD_OBJECT_PARENT_ID,
    WPD_OBJECT_NAME,
    WPD_OBJECT_FORMAT,
    WPD_OBJECT_CONTENT_TYPE,
    WPD_OBJECT_CAN_DELETE,
};
```

如果使用 *WpdInfo.exe* 工具检索当前设备和传感器属性，则会注意到这两个列表中的属性都显示在前面的数组中。

第二个数组是 PROPERTYKEYS 的数组，用于标识设备对象支持的属性。

```cpp
const PROPERTYKEY g_SupportedDeviceProperties[] =
{
    WPD_DEVICE_FIRMWARE_VERSION,
    WPD_DEVICE_POWER_LEVEL,
    WPD_DEVICE_POWER_SOURCE,
    WPD_DEVICE_PROTOCOL,
    WPD_DEVICE_MODEL,
    WPD_DEVICE_SERIAL_NUMBER,
    WPD_DEVICE_SUPPORTS_NON_CONSUMABLE,
    WPD_DEVICE_MANUFACTURER,
    WPD_DEVICE_FRIENDLY_NAME,
    WPD_DEVICE_TYPE,
    WPD_FUNCTIONAL_OBJECT_CATEGORY,
};
```

分配给此数组中各种静态属性的值是在 *WpdObjectProperties*中定义的。

```cpp
#define DEVICE_PROTOCOL_VALUE            L"Sensor Protocol ver 1.00"
#define DEVICE_FIRMWARE_VERSION_VALUE    L"1.0.0.0"
#define DEVICE_POWER_LEVEL_VALUE         100
#define DEVICE_MODEL_VALUE               L"RS232 Sensor"
#define DEVICE_FRIENDLY_NAME_VALUE       L"Parallax BS2 Sensor"
#define DEVICE_MANUFACTURER_VALUE        L"Windows Portable Devices Group"
#define DEVICE_SERIAL_NUMBER_VALUE       L"01234567890123-45676890123456"
#define DEVICE_SUPPORTS_NONCONSUMABLE_VALUE    FALSE
```

这些值是在 **WpdObjectProperties：： GetPropertyValuesForObject** 方法中赋值的。

例如，此方法中的以下摘录将 (视差 BS2 传感器) 的设备模型字符串分配到 WPD \_ 设备 \_ 模型属性。

```cpp
if (IsEqualPropertyKey(Key, WPD_DEVICE_MODEL))
{
    hr = pValues->SetStringValue(WPD_DEVICE_MODEL, DEVICE_MODEL_VALUE);
    CHECK_HR(hr, "Failed to set WPD_DEVICE_MODEL");
}
```

第三个数组是 PROPERTYKEYS 的数组，用于标识传感器对象支持的属性，以及通用对象属性。

```cpp
const PROPERTYKEY g_SupportedSensorProperties[] =
{
    SENSOR_READING,
    SENSOR_UPDATE_INTERVAL,
    WPD_FUNCTIONAL_OBJECT_CATEGORY,
};
```

这些值也是在 **WpdObjectProperties：： GetPropertyValuesForObject** 方法中赋值的。 但是，分配给传感器 \_ 读数和传感器 \_ 更新 \_ 间隔属性的值不是常量，而是通过两个 helper 函数实时检索值： **WpdObjectProperties：： GetSensorReading** 和 **WpdObjectProperties：： GetUpdateInterval**。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)









