---
title: 初始化地理位置对象
description: 地理位置 .cpp 包含初始化方法，该方法可为模拟的地理位置传感器初始化可设置的属性键和数据字段键。
ms.assetid: 3803BD3B-9853-4AA4-A278-22F8D835B1ED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96dabdd3519742278833e0b4c0d89b2f69cc2db6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188675"
---
# <a name="initializing-the-geolocation-object"></a>初始化地理位置对象

> [!IMPORTANT] 
> 此文档和 Windows 8.1 的地理位置驱动程序示例已弃用。

对象源文件（即 node.js）包含初始化方法，该 **方法可为** 模拟的地理位置传感器初始化可设置的属性键和数据字段键。 此方法由传感器管理器在启动时调用。

 (**PROPERTYKEY**) 的属性键是由 **GUID** 和 **DWORD** （提供传感器属性的唯一标识符）组成的数据结构。 对于模拟的地理位置传感器，有三个可设置的属性键，它们对应于：设备的更改敏感度、当前报表间隔以及所需的准确性。 这些密钥在文件地理位置 .cpp 中定义。

```cpp
const PROPERTYKEY g_SettableGeolocationProperties[] =
{
    SENSOR_PROPERTY_CHANGE_SENSITIVITY,         //[VT_UNKNOWN], IPortableDeviceValues
    SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL,    //[VT_UI4]
    SENSOR_PROPERTY_LOCATION_DESIRED_ACCURACY,  //[VT_UI4]
};
```

有关更改敏感度和报表间隔的详细信息，请参阅 [筛选数据](../sensors/filtering-data.md) 主题。

数据字段键是驱动程序用来标识它所支持的每个唯一数据字段的 **PROPERTYKEY** 。 对于伪地理位置传感器，有八个受支持的数据字段，这些字段包括读取时间戳、当前纬度 (度) 、当前经度 (度) 等数据。 这些密钥也是在文件的地理位置中定义的。

```cpp
const PROPERTYKEY g_SupportedGeolocationDataFields[] =
{
    SENSOR_DATA_TYPE_TIMESTAMP,                 //[VT_FILETIME]
    SENSOR_DATA_TYPE_LATITUDE_DEGREES,          //[VT_R8]
    SENSOR_DATA_TYPE_LONGITUDE_DEGREES,         //[VT_R8]
    SENSOR_DATA_TYPE_ERROR_RADIUS_METERS,       //[VT_R8]
    SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_METERS, //[VT_R8]
    SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_ERROR_METERS, //[VT_R8]
    SENSOR_DATA_TYPE_SPEED_KNOTS,               //[VT_R8]
    SENSOR_DATA_TYPE_TRUE_HEADING_DEGREES,      //[VT_R8]
};
```

**CSensorManager：： Start**方法将在创建传感器设备驱动程序接口 (DDI) 后立即调用**CGeolocation：： Initialize** 。 此操作发生在 sensormanager 模块中。

然后， **Initialize** 方法会调用 **InitializeGeolocation** 方法。 后一种方法会调用 **CGeolocation：： AddGeolocationSettablePropertyKeys** 来初始化伪传感器支持的可写属性的属性键。 添加属性键后， **InitializeGeolocation** 方法会调用 **CGeolocation：： AddGeolocationDataFieldKeys** 来初始化支持的数据字段的数据字段键。

## <a name="related-topics"></a>相关主题
[定义地理位置对象](defining-the-geolocation-object.md)  
[筛选数据](../sensors/filtering-data.md)