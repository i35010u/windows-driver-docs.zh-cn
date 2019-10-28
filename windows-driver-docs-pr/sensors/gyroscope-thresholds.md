---
title: 陀螺仪阈值
description: 本主题提供有关陀螺仪阈值的信息。
ms.assetid: 68B11108-CA1A-4A49-BC44-4E9FE09955A9
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 09def43c8fa88f6b8ae882df5091aebce5889d77
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841685"
---
# <a name="gyroscope-thresholds"></a>陀螺仪阈值


本主题提供有关陀螺仪阈值的信息。

下表显示了陀螺仪的默认阈值。 有关 "类型" 列中显示的类型的详细信息，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|类型|必需/可选|默认值|说明|
|---|---|---|---|---|
|PKEY_SensorData_AngularVelocityX_DegreesPerSecond|VT_R4|需要|0.1 f|达到阈值时所需的围绕 x 轴的角度速度变化的最小值，以度/秒为单位。|
|PKEY_SensorData_AngularVelocityY_DegreesPerSecond|VT_R4|需要|0.1 f|达到阈值时所需的围绕 y 轴的角度速度变化的最小值，以度/秒为单位。|
|PKEY_SensorData_AngularVelocityZ_DegreesPerSecond|VT_R4|需要|0.1 f|达到达到阈值时所需的针对 z 轴的角度速度变化的最小值，以每秒度为单位进行度量。|

陀螺仪驱动程序必须在 PKEY_SensorData_AngularVelocityX_DegreesPerSecond、PKEY_SensorData_AngularVelocityY_DegreesPerSecond 或 PKEY_ 上通过调用[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensordataready)来报告对传感器类扩展的示例读取满足 SensorData_AngularVelocityZ_DegreesPerSecond 阈值。 每个阈值必须按轴测量。 因此，无论何时在任一轴上满足阈值条件，驱动程序都必须调用 SensorsCxSensorDataReady。
当 PKEY_SensorData_AngularVelocityX_DegreesPerSecond、PKEY_SensorData_AngularVelocityY_DegreesPerSecond 或 PKEY_SensorData_AngularVelocityZ_DegreesPerSecond 设置为 0.0 f 时，驱动程序必须将示例读取报告给传感器类每个间隔的扩展。 此模式称为*传感器示例流式处理*。

陀螺仪驱动程序必须始终在传感器类扩展调用[EvtSensorStart](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)回调之后报告一个示例读取，而不考虑阈值。 此示例称为称为初始示例读取。

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)







