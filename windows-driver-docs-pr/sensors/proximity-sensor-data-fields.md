---
title: 邻近感应传感器数据字段
description: 本主题提供有关特定于邻近感应传感器的数据字段的信息。
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6542f889929bd28f596f159dbf2f5b11c7360b8f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812259"
---
# <a name="proximity-sensor-data-fields"></a>邻近感应传感器数据字段


本主题提供有关特定于邻近感应传感器的数据字段的信息。

下表显示了数据字段。 有关 "类型" 列中显示的类型的详细信息，请参阅 [PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)。

|属性键|类型|必需/可选|说明|
|--|--|--|--|
|PKEY_SensorData_ProximityDetection|VT_BOOL|必须|指示对象在传感器附近。|
|PKEY_SensorData_ProximityDistanceMillimeters|VT_UI4|可选|与检测到的对象的距离（以毫米为单位）。|

 

## <a name="remarks"></a>备注


如果某个传感器支持 **PKEY \_ SensorData \_ ProximityDistanceMillimeters** data 字段，则在响应 [EvtSensorGetDataFieldProperties](/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config) 针对 **PKEY \_ SensorData \_ ProximityDistanceMillimeters** data 字段的调用时，该传感器必须报告以下数据字段 *属性*：

|数据字段属性|类型|必需/可选|说明|
|--|--|--|--|
|PKEY_SensorDataField_RangeMinimum|VT_R4 (float) |必须|指示传感器的有效检测范围（以毫米为单位）的下限) 的下边界 (。|
|PKEY_SensorDataField_RangeMaximum|VT_R4 (float) |必须|指示传感器的有效检测范围的上限（以毫米为单位） (非独占检测范围) 。|

 

>[!NOTE]
> 有效检测范围是从传感器到对象的直线距离。 此距离沿传感器指向的轴测量，并包含实际边界。

 

如果驱动程序无法报告这些数据字段属性，应用仍将能够通过 WinRT API 检测近程传感器。 但是，这些应用程序将不知道受支持的传感器范围，并可能决定不使用该传感器。

## <a name="related-topics"></a>相关主题


[EvtSensorGetDataFieldProperties](/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)

[PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)

