---
title: 传感器\_类别\_生物识别
description: 传感器\_类别\_生物识别类别包含提供有关生物信息的传感器。
ms.assetid: e26073e1-11cc-40a9-9a60-3a15ceb46059
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
ms.openlocfilehash: 1b76336448a5b6ef1a27e297f8548b0e7627747c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566611"
---
# <a name="sensorcategorybiometric"></a>传感器\_类别\_生物识别


传感器\_类别\_生物识别类别包含提供有关生物信息的传感器。

## <a name="platform-defined-sensor-types"></a>平台定义的传感器类型

此类别包括以下平台定义的传感器类型。

|传感器类型|含义|
|--|--|
|SENSOR_TYPE_HUMAN_PRESENCE|检测在场的传感器。|
|SENSOR_TYPE_HUMAN_PROXIMITY|检测人邻近的传感器。|
|SENSOR_TYPE_TOUCH|触摸传感器。|

 

### <a name="platform-defined-data-fields"></a>平台定义的数据字段

此类别包括以下平台定义的数据字段。

|数据类型|在任务栏的搜索框中键入|含义|
|--|--|--|
|SENSOR_DATA_TYPE_HUMAN_PRESENCE|VT_BOOL|VARIANT_TRUE： 当用户使用该计算机。|
|SENSOR_DATA_TYPE_HUMAN_PROXIMITY_METERS|VT_R4|用户和计算机，以米为单位之间的距离。|
|SENSOR_DATA_TYPE_TOUCH_STATE|VT_BOOL|为 VARIANT_TRUE 时涉及到触摸传感器，否则为 VARIANT_FALSE。|

 

>[!IMPORTANT]
> 每个平台定义生物识别数据类型**PROPERTYKEY**基于一种常见**GUID**名为传感器\_数据\_类型\_生物识别\_GUID。 由于它是保留的基值，请勿使用此**GUID**来定义你自己属性的密钥。

 

## <a name="requirements"></a>要求


| | |
|--|--|
|最低受支持的客户端|Windows 7|
|最低受支持的服务器|无受支持的版本|
|版本|在 Windows 7 中可用。|
|Header|Sensors.h|

 

 





