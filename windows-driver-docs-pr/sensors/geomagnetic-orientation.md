---
title: Geomagnetic 方向
description: 本主题提供有关特定于 geomagnetic 方向传感器的数据字段的信息。
ms.assetid: C164E5A9-A664-4EE5-91CE-918233DFFB6D
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 619f6a6b1b6609bc36ab07508fea5c2695538910
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555794"
---
# <a name="geomagnetic-orientation"></a>Geomagnetic 方向


本主题提供有关特定于 geomagnetic 方向传感器的数据字段的信息。

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
<th>说明/评论</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PKEY_SensorData_QuaternionW</p></td>
<td><p>VT_R4</p></td>
<td><p>必需</p></td>
<td><p>（而不是复数的虚部部分） 的真实系数。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorData_QuaternionX</p></td>
<td><p>VT_R4</p></td>
<td><p>必需</p></td>
<td><p>旋转轴向量的 X 分量。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_SensorData_QuaternionY</p></td>
<td><p>VT_R4</p></td>
<td><p>必需</p></td>
<td><p>旋转轴向量的 Y 分量。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorData_QuaternionZ</p></td>
<td><p>VT_R4</p></td>
<td><p>必需</p></td>
<td><p>旋转轴向量的 Z 分量。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_SensorData_DeclinationAngle_Degrees</p></td>
<td><p>VT_R4</p></td>
<td><p>必需</p></td>
<td><p>赤纬角度。 如果不支持，此类扩展会计算此值。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorData_RotationAngle_Degrees</p></td>
<td><p>VT_R4</p></td>
<td><p>所需的 Windows 10 移动版</p>
<p>适用于 Windows 10 桌面版 （主页、 专业版、 企业版和教育版） 的可选</p></td>
<td><p>旋转角度 （以度为单位）。</p>
<p>公开设备方向传感器的驱动程序应将此属性密钥用作阈值密钥。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






