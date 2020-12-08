---
title: '\_全部传感器类别 \_'
description: 传感器 \_ 类别 \_ all 类别表示所有平台定义的传感器类别的集合。
keywords: SENSOR_CATEGORY_ALL 传感器设备
topic_type:
- apiref
api_name:
- SENSOR_CATEGORY_ALL
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: f8d54ab85dc6765782ab9e202535b77af726b872
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812235"
---
# <a name="sensor_category_all"></a>\_全部传感器类别 \_


传感器 \_ 类别 \_ all 类别表示所有平台定义的传感器类别的集合。

## <a name="platform-defined-property-keys"></a>平台定义的属性键

此类别包括以下平台定义的数据字段。

|数据类型|类型|含义|
|--|--|--|
|SENSOR_DATA_TYPE_TIMESTAMP|VT_FILETIME|对于所有数据报表都是必需的。 将每个数据报表标记为创建数据报表的时间。 使用协调世界时 (UTC) 。|
 

>[!IMPORTANT]
> 每个平台定义的通用数据类型 **PROPERTYKEY** 基于一个名为 **GUID** "传感器 \_ 数据 \_ 类型 \_ 公用 guid" 的通用 guid \_ 。 由于这是保留的基值，请不要使用此 **GUID** 来定义自己的属性键。

 

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 7

**支持的最低服务器**：不支持

**版本**：在 Windows 7 中可用。

**标头**：传感器。h

 

 





