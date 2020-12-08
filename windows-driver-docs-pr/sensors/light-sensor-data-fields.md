---
title: 光传感器数据字段
description: 本主题提供有关特定于光源传感器的数据字段的信息。
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 64b554d597b3642e303ea84681124ab57b0cd5b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812311"
---
# <a name="light-sensor-data-fields"></a>光传感器数据字段


本主题提供有关特定于光源传感器的数据字段的信息。

下表显示了数据字段。 有关 "类型" 列中显示的类型的详细信息，请参阅 [PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性键</th>
<th>类型</th>
<th>必需/可选</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PKEY_SensorData_LightLevel_Lux</p></td>
<td><p>VT_R4</p></td>
<td><p>必须</p></td>
<td><p>Lux 中的 illuminance 级别。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorData_LightTemperature_Kelvins</p></td>
<td><p>VT_R4</p></td>
<td><p>可选</p></td>
<td><p>开氏中的温度较低。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_SensorData_LightChromaticityX</p></td>
<td><p>VT_R4</p></td>
<td><p>可选</p></td>
<td><p>CIE 1931 chromaticity 关系图上的 x 颜色坐标。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorData_LightChromaticityY</p></td>
<td><p>VT_R4</p></td>
<td><p>可选</p></td>
<td><p>CIE 1931 chromaticity 关系图上的 y 颜色坐标。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorData_IsValid</p></td>
<td><p>VT_BOOL</p></td>
<td><p>可选</p></td>
<td><p>当环境光线传感器当前无法返回任何有效的样本时，此值必须设置为 FALSE。 例如，当视图的 "传感器" 字段为 "受阻" 时，此值可能设置为 "FALSE" (例如，当对象或用户手头位于传感器) 之前。 当环境光线传感器能够准确测量环境光线时，此值应设置为 TRUE。 适当的硬件设计应尽量缩短需要此值设置为 FALSE 的时间和方案，因为这种情况会导致系统无法正确控制亮度。 在理想的系统上，此值始终设置为 TRUE。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)

 

