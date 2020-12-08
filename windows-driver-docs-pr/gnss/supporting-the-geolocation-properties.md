---
title: 支持地理位置属性
description: 源文件（即 node.js）包含三个 PROPERTYKEY 结构数组，它们定义了模拟传感器支持的属性。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bdda2ad6dbdc9f27c1ae358c97209869c43e898
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816791"
---
# <a name="supporting-the-geolocation-properties"></a>支持地理位置属性

> [!IMPORTANT] 
> 此文档和 Windows 8.1 的地理位置驱动程序示例已弃用。

源文件（即 node.js）包含三个 PROPERTYKEY 结构数组，它们定义了模拟传感器支持的属性。

第一个数组定义模拟传感器支持的只读和读写属性。

```cpp
const PROPERTYKEY g_SupportedGeolocationProperties[] =
{
    SENSOR_PROPERTY_TYPE,                       //[VT_CLSID]
    SENSOR_PROPERTY_STATE,                      //[VT_UI4]
    SENSOR_PROPERTY_MIN_REPORT_INTERVAL,        //[VT_UI4]
    SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL,    //[VT_UI4]
    SENSOR_PROPERTY_PERSISTENT_UNIQUE_ID,       //[VT_CLSID]
    SENSOR_PROPERTY_MANUFACTURER,               //[VT_LPWSTR]
    SENSOR_PROPERTY_MODEL,                      //[VT_LPWSTR]
    SENSOR_PROPERTY_SERIAL_NUMBER,              //[VT_LPWSTR]
    SENSOR_PROPERTY_FRIENDLY_NAME,              //[VT_LPWSTR]
    SENSOR_PROPERTY_DESCRIPTION,                //[VT_LPWSTR]
    SENSOR_PROPERTY_CONNECTION_TYPE,            //[VT_UI4]
    SENSOR_PROPERTY_CHANGE_SENSITIVITY,         //[VT_UNKNOWN], IPortableDeviceValues
    SENSOR_PROPERTY_LOCATION_DESIRED_ACCURACY,  //[VT_UI4]
    WPD_FUNCTIONAL_OBJECT_CATEGORY,             //[VT_CLSID]
};
```

示例驱动程序在检索属性时使用这些值 (或) 响应应用程序请求。 检索属性值的方法是 **CGeolocation：： GetPropertyValuesForGeolocationObject**。

第二个数组定义了可选属性。

```cpp
const PROPERTYKEY g_OptionalSupportedGeolocationProperties[] =
{
    SENSOR_PROPERTY_RANGE_MAXIMUM,              //[VT_UNKNOWN], IPortableDeviceValues
    SENSOR_PROPERTY_RANGE_MINIMUM,              //[VT_UNKNOWN], IPortableDeviceValues
    SENSOR_PROPERTY_ACCURACY,                   //[VT_UNKNOWN], IPortableDeviceValues
    SENSOR_PROPERTY_RESOLUTION,                 //[VT_UNKNOWN], IPortableDeviceValues
};
```

第三个阵列定义了伪传感器支持的可写属性或可设置的属性。

```cpp
const PROPERTYKEY g_SettableGeolocationProperties[] =
{
    SENSOR_PROPERTY_CHANGE_SENSITIVITY,         //[VT_UNKNOWN], IPortableDeviceValues
    SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL,    //[VT_UI4]
    SENSOR_PROPERTY_LOCATION_DESIRED_ACCURACY,  //[VT_UI4]
};
```

 (或属性) 更新可写属性时，示例驱动程序也使用这些值。 更新属性值的方法是 **CGeolocation：： UpdateGeolocationPropertyValues**。

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)  



