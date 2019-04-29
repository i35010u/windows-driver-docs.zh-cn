---
title: 事件常量
description: 传感器平台定义以下常量的驱动程序的事件。
ms.assetid: d9bcfda4-d731-462f-802d-99c85911a6ca
keywords:
- 事件常量
- 传感器设备
topic_type:
- apiref
api_name:
- Event Constants
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: b5ad2115639364fbec507f14ef94bb11ca4aa658
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377782"
---
# <a name="event-constants"></a>事件常量


传感器平台定义以下常量的驱动程序的事件。

### <a name="sensor-event-types"></a>传感器事件类型

传感器平台定义以下传感器事件类型标识符。

|名称|描述|
|--|--|
|SENSOR_EVENT_DATA_UPDATED|指示新数据可用。|
|SENSOR_EVENT_PROPERTY_CHANGED|指示属性值更改。|
|SENSOR_EVENT_STATE_CHANGED|例如，到 SENSOR_STATE_READY SENSOR_STATE_INITIALIZING 从指示操作状态的更改。|

 

### <a name="sensor-event-propertykeys"></a>传感器事件 PROPERTYKEYs

传感器平台定义了以下**PROPERTYKEY**s 以标识传感器事件的参数。

|名称|描述|
|--|--|
|SENSOR_EVENT_PARAMETER_EVENT_ID|指示<strong>GUID</strong>中的值[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)是事件类型 ID，如 SENSOR_EVENT_DATA_UPDATED。|
|SENSOR_EVENT_PARAMETER_STATE|指示中的无符号的整数值[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)是传感器状态，例如 SENSOR_STATE_READY。 若要引发状态更改事件，调用[ <strong>ISensorClassExtension::PostStateChange</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)。 无需显式指定 SENSOR_EVENT_PARAMETER_STATE 来引发事件。|

 

<a name="requirements"></a>要求
------------

| | |
|--|--|
| 最低受支持的客户端 | Windows 7 |
| 最低受支持的服务器 | 无受支持的版本 |
| Version | 在 Windows 7 中可用|
| Header | Sensors.h |



## <a name="see-also"></a>请参阅


[有关传感器驱动程序事件](about-sensor-driver-events.md)

[筛选数据](filtering-data.md)

[传感器地理位置驱动程序示例](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)

[**SensorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0001)

 

 






