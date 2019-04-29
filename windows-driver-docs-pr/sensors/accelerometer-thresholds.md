---
title: 加速计阈值
description: 本主题提供有关加速感应器阈值的信息。
ms.assetid: 7BB8B087-6CE5-4BD2-9286-350AE607B1D7
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6715820e6eb21af2b4452bfa9d00b67078c9f655
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360930"
---
# <a name="accelerometer-thresholds"></a>加速计阈值


本主题提供有关加速感应器阈值的信息。

下表列出了可用的阈值的值的加速感应器。 有关类型列中显示的类型的详细信息，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|在任务栏的搜索框中键入|必需/可选|默认值|描述|
|---|---|---|---|---|
|PKEY_SensorData_AccelerationX_Gs|VT_R4|必需|0.1f|加速增加或减少所需达到的阈值，在 x 轴的最小量，以 g's 单位|
|PKEY_SensorData_AccelerationY_Gs|VT_R4|必需|0.1f|加速增加或减少所需达到的阈值，在 y 轴的最小量，以 g's 单位|
|PKEY_SensorData_AccelerationZ_Gs|VT_R4|必需|0.1f|加速增加或减少沿 z 轴达到阈值，所需的最小量，以 g's 单位|

加速感应器驱动程序必须通过调用报告至传感器类扩展的示例读取[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensordataready)时 PKEY_SensorData_AccelerationX_Gs、 PKEY_SensorData_AccelerationY_Gs 或 PKEY_SensorData_在达到 AccelerationZ_Gs 阈值。 每个阈值必须测量每个轴。 驱动程序因此必须调用 SensorsCxSensorDataReady 每当阈值条件满足任何一个轴上。
当 PKEY_SensorData_AccelerationX_Gs，或 PKEY_SensorData_AccelerationY_Gs 或 PKEY_SensorData_AccelerationZ_Gs 设置为 0.0f 时，驱动程序必须在每个单个间隔报告至传感器类扩展的示例读数。 此模式称为*传感器示例流*。

加速感应器驱动程序必须始终报告一个示例读取传感器类扩展调用后立即[EvtSensorStart](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)回调而不考虑的阈值。 此示例称为嘿 *初始示例读取*。

>[!NOTE]
>加速感应器驱动程序还必须报告 PKEY_SensorData_Shake 数据字段的更改 （如果支持），而不考虑所设置的阈值时读取至传感器类扩展的示例。

## <a name="related-topics"></a>相关主题

[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)


