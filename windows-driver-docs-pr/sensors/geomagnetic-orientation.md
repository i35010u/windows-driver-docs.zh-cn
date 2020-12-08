---
title: 磁场方向
description: 本主题提供有关特定于磁场方向传感器的数据字段的信息。
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: a6ee68545cde799549c8c6674d1b4b01b815894e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812321"
---
# <a name="geomagnetic-orientation"></a>地磁方向


本主题提供有关特定于磁场方向传感器的数据字段的信息。

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
<th>说明/注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PKEY_SensorData_QuaternionW</p></td>
<td><p>VT_R4</p></td>
<td><p>必须</p></td>
<td><p>实系数 (相对于复数的虚部) 。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorData_QuaternionX</p></td>
<td><p>VT_R4</p></td>
<td><p>必须</p></td>
<td><p>旋转轴向量的 X 分量。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_SensorData_QuaternionY</p></td>
<td><p>VT_R4</p></td>
<td><p>必须</p></td>
<td><p>旋转轴向量的 Y 分量。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorData_QuaternionZ</p></td>
<td><p>VT_R4</p></td>
<td><p>必须</p></td>
<td><p>旋转轴向量的 Z 分量。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_SensorData_DeclinationAngle_Degrees</p></td>
<td><p>VT_R4</p></td>
<td><p>必须</p></td>
<td><p>赤纬角。 如果不支持，类扩展将计算此值。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorData_RotationAngle_Degrees</p></td>
<td><p>VT_R4</p></td>
<td><p>对于 Windows 10 移动版是必需的</p>
<p>适用于适用于桌面版的 Windows 10 (Home、Pro、Enterprise 和教育) </p></td>
<td><p>旋转角度（以度为单位）。</p>
<p>公开设备方向传感器的驱动程序应将此属性键用于阈值键。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PROPVARIANT 结构](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)

 

