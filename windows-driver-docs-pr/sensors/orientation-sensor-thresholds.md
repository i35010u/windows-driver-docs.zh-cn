---
title: 方向传感器阈值
description: 本主题提供有关方向信息传感器的阈值。
ms.assetid: BC7B76C3-F6D3-48FC-AA22-A91519A0A0D8
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 197be6f9e5bf76ba634d3d58a14bf747badc9b1e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330099"
---
# <a name="orientation-sensor-thresholds"></a>方向传感器阈值


本主题提供有关方向信息传感器的阈值。

下表显示了可用的阈值的值的方向传感器。 有关类型列中显示的类型的详细信息，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|在任务栏的搜索框中键入|必需/可选|默认值|描述|
|---|---|---|---|---|
|PKEY_SensorData_RotationAngle_Degrees|VT_R4|必需|10.0f|方向角度更改围绕所需达到的阈值，以度为单位测量任何轴的最小数量。 应为两个四元数之间的角度计算此值。 从数学上，这表示为：2*cos-1 (dot product(q1, q2))|
|PKEY_SensorData_LinearAccelerationX_Gs|VT_R4|可选|不适用|加速增加或减少所需达到的阈值，在 x 轴的最小量，以 g's 单位|
|PKEY_SensorData_LinearAccelerationY_Gs|VT_R4|可选|不适用|加速增加或减少所需达到的阈值，在 y 轴的最小量，以 g's 单位|
|PKEY_SensorData_LinearAccelerationZ_Gs|VT_R4|可选|不适用|加速增加或减少沿 z 轴达到阈值，所需的最小量，以 g's 单位|
|PKEY_SensorData_CorrectedAngularVelocityX_DegreesPerSecond|VT_R4|可选|不适用|更改围绕 x 轴来达到阈值，以度 / 秒为单位的最小数量。|
|PKEY_SensorData_CorrectedAngularVelocityY_DegreesPerSecond|VT_R4|可选|不适用|更改围绕 x 轴来达到阈值，以度 / 秒为单位的最小数量。|
|PKEY_SensorData_CorrectedAngularVelocityZ_DegreesPerSecond|VT_R4|可选|不适用|更改围绕 x 轴来达到阈值，以度 / 秒为单位的最小数量。|

方向传感器驱动程序必须报告的示例通过调用读取至传感器类扩展[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensordataready)满足 PKEY_SensorData_RotationAngle_Degrees 阈值时。

当 PKEY_SensorData_RotationAngle_Degrees 设置为 0.0f 时，该驱动程序必须在每个时间间隔报告至传感器类扩展的示例读数。 此模式称为*传感器示例流*。

方向传感器驱动程序必须始终报告一个示例读取传感器类扩展调用后立即[EvtSensorStart](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)回调而不考虑的阈值。 此示例称为嘿 *初始示例读取*。

方向传感器驱动程序必须报告读取至传感器类扩展，满足各自的阈值时的示例：

* PKEY_SensorData_LinearAccelerationX_Gs
* PKEY_SensorData_LinearAccelerationY_Gs
* PKEY_SensorData_LinearAccelerationZ_Gs
* PKEY_SensorData_CorrectedAngularVelocityX_DegreesPerSecond
* PKEY_SensorData_CorrectedAngularVelocityY_DegreesPerSecond
* PKEY_SensorData_CorrectedAngularVelocityZ_DegreesPerSecond

每个阈值必须测量每个轴。 驱动程序因此必须调用 SensorsCxSensorDataReady 每当阈值条件满足任何一个轴上。

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

