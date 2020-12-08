---
title: 传感器 \_ 类别 \_ 环境
description: 传感器 \_ 类别 \_ 环境类别包含的传感器提供有关周围环境或天气的信息。
keywords:
- SENSOR_CATEGORY_ENVIRONMENTAL 传感器设备
topic_type:
- apiref
api_name:
- SENSOR_CATEGORY_ENVIRONMENTAL
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 730829650d36336b5846c385106f99e72baa29bd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812215"
---
# <a name="sensor_category_environmental"></a>传感器 \_ 类别 \_ 环境


传感器 \_ 类别 \_ 环境类别包含的传感器提供有关周围环境或天气的信息。

### <a name="platform-defined-sensor-types"></a>平台定义的传感器类型

此类别包括以下平台定义的传感器类型。

|传感器类型|含义|
|--|--|
|SENSOR_TYPE_ENVIRONMENTAL_ATMOSPHERIC_PRESSURE|Barometers.|
|SENSOR_TYPE_ENVIRONMENTAL_HUMIDITY|Hygrometers.|
|SENSOR_TYPE_ENVIRONMENTAL_TEMPERATURE|温度计.|
|SENSOR_TYPE_ENVIRONMENTAL_WIND_DIRECTION|天气 vanes。|
|SENSOR_TYPE_ENVIRONMENTAL_WIND_SPEED|Anemometers.|

 

### <a name="platform-defined-data-fields"></a>平台定义的数据字段

此类别包括以下平台定义的数据字段。

|数据类型|类型|含义|
|--|--|--|
|SENSOR_DATA_TYPE_ATMOSPHERIC_PRESSURE_BAR|VT_R4|) 的 atmospheres (条面临大气。|
|SENSOR_DATA_TYPE_TEMPERATURE_CELSIUS|VT_R4|温度（摄氏度）。|
|SENSOR_DATA_TYPE_RELATIVE_HUMIDITY_PERCENT|VT_R4|相对湿度，以百分比表示。|
|SENSOR_DATA_TYPE_WIND_DIRECTION_DEGREES_ANTICLOCKWISE|VT_R4|相对于北部的风方向，以度为单位。 北部在 x 轴)  (顶部表示为0.0，值以逆时针旋转。 Z 轴向上指。|
|SENSOR_DATA_TYPE_WIND_SPEED_METERS_PER_SECOND|VT_R4|风速度，以米/秒为单位。|

 

>[!IMPORTANT]
> 每个平台定义的环境数据类型 **PROPERTYKEY** 基于一个名为 **GUID** "传感器 \_ 数据 \_ 类型 \_ 环境 GUID" 的通用 GUID \_ 。 由于这是保留的基值，请不要使用此 **GUID** 来定义自己的属性键。

 

## <a name="requirements"></a>要求


**支持的最低客户端**： Windows 7

**支持的最低服务器**：不支持

**版本**：在 Windows 7 中可用。

**标头**：传感器。h



 

 





