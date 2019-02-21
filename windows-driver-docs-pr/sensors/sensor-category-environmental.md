---
title: 传感器\_类别\_环境
description: 传感器\_类别\_环境类别包含提供有关周围的环境或天气信息的传感器。
ms.assetid: 49839092-0792-4e89-bc3a-7defc4730937
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
ms.openlocfilehash: d130f2a0e6a8667a0da6737742b5afc9700ee13d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519767"
---
# <a name="sensorcategoryenvironmental"></a>传感器\_类别\_环境


传感器\_类别\_环境类别包含提供有关周围的环境或天气信息的传感器。

### <a name="platform-defined-sensor-types"></a>平台定义的传感器类型

此类别包括以下平台定义的传感器类型。

|传感器类型|含义|
|--|--|
|SENSOR_TYPE_ENVIRONMENTAL_ATMOSPHERIC_PRESSURE|Barometers。|
|SENSOR_TYPE_ENVIRONMENTAL_HUMIDITY|Hygrometers。|
|SENSOR_TYPE_ENVIRONMENTAL_TEMPERATURE|温度计。|
|SENSOR_TYPE_ENVIRONMENTAL_WIND_DIRECTION|天气叶轮。|
|SENSOR_TYPE_ENVIRONMENTAL_WIND_SPEED|Anemometers。|

 

### <a name="platform-defined-data-fields"></a>平台定义的数据字段

此类别包括以下平台定义的数据字段。

|数据类型|在任务栏的搜索框中键入|含义|
|--|--|--|
|SENSOR_DATA_TYPE_ATMOSPHERIC_PRESSURE_BAR|VT_R4|大气压力大气 （条形图） 中。|
|SENSOR_DATA_TYPE_TEMPERATURE_CELSIUS|VT_R4|单位为摄氏度的温度。|
|SENSOR_DATA_TYPE_RELATIVE_HUMIDITY_PERCENT|VT_R4|相对湿度百分比。|
|SENSOR_DATA_TYPE_WIND_DIRECTION_DEGREES_ANTICLOCKWISE|VT_R4|大风的方向相对于磁北方，以度为单位。 北部表示为介于 0.0 （顶部 x 轴），增加逆时针方向旋转中的值。 向上 z 轴点。|
|SENSOR_DATA_TYPE_WIND_SPEED_METERS_PER_SECOND|VT_R4|以米为单位每秒风速。|

 

>[!IMPORTANT]
> 每个平台定义环境的数据类型**PROPERTYKEY**基于一种常见**GUID**名为传感器\_数据\_类型\_ENVIRONMENTAL\_GUID。 由于它是保留的基值，请勿使用此**GUID**来定义你自己属性的密钥。

 

## <a name="requirements"></a>要求


| | |
|--|--|
|最低受支持的客户端|Windows 7|
|最低受支持的服务器|无受支持的版本|
|版本|在 Windows 7 中可用。|
|标头|Sensors.h|


 

 





