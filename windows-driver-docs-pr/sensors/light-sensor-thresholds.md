---
title: 光传感器阈值
description: 本主题提供有关光线传感器阈值的信息。
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 72f5e6336e3a2440d3b44ece7509dfb6756d9610
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812309"
---
# <a name="light-sensor-thresholds"></a>光传感器阈值


本主题提供有关光线传感器阈值的信息。

下表显示了光传感器的驱动程序默认阈值。 光源传感器的默认间隔为 10 Hz。 有关 "类型" 列中显示的类型的详细信息，请参阅 [PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)。

|属性键|类型|必需/可选|默认值|说明|
|---|---|---|---|---|
|PKEY_SensorData_LightLevel_Lux|VT_R4|必须|0.25 f|达到阈值时所需的 illuminance 更改的最小值，以 lux 的百分比度量。 如果值为 0.25 f，则表示 illuminance 中的更改了25%。|
|PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference|VT_R4|可选|1.0f|达到阈值时所需的 illuminance 更改的最小值，以 lux 度量。 值为 1.0 f 表示 illuminance 中的 lux 更改。 <br>__注意：__ 强烈建议在便携设备上实施此阈值，因为它有助于降低环境轻型环境中的电池电量消耗。|
|PKEY_SensorData_LightChromaticityX|VT_R4|如果支持颜色，则为必需。 可选，否则|0.01 f|达到阈值时所需的 CIE 1931 x 颜色坐标的最小更改量，表示为绝对差值。|
|PKEY_SensorData_LightChromaticityY|VT_R4|如果支持颜色，则为必需。 可选，否则|0.01 f|达到阈值时所需的 CIE 1931 y 颜色坐标的最小更改量，以绝对差值表示。|
|PKEY_SensorData_LightTemperature_Kelvins|VT_R4|如果支持颜色，则为必需。 可选，否则|50.0 f|达到阈值时所需的光线温度的最小更改量，以开氏度量。|

光源传感器必须 *仅在 LUX 值更改时* 报告新数据示例。 此建议的报表模型可确保光线传感器不会重复报告新的数据样本，因为它处于完全暗、零 (0) LUX 环境中。

如果未提供 PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference，环境光线传感器驱动程序必须在满足 PKEY_SensorData_LightLevel_Lux 阈值时，通过调用 [SensorsCxSensorDataReady](/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensordataready) 来报告对传感器类扩展的示例读取。 PKEY_SensorData_LightLevel_Lux 阈值表示为 Lux 中的差异百分比。 例如，如果将此阈值设置为 0.25 f，并且向传感器类扩展报告的最后一个样本为 40 lux，则报告的下一个示例应低于 30 lux 或大于 50 lux (+/-25% 的 40) 。
如果除了 PKEY_SensorData_LightLevel_Lux 之外还提供了 PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference，环境光线传感器必须报告对传感器类扩展的示例读取（如果 __同时满足这两个__ 阈值）。 例如，如果将 PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference 设置为 4.0 Lux，并将 PKEY_SensorData_LightLevel_Lux 设置为 0.25 (即 25% ) 并且向传感器类扩展报告的最后一个样本读数的值为 4 Lux，则最严格的阈值为 PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference。 因此，要报告的下一个样本读数应为 0 lux 或 8 lux。
相对来说，如果 PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference 设置为 4.0 Lux 并且 PKEY_SensorData_LightLevel_Lux 设置为 0.25 (即 25% ) 但向传感器类扩展报告的最后一个示例读数的值为 40 Lux，则最严格的阈值为 PKEY_SensorData_LightLevel_Lux。 在这种情况下，要报告的下一个样本读数应为 30 lux 或 50 lux。
永远不会设置 PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference，PKEY_SensorData_LightLevel_Lux。

当传感器驱动程序报告 Chromaticity x 和 Chromaticity y 颜色组件时，环境光线传感器驱动程序还必须支持 PKEY_SensorData_LightChromaticityX、PKEY_SensorData_LightChromaticityY 和 PKEY_SensorData_LightTemperature_Kelvins 阈值。
环境光线传感器驱动程序会在满足 PKEY_SensorData_LightChromaticityX、PKEY_SensorData_LightChromaticityY 或 PKEY_SensorData_LightTemperature_Kelvins 阈值时报告对传感器类扩展的示例。

环境光线传感器驱动程序必须始终在传感器类扩展调用 [EvtSensorStart](/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config) 回调之后报告一个示例读取，而不考虑阈值。 此示例称为初始示例读取。

>**注意**   当 IsValid 数据字段发生更改时，环境光线传感器驱动程序还必须报告对传感器类扩展的示例读取，而不考虑所设置的阈值。

当 PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference 和 PKEY_SensorData_LightLevel_Lux 设置为 0.0 f 时，驱动程序必须在每个间隔中向传感器类扩展报告样本读数。
如果 PKEY_SensorData_LightChromaticityX __或__ PKEY_SensorData_LightChromaticityY __或__ PKEY_SensorData_LightTemperature_Kelvins 设置为 0.0 f，则驱动程序必须在每个间隔将示例读取报告给传感器类扩展。
报告每个间隔的传感器示例称为 *传感器示例流式处理*。

>[!NOTE]
> 在阈值模式下，不报告将 PKEY \_ SensorData \_ IsValid 设置为 FALSE 的连续示例。 换句话说，在阈值模式下，仅发送第一个示例，其中 PKEY \_ SensorData \_ IsValid 已切换为 FALSE。
 

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)
