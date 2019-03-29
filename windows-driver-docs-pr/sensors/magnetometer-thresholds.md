---
title: 磁力计阈值
description: 本主题提供有关磁力仪阈值的信息。
ms.assetid: F245AD4C-F63C-48A7-9AEB-7414047E0627
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9ecaa0ae3e678b386eb87a1be195d3bf93cc8a1a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576361"
---
# <a name="magnetometer-thresholds"></a>磁力计阈值


本主题提供有关磁力仪阈值的信息。

下表显示了可用的阈值的值为磁力仪。 有关类型列中显示的类型的详细信息，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|在任务栏的搜索框中键入|必需/可选|默认值|描述|
|---|---|---|---|---|
|PKEY_SensorData_MagneticFieldStrengthX_Microteslas|VT_R4|必需|5.0f|沿 x 轴来达到阈值，以 microteslas 磁场更改的最小数量。|
|PKEY_SensorData_MagneticFieldStrengthY_Microteslas|VT_R4|必需|5.0f|沿 y 轴来达到阈值，以 microteslas 磁场更改的最小数量。|
|PKEY_SensorData_MagneticFieldStrengthZ_Microteslas|VT_R4|必需|5.0f|沿 z 轴来达到阈值，以 microteslas 磁场更改的最小数量。|

磁力仪驱动程序必须通过调用报告至传感器类扩展的示例读取[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensordataready)时任一 PKEY_SensorData_MagneticFieldStrengthX_Microteslas PKEY_SensorData_MagneticFieldStrengthY_Microteslas 或 PKEY_SensorData_MagneticFieldStrengthZ_Microteslas 阈值都得到满足。 每个阈值必须测量每个轴。 驱动程序因此必须调用 SensorsCxSensorDataReady 每当阈值条件满足任何一个轴上。
当 PKEY_SensorData_MagneticFieldStrengthX_Microteslas，或 PKEY_SensorData_MagneticFieldStrengthY_Microteslas 或 PKEY_SensorData_MagneticFieldStrengthZ_Microteslas 设置为 0.0f 时，该驱动程序必须报告示例读数到传感器类在每个间隔的扩展。 此模式称为*传感器示例流*。

磁力仪驱动程序必须始终报告一个示例读取传感器类扩展调用后立即[EvtSensorStart](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)回调而不考虑的阈值。 此示例称为嘿 *初始示例读取*。

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

 


