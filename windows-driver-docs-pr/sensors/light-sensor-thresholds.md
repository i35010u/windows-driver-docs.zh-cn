---
title: 光线传感器的阈值
description: 本主题提供有关光线传感器阈值的信息。
ms.assetid: A120601A-A5CE-4778-94A9-97E71B721E9B
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: f87faf112f72635362704fe06e3ce5b82f38745f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541231"
---
# <a name="light-sensor-thresholds"></a>光线传感器的阈值


本主题提供有关光线传感器阈值的信息。

下表列出了光线传感器的驱动程序的默认阈值。 光线传感器的默认间隔为 10 Hz。 有关类型列中显示的类型的详细信息，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|在任务栏的搜索框中键入|必需/可选|默认值|描述|
|---|---|---|---|---|
|PKEY_SensorData_LightLevel_Lux|VT_R4|必需|0.25f|最小的 illuminance 达到阈值，以百分比的 lux 度量所需的更改量。 值为 0.25f 表示 illuminance 的 25%更改。|
|PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference|VT_R4|可选|1.0f|最小的 illuminance 达到阈值，以 lux 度量所需的更改量。 值为 1.0 f 表示 1 lux illuminance 中更改。 <br>__注意：__ 实现此阈值是强烈建议在便携设备上因为，从而帮助降低电池电量低环境光线环境中。|
|PKEY_SensorData_LightChromaticityX|VT_R4|所需颜色受支持。 否则为可选|0.01f|最小 x 达到阈值，表示为绝对差异所需的颜色坐标 CIE 1931 更改量。|
|PKEY_SensorData_LightChromaticityY|VT_R4|所需颜色受支持。 否则为可选|0.01f|更改所需达到的阈值，表示为绝对差异的 CIE 1931 y 颜色坐标的最小数量。|
|PKEY_SensorData_LightTemperature_Kelvins|VT_R4|所需颜色受支持。 否则为可选|50.0f|最小所需达到的阈值，以开氏度为单位的轻型温度更改量。|

光线传感器必须报告新数据样本*LUX 值发生更改时，才*。 建议使用此报表模型可确保，光线传感器不会报告新数据示例重复在完全深色时，零 (0) LUX 环境。

如果未提供 PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference，环境光线传感器驱动程序必须通过调用报告至传感器类扩展的示例读取[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensordataready)时 PKEY_达到 SensorData_LightLevel_Lux 阈值。 PKEY_SensorData_LightLevel_Lux 阈值表示为占 lux 的差异。 例如，如果此阈值设置为 0.25f 并报告给传感器类扩展的最后一个示例是 40 lux 下, 一个示例报告应是低于 30 lux 或大于 50 lux （+ /-为 40 25%)。
如果除了 PKEY_SensorData_LightLevel_Lux 提供 PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference，则环境光线传感器必须报告示例读取至传感器类扩展如果__同时__在达到阈值。 例如，如果 PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference 设置为 4.0 lux 并且 PKEY_SensorData_LightLevel_Lux 设置为 0.25 （即 25%)而且在最后一个样本读取的值报告给传感器类扩展是 4 lux，限制性最强的阈值时 PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference。 因此下, 一步的示例读取，报告应为 0 的 lux 或 8 lux。
相对来说，如果 PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference 设置为 4.0 lux 并且 PKEY_SensorData_LightLevel_Lux 设置为 0.25 （即 25%)但最后一个样本读取的值报告给传感器类扩展是 40 lux，限制性最强的阈值为 PKEY_SensorData_LightLevel_Lux。 在这种情况下下, 一步的示例读取，报告应为 30 lux 或 50 lux。
没有 PKEY_SensorData_LightLevel_Lux 永远不会设置 PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference。

当传感器驱动程序报告了色度 x 和色度 y 分量，环境光线传感器驱动程序还必须支持 PKEY_SensorData_LightChromaticityX、 PKEY_SensorData_LightChromaticityY 和 PKEY_SensorData_LightTemperature_Kelvins阈值。
环境光线传感器驱动程序报告读取至传感器类扩展，满足 PKEY_SensorData_LightChromaticityX、 PKEY_SensorData_LightChromaticityY 或 PKEY_SensorData_LightTemperature_Kelvins 阈值时的示例。

环境光线传感器驱动程序必须始终报告一个示例读取传感器类扩展调用后立即[EvtSensorStart](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)回调而不考虑的阈值。 此示例称为初始示例读取。

>**请注意**  环境光线传感器驱动程序还必须报告 IsValid 数据字段的更改，而不考虑所设置的阈值时读取至传感器类扩展的示例。

当 PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference 和 PKEY_SensorData_LightLevel_Lux 设置为 0.0f 时，驱动程序必须在每个时间间隔报告至传感器类扩展的示例读数。
当 PKEY_SensorData_LightChromaticityX__或__PKEY_SensorData_LightChromaticityY__或__PKEY_SensorData_LightTemperature_Kelvins 设置为 0.0f，该驱动程序必须报告为示例读数在每个时间间隔的传感器类扩展。
在每个间隔中报告的传感器示例被称为*传感器示例流*。

>[!NOTE]
> 在阈值模式下，不会报告具有主键的连续样本\_SensorData\_IsValid 设置为 FALSE。 换而言之，在阈值模式下，只发送第一个示例中的主键\_SensorData\_IsValid 切换为 FALSE。
 

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

 






