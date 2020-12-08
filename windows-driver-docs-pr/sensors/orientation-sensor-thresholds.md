---
title: 方向传感器阈值
description: 本主题提供有关定向传感器阈值的信息。
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 37e6724bba5457b04c4fe55c82783a805962b534
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812277"
---
# <a name="orientation-sensor-thresholds"></a>方向传感器阈值


本主题提供有关定向传感器阈值的信息。

下表显示了方向传感器的可用阈值。 有关 "类型" 列中显示的类型的详细信息，请参阅 [PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)。

|属性键|类型|必需/可选|默认值|说明|
|---|---|---|---|---|
|PKEY_SensorData_RotationAngle_Degrees|VT_R4|必须|10.0 f|达到阈值所需的任何轴的最小方向角变化量（以度为单位）。 应将此值计算为两个四元数之间的角度。 从数学上来说，这表示为： 2 * cos-1 (点积 (q1，第2季度) # A3|
|PKEY_SensorData_LinearAccelerationX_Gs|VT_R4|可选|不适用|达到阈值时，所需的最小加速度增加或减小 x 轴，以 g 的度量。|
|PKEY_SensorData_LinearAccelerationY_Gs|VT_R4|可选|不适用|达到阈值时，所需的最小加速度量会增大或减小，并以 g 的度量。|
|PKEY_SensorData_LinearAccelerationZ_Gs|VT_R4|可选|不适用|达到阈值时，所需的最小加速度量会增大或减小，以 g 为单位。|
|PKEY_SensorData_CorrectedAngularVelocityX_DegreesPerSecond|VT_R4|可选|不适用|达到阈值时所需的围绕 x 轴的角度速度变化的最小值，以度/秒为单位。|
|PKEY_SensorData_CorrectedAngularVelocityY_DegreesPerSecond|VT_R4|可选|不适用|达到阈值时所需的围绕 x 轴的角度速度变化的最小值，以度/秒为单位。|
|PKEY_SensorData_CorrectedAngularVelocityZ_DegreesPerSecond|VT_R4|可选|不适用|达到阈值时所需的围绕 x 轴的角度速度变化的最小值，以度/秒为单位。|

方向传感器驱动程序必须在满足 PKEY_SensorData_RotationAngle_Degrees 阈值时，通过调用 [SensorsCxSensorDataReady](/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensordataready) 来报告对传感器类扩展的示例。

如果将 PKEY_SensorData_RotationAngle_Degrees 设置为 0.0 f，则驱动程序必须在每个间隔中向传感器类扩展报告样本读数。 此模式称为 *传感器示例流式处理*。

方向传感器驱动程序必须始终在传感器类扩展调用 [EvtSensorStart](/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config) 回调之后报告一个示例读取，而不考虑阈值。 此示例称为称为 *初始示例读取*。

当满足各自的阈值时，方向传感器驱动程序必须报告对传感器类扩展的示例。

如果驱动程序支持以下任何其他可选的可测量值，用于测量每个轴的读数，则必须公开相应轴的阈值：
* PKEY_SensorData_LinearAccelerationX_Gs
* PKEY_SensorData_LinearAccelerationY_Gs
* PKEY_SensorData_LinearAccelerationZ_Gs
* PKEY_SensorData_CorrectedAngularVelocityX_DegreesPerSecond
* PKEY_SensorData_CorrectedAngularVelocityY_DegreesPerSecond
* PKEY_SensorData_CorrectedAngularVelocityZ_DegreesPerSecond

因此，无论何时在任一轴上满足阈值条件，驱动程序都必须调用 SensorsCxSensorDataReady。

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)
