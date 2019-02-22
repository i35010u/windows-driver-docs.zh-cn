---
title: 初始化地理位置对象
description: Geolocation.cpp 包含初始化的可设置属性键和模拟地理位置传感器的数据字段键的 Initialize 方法。
ms.assetid: 3803BD3B-9853-4AA4-A278-22F8D835B1ED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d43e676a93ec298a0daf71b18820a6f70b72c18
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543516"
---
# <a name="initializing-the-geolocation-object"></a>初始化地理位置对象

> [!IMPORTANT] 
> 已弃用此文档和 Windows 8.1 的地理位置驱动程序示例。

对象的源文件、 geolocation.cpp，包含**初始化**初始化可设置属性键和模拟地理位置传感器的数据字段密钥的方法。 传感器管理器在启动时调用此方法。

属性键 (**PROPERTYKEY**) 是一种数据结构组成**GUID**和一个**DWORD**的传感器属性提供的唯一标识符。 对于模拟的地理位置传感器，有对应的三个可设置属性键： 设备的变化敏感度，其当前报告间隔，以及所需的准确性。 文件 geolocation.cpp 中定义了这些密钥。

```cpp
const PROPERTYKEY g_SettableGeolocationProperties[] =
{
    SENSOR_PROPERTY_CHANGE_SENSITIVITY,         //[VT_UNKNOWN], IPortableDeviceValues
    SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL,    //[VT_UI4]
    SENSOR_PROPERTY_LOCATION_DESIRED_ACCURACY,  //[VT_UI4]
};
```

有关更改敏感度和报表时间间隔内的详细信息，请参阅[筛选数据](https://msdn.microsoft.com/library/windows/hardware/hh706201)主题。

数据字段该键**PROPERTYKEY**驱动程序用来标识它支持每个唯一的数据字段。 在伪地理位置传感器的情况下有八个受支持的数据字段包含数据，例如读取、 当前纬度 （以度为单位），（以度为单位），当前经度和等等的时间戳。 在文件 geolocation.cpp 中也定义了这些密钥。

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

**CSensorManager::Start**方法将调用**CGeolocation::Initialize**后它会立即创建传感器设备驱动程序接口 (DDI)。 这项工作出现在模块 sensormanager.cpp 中。

**初始化**方法，反过来，调用**InitializeGeolocation**方法。 此后一种方法将调用**CGeolocation::AddGeolocationSettablePropertyKeys**初始化伪传感器支持的可写属性的属性键。 添加属性键之后, **InitializeGeolocation**方法将调用**CGeolocation::AddGeolocationDataFieldKeys**来初始化支持的数据字段的数据字段键。

## <a name="related-topics"></a>相关主题
[定义地理位置对象](defining-the-geolocation-object.md)  
[筛选数据](https://msdn.microsoft.com/library/windows/hardware/hh706201)  



