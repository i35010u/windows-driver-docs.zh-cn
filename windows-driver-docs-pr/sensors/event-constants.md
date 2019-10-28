---
title: 事件常量
description: 传感器平台为驱动程序事件定义以下常量。
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
ms.openlocfilehash: fc51c1a7933b4599cbcb388472efa60e653fd450
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841682"
---
# <a name="event-constants"></a>事件常量


传感器平台为驱动程序事件定义以下常量。

### <a name="sensor-event-types"></a>传感器事件类型

传感器平台定义以下传感器事件类型标识符。

|名称|描述|
|--|--|
|SENSOR_EVENT_DATA_UPDATED|指示新数据可用。|
|SENSOR_EVENT_PROPERTY_CHANGED|指示属性值已更改。|
|SENSOR_EVENT_STATE_CHANGED|指示操作状态的更改，例如，从 SENSOR_STATE_INITIALIZING 到 SENSOR_STATE_READY。|

 

### <a name="sensor-event-propertykeys"></a>传感器事件 PROPERTYKEYs

传感器平台定义以下**PROPERTYKEY**，用于标识传感器事件的参数。

|名称|描述|
|--|--|
|SENSOR_EVENT_PARAMETER_EVENT_ID|指示[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)中的<strong>GUID</strong>值是事件类型 ID，如 SENSOR_EVENT_DATA_UPDATED。|
|SENSOR_EVENT_PARAMETER_STATE|指示[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)中的无符号整数值为传感器状态，如 SENSOR_STATE_READY。 若要引发状态更改事件，请调用[<strong>ISensorClassExtension：:P oststatechange</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)。 无需显式指定 SENSOR_EVENT_PARAMETER_STATE 来引发事件。|

 

<a name="requirements"></a>要求
------------

| | |
|--|--|
| 最低受支持的客户端 | Windows 7 |
| 最低受支持的服务器 | 无受支持的版本 |
| 版本 | 在 Windows 7 中提供|
| 标头 | 传感器。h |



## <a name="see-also"></a>另请参阅


[关于传感器驱动程序事件](about-sensor-driver-events.md)

[筛选数据](filtering-data.md)

[传感器地理位置驱动程序示例](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)

[**SensorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0001)

 

 






