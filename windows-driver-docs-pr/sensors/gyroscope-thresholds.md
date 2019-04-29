---
title: 陀螺仪阈值
description: 本主题提供有关陀螺仪阈值的信息。
ms.assetid: 68B11108-CA1A-4A49-BC44-4E9FE09955A9
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: dadbee3a04b7d89e7d2f33e1cb7e7ce26ca86b59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366510"
---
# <a name="gyroscope-thresholds"></a>陀螺仪阈值


本主题提供有关陀螺仪阈值的信息。

下表显示了陀螺仪的默认阈值。 有关类型列中显示的类型的详细信息，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|在任务栏的搜索框中键入|必需/可选|默认值|描述|
|---|---|---|---|---|
|PKEY_SensorData_AngularVelocityX_DegreesPerSecond|VT_R4|必需|0.1f|更改围绕 x 轴来达到阈值，以度 / 秒为单位的最小数量。|
|PKEY_SensorData_AngularVelocityY_DegreesPerSecond|VT_R4|必需|0.1f|更改围绕 y 轴来达到阈值，以度 / 秒为单位的最小数量。|
|PKEY_SensorData_AngularVelocityZ_DegreesPerSecond|VT_R4|必需|0.1f|更改围绕 z 轴来达到阈值，以度 / 秒为单位的最小数量。|

陀螺仪驱动程序必须通过调用报告至传感器类扩展的示例读取[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensordataready)时任一 PKEY_SensorData_AngularVelocityX_DegreesPerSecond PKEY_SensorData_AngularVelocityY_DegreesPerSecond 或 PKEY_SensorData_AngularVelocityZ_DegreesPerSecond 阈值都得到满足。 每个阈值必须测量每个轴。 驱动程序因此必须调用 SensorsCxSensorDataReady 每当阈值条件满足任何一个轴上。
当 PKEY_SensorData_AngularVelocityX_DegreesPerSecond，或 PKEY_SensorData_AngularVelocityY_DegreesPerSecond 或 PKEY_SensorData_AngularVelocityZ_DegreesPerSecond 设置为 0.0f 时，该驱动程序必须报告示例读数到传感器类在每个间隔的扩展。 此模式称为*传感器示例流*。

陀螺仪驱动程序必须始终报告一个示例读取传感器类扩展调用后立即[EvtSensorStart](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)回调而不考虑的阈值。 此示例称为初始示例读取称为。

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)







