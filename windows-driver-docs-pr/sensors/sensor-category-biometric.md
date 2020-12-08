---
title: 传感器 \_ 类别 \_ 生物识别
description: 传感器 \_ 类别 \_ 生物识别类别包含提供有关生活的信息的传感器。
keywords:
- SENSOR_CATEGORY_BIOMETRIC 传感器设备
topic_type:
- apiref
api_name:
- SENSOR_CATEGORY_BIOMETRIC
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6a74df32146cc1ddb057dacb1ada618315a031fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812231"
---
# <a name="sensor_category_biometric"></a>传感器 \_ 类别 \_ 生物识别


传感器 \_ 类别 \_ 生物识别类别包含提供有关生活的信息的传感器。

## <a name="platform-defined-sensor-types"></a>平台定义的传感器类型

此类别包括以下平台定义的传感器类型。

|传感器类型|含义|
|--|--|
|SENSOR_TYPE_HUMAN_PRESENCE|检测人为状态的传感器。|
|SENSOR_TYPE_HUMAN_PROXIMITY|检测人为邻近性的传感器。|
|SENSOR_TYPE_TOUCH|触摸传感器。|

 

### <a name="platform-defined-data-fields"></a>平台定义的数据字段

此类别包括以下平台定义的数据字段。

|数据类型|类型|含义|
|--|--|--|
|SENSOR_DATA_TYPE_HUMAN_PRESENCE|VT_BOOL|VARIANT_TRUE 用户使用计算机的时间。|
|SENSOR_DATA_TYPE_HUMAN_PROXIMITY_METERS|VT_R4|人类与计算机之间的距离（以米为单位）。|
|SENSOR_DATA_TYPE_TOUCH_STATE|VT_BOOL|VARIANT_TRUE 触摸感应器接触时，则为; 否则 VARIANT_FALSE。|

 

>[!IMPORTANT]
> 每个平台定义的生物识别数据类型 **PROPERTYKEY** 都基于名 **GUID** 为传感器 \_ 数据 \_ 类型 \_ 生物识别 guid 的通用 GUID \_ 。 由于这是保留的基值，请不要使用此 **GUID** 来定义自己的属性键。

 

## <a name="requirements"></a>要求


**支持的最低客户端**： Windows 7

**支持的最低服务器**：不支持

**版本**：在 Windows 7 中可用。

**标头**：传感器。h


 

 





