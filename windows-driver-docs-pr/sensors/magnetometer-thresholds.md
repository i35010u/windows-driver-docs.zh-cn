---
title: 磁力计阈值
description: 本主题提供有关磁力仪阈值的信息。
ms.assetid: F245AD4C-F63C-48A7-9AEB-7414047E0627
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: a8a6e84a0c3aa9d7a2a295c2e6200f55c24efc43
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010217"
---
# <a name="magnetometer-thresholds"></a>磁力计阈值


本主题提供有关磁力仪阈值的信息。

下表显示了磁力仪的可用阈值。 有关 "类型" 列中显示的类型的详细信息，请参阅 [PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|类型|必需/可选|默认值|说明|
|---|---|---|---|---|
|PKEY_SensorData_MagneticFieldStrengthX_Microteslas|VT_R4|必需|5.0 f|达到阈值时所需的最小磁性字段变化量（以 microteslas 为单位）。|
|PKEY_SensorData_MagneticFieldStrengthY_Microteslas|VT_R4|必需|5.0 f|达到阈值时，需要沿 y 轴的最小磁场变化量，以 microteslas 度量。|
|PKEY_SensorData_MagneticFieldStrengthZ_Microteslas|VT_R4|必需|5.0 f|达到阈值时所需的区域的最小磁场变化量（以 microteslas 为单位）。|

磁力仪驱动程序必须在满足 PKEY_SensorData_MagneticFieldStrengthX_Microteslas、PKEY_SensorData_MagneticFieldStrengthY_Microteslas 或 PKEY_SensorData_MagneticFieldStrengthZ_Microteslas 阈值时，通过调用 [SensorsCxSensorDataReady](/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensordataready) 来报告读取传感器类扩展的示例。 每个阈值必须按轴测量。 因此，无论何时在任一轴上满足阈值条件，驱动程序都必须调用 SensorsCxSensorDataReady。
当 PKEY_SensorData_MagneticFieldStrengthX_Microteslas、PKEY_SensorData_MagneticFieldStrengthY_Microteslas 或 PKEY_SensorData_MagneticFieldStrengthZ_Microteslas 设置为 0.0 f 时，驱动程序必须在每个间隔将示例读取报告给传感器类扩展。 此模式称为 *传感器示例流式处理*。

磁力仪驱动程序必须始终在传感器类扩展调用 [EvtSensorStart](/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config) 回调之后报告一个示例读取，而不考虑阈值。 此示例称为称为 *初始示例读取*。

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

