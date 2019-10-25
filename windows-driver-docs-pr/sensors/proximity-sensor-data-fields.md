---
title: 邻近感应传感器数据字段
description: 本主题提供有关特定于邻近感应传感器的数据字段的信息。
ms.assetid: 03B561DB-FAF2-4404-AA49-6A0DA139AA11
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: e54cd2c045a773deb46a66133db61cc92e0e2f35
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842335"
---
# <a name="proximity-sensor-data-fields"></a>邻近感应传感器数据字段


本主题提供有关特定于邻近感应传感器的数据字段的信息。

下表显示了数据字段。 有关 "类型" 列中显示的类型的详细信息，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|在任务栏的搜索框中键入|必需/可选|描述|
|--|--|--|--|
|PKEY_SensorData_ProximityDetection|VT_BOOL|必需|指示对象在传感器附近。|
|PKEY_SensorData_ProximityDistanceMillimeters|VT_UI4|可选|与检测到的对象的距离（以毫米为单位）。|

 

## <a name="remarks"></a>备注


如果某个传感器支持**PKEY\_SensorData\_ProximityDistanceMillimeters** "数据字段，则响应 PKEY\_SensorData 的[EvtSensorGetDataFieldProperties](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)调用 **\_ProximityDistanceMillimeters**数据字段，传感器必须报告以下数据字段*属性*：

|数据字段属性|在任务栏的搜索框中键入|必需/可选|描述|
|--|--|--|--|
|PKEY_SensorDataField_RangeMinimum|VT_R4 （float）|必需|指示传感器的有效检测范围的下限（含）（以毫米为单位）。|
|PKEY_SensorDataField_RangeMaximum|VT_R4 （float）|必需|指示传感器的有效检测范围的上限（含）（以毫米为单位）。|

 

>[!NOTE]
> 有效检测范围是从传感器到对象的直线距离。 此距离沿传感器指向的轴测量，并包含实际边界。

 

如果驱动程序无法报告这些数据字段属性，应用仍将能够通过 WinRT API 检测近程传感器。 但是，这些应用程序将不知道受支持的传感器范围，并可能决定不使用该传感器。

## <a name="related-topics"></a>相关主题


[EvtSensorGetDataFieldProperties](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)

[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






