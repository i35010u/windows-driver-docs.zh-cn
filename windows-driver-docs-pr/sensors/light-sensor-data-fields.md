---
title: 光线传感器数据字段
description: 本主题提供有关特定于光线传感器的数据字段的信息。
ms.assetid: 96572A6A-CACC-4B79-B63C-5554C07F7C83
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1f731ab9f09c2776063f610fbc653d7ae78d7f60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546741"
---
# <a name="light-sensor-data-fields"></a>光线传感器数据字段


本主题提供有关特定于光线传感器的数据字段的信息。

下表显示数据字段。 有关类型列中显示的类型的详细信息，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

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
<th>在任务栏的搜索框中键入</th>
<th>必需/可选</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PKEY_SensorData_LightLevel_Lux</p></td>
<td><p>VT_R4</p></td>
<td><p>必需</p></td>
<td><p>Lux illuminance 级别。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorData_LightTemperature_Kelvins</p></td>
<td><p>VT_R4</p></td>
<td><p>可选</p></td>
<td><p>开氏浅温度。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_SensorData_LightChromaticityX</p></td>
<td><p>VT_R4</p></td>
<td><p>可选</p></td>
<td><p>X 颜色协调 CIE 1931 色度关系图上。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorData_LightChromaticityY</p></td>
<td><p>VT_R4</p></td>
<td><p>可选</p></td>
<td><p>Y 颜色协调 CIE 1931 色度关系图上。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorData_IsValid</p></td>
<td><p>VT_BOOL</p></td>
<td><p>可选</p></td>
<td><p>当环境光线传感器目前不能返回任何有效的示例时，此值必须设置为 FALSE。 例如，此值可能设置为 FALSE 时 （例如，当对象或用户手动为传感器的前面） 挡住传感器的视野。 环境光线传感器可以准确衡量环境光线时，此值应设置为 TRUE。 适当的硬件设计应尝试尽量减少时间和需要此值可设置为 FALSE，这种方案方案导致系统无法正确地控制亮度。 在理想的系统，此值始终设置为 TRUE。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题


[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






