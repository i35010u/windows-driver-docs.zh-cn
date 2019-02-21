---
Description: Defining the Sensor Properties
title: 定义传感器属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d36174949ef6b5dd40e0f6b53c3e3270219500af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540959"
---
# <a name="defining-the-sensor-properties"></a>定义传感器属性


Windows 便携式设备 (WPD) 属性是对象说明的元数据。 本部分介绍的示例驱动程序支持的属性。 设备对象支持 18 属性，并且每个传感器对象支持 10 个属性。 某些对象属性所需的驱动程序的功能，例如 WPD\_对象\_ID 和 WPD\_对象\_的永久\_UNIQUE\_id。 存在其他属性来提供信息，用于描述对象，如 WPD\_设备\_制造商。

WDK WPD 驱动程序开发人员对于包含多种工具。 这些工具之一*WpdInfo.exe*，使开发人员若要检查的对象和由给定的驱动程序公开的属性。 以下屏幕截图*WpdInfo.exe*工具显示的属性驱动程序中的设备对象支持。

![wpd 信息工具](images/wpdinfo_device_object.png)

在上图中，最左边的列的顶部窗格中列出的驱动程序支持的对象。 中心窗格中列出的设备对象的驱动程序支持的 18 属性。 在此窗格中的第一列列出属性名称、 第二列列出了该属性的值、 第三个列，列出的类型，依此类推。 下部窗格显示了返回的事件的驱动程序支持的信息。

以下屏幕截图*WpdInfo.exe*工具显示的属性的 TempHumidity 对象支持。

![wpd 信息工具](images/wpdinfo_temphumidity_object.png)

此对象支持 10 个属性。 其中，传感器\_读取和传感器\_更新\_间隔是由 WpdBasicHardwareDriver，定义并表示数据由传感器固件颁发的自定义属性。 在此示例中，传感器\_读取属性标识传感器 (2 = Sensiron 温度和湿度传感器)，元素计数 (1)、 元素大小 （7 字节）、 当前温度 (74.4 F) 和相对湿度 （37.3%)。 传感器\_更新\_间隔属性指定该设备会触发事件的频率。 指示 2 秒更新间隔以毫秒为单位，指定此值，02000。 固件支持更新间隔介于 2 到 60 秒之间的配置。

WPD，在由 PROPERTYKEY 数据结构表示属性。 此结构由两部分组成： 一个 GUID 和一个 dword 值。 全局唯一标识符 (GUID) 标识属性类别和 DWORD 标识该类别中的特定属性。 PROPERTYKEY 结构的详细信息，请参阅[PROPERTYKEYs 和 WPD 中的 Guid](propertykeys-and-guids-in-windows-portable-devices.md) Windows Driver Kit (WDK) 文档中。

使用 DECLARE\_PROPERTYKEY 宏，您可以在您的驱动程序中声明一个新的属性的 PROPERTYKEY 结构。 下面的示例演示声明 PROPERTYKEY 传感器\_读取属性。 此示例显示在*WpdObjectProperties.cpp*文件。

```cpp
DECLARE_PROPERTYKEY(SENSOR_READING, 0xa7ef4367, 0x6550, 0x4055, 0xb6, 0x6f, 0xbe, 0x6f, 0xda, 0xcf, 0x4e, 0x9f, 2);
```

除了声明 PROPERTYKEY 时，必须定义该密钥。 定义的传感器\_读取项将显示在*Stdafx.h*文件。

```cpp
DEFINE_PROPERTYKEY(SENSOR_READING, 0xa7ef4367, 0x6550, 0x4055, 0xb6, 0x6f, 0xbe, 0x6f, 0xda, 0xcf, 0x4e, 0x9f, 2);
```

*WpdObjectProperties.cpp*文件包含的 PROPERTKEY 结构定义的三个数组。 这些列阵标识相关的、 支持的属性的集合。 第一个是 PROPERTYKEYs 标识设备和传感器对象所共有的属性的数组。

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

如果您使用*WpdInfo.exe*工具检索当前的设备和传感器属性时，你将注意到前一个数组中的属性显示在两个列表。

第二个数组是 PROPERTYKEYS 标识设备对象支持的属性的数组。

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

分配给此数组中的各种静态属性的值中定义*WpdObjectProperties.h*。

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

在为这些值分配**WpdObjectProperties::GetPropertyValuesForObject**方法。

例如，以下内容摘自此方法将设备模型字符串 （视差 BS2 传感器） 分配给 WPD\_设备\_模型属性。

```cpp
if (IsEqualPropertyKey(Key, WPD_DEVICE_MODEL))
{
    hr = pValues->SetStringValue(WPD_DEVICE_MODEL, DEVICE_MODEL_VALUE);
    CHECK_HR(hr, "Failed to set WPD_DEVICE_MODEL");
}
```

第三个数组是 PROPERTYKEYS 标识支持的传感器对象，以及常见的对象属性的属性的数组。

```cpp
const PROPERTYKEY g_SupportedSensorProperties[] =
{
    SENSOR_READING,
    SENSOR_UPDATE_INTERVAL,
    WPD_FUNCTIONAL_OBJECT_CATEGORY,
};
```

这些值也在分配**WpdObjectProperties::GetPropertyValuesForObject**方法。 但是，分配到传感器的值\_读取和传感器\_更新\_间隔属性不是常量; 相反，它们是两个 helper 函数来检索在真实时间中的值：**WpdObjectProperties::GetSensorReading**并**WpdObjectProperties::GetUpdateInterval**。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)









