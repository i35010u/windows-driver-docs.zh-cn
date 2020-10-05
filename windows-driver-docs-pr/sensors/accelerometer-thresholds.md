---
title: 加速计阈值
description: 本主题提供有关加速度阈值的信息。
ms.assetid: 7BB8B087-6CE5-4BD2-9286-350AE607B1D7
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2119aa733a154ab0da1468883d30693f9e3603ca
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734417"
---
# <a name="accelerometer-thresholds"></a>加速计阈值


本主题提供有关加速度阈值的信息。

下表列出了加速感应的可用阈值。 有关 "类型" 列中显示的类型的详细信息，请参阅 [PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)。

|属性键|类型|必需/可选|默认值|说明|
|---|---|---|---|---|
|PKEY_SensorData_AccelerationX_Gs|VT_R4|必须|0.1 f|达到阈值时，所需的最小加速度增加或减小 x 轴，以 g 的度量。|
|PKEY_SensorData_AccelerationY_Gs|VT_R4|必须|0.1 f|达到阈值时，所需的最小加速度量会增大或减小，并以 g 的度量。|
|PKEY_SensorData_AccelerationZ_Gs|VT_R4|必须|0.1 f|达到阈值时，所需的最小加速度量会增大或减小，以 g 为单位。|

加速感应驱动程序必须在满足 PKEY_SensorData_AccelerationX_Gs、PKEY_SensorData_AccelerationY_Gs 或 PKEY_SensorData_AccelerationZ_Gs 阈值时，通过调用 [SensorsCxSensorDataReady](/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensordataready) 来报告对传感器类扩展的示例。 每个阈值必须按轴测量。 因此，无论何时在任一轴上满足阈值条件，驱动程序都必须调用 SensorsCxSensorDataReady。
当 PKEY_SensorData_AccelerationX_Gs、PKEY_SensorData_AccelerationY_Gs 或 PKEY_SensorData_AccelerationZ_Gs 设置为 0.0 f 时，驱动程序必须在每个间隔中向传感器类扩展报告示例读取。 此模式称为 *传感器示例流式处理*。

加速感应程序必须始终在传感器类扩展调用 [EvtSensorStart](/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config) 回调之后报告一个示例读取，而不考虑阈值。 此示例称为称为 *初始示例读取*。

>[!NOTE]
>如果 PKEY_SensorData_Shake 数据字段发生更改时，加速感应器驱动程序还必须报告对传感器类扩展的示例 () ，而不考虑所设置的阈值。

## <a name="related-topics"></a>相关主题

[PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)