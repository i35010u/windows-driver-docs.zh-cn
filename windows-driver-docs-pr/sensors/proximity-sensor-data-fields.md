---
title: 邻近感应传感器数据字段
description: 本主题提供有关特定于邻近感应传感器的数据字段的信息。
ms.assetid: 03B561DB-FAF2-4404-AA49-6A0DA139AA11
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: e502155193fa29a7f1ff00d4c76110f81e10f727
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330103"
---
# <a name="proximity-sensor-data-fields"></a>邻近感应传感器数据字段


本主题提供有关特定于邻近感应传感器的数据字段的信息。

下表显示数据字段。 有关类型列中显示的类型的详细信息，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|在任务栏的搜索框中键入|必需/可选|描述|
|--|--|--|--|
|PKEY_SensorData_ProximityDetection|VT_BOOL|必需|对象是邻近的传感器中指示。|
|PKEY_SensorData_ProximityDistanceMillimeters|VT_UI4|可选|检测到的对象，以毫米为单位的距离。|

 

## <a name="remarks"></a>备注


如果支持传感器**主键\_SensorData\_ProximityDistanceMillimeters**数据字段，然后在响应中的调用[EvtSensorGetDataFieldProperties](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)为**主键\_SensorData\_ProximityDistanceMillimeters**数据字段中，传感器必须报告以下数据字段*属性*:

|数据字段属性|在任务栏的搜索框中键入|必需/可选|描述|
|--|--|--|--|
|PKEY_SensorDataField_RangeMinimum|VT_R4 (float)|必需|指示 （非独占） 以毫米为单位的传感器的有效的检测范围的下限。|
|PKEY_SensorDataField_RangeMaximum|VT_R4 (float)|必需|指示 （非独占） 以毫米为单位的传感器的有效的检测范围的上限。|

 

>[!NOTE]
> 有效的检测范围是从传感器到对象的直线距离。 此距离沿轴其中指向传感器，，它是包括实际的边界。

 

如果该驱动程序无法报告这些数据字段属性，应用程序仍将能够检测到通过 WinRT API 邻近感应传感器。 但是，这些应用不会知道传感器，支持范围，并且可能会决定不使用传感器。

## <a name="related-topics"></a>相关主题


[EvtSensorGetDataFieldProperties](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)

[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






