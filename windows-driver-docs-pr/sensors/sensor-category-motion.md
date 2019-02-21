---
title: 传感器\_类别\_运动
description: 传感器\_类别\_运动类别包含提供与物理移动相关的信息的传感器。
ms.assetid: 9189aefc-e92d-483c-80da-f61339b14ebd
keywords:
- SENSOR_CATEGORY_MOTION 传感器设备
topic_type:
- apiref
api_name:
- SENSOR_CATEGORY_MOTION
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: cabb7b6cef6f0c1be87675db5aede006f18b213c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543759"
---
# <a name="sensorcategorymotion"></a>传感器\_类别\_运动


传感器\_类别\_运动类别包含提供与物理移动相关的信息的传感器。 加速感应器度量值的传感器，包括引力加速的加速。 运动检测程序，例如在安全系统中，移动对象的有意义的人体运动检测。 Gyrometers 感应角速度中的更改。 里程表测量速度。

### <a name="span-idplatformdefinedsensortypesspanspan-idplatformdefinedsensortypesspanplatform-defined-sensor-types"></a><span id="platform_defined_sensor_types"></span><span id="PLATFORM_DEFINED_SENSOR_TYPES"></span>平台定义的传感器类型

此类别包括以下平台定义的传感器类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>传感器类型</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SENSOR_TYPE_ACCELEROMETER_1D</p></td>
<td><p>一个轴加速感应器。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_ACCELEROMETER_2D</p></td>
<td><p>两个轴加速感应器。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_TYPE_ACCELEROMETER_3D</p></td>
<td><p>三个轴加速感应器。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_GYROMETER_1D</p></td>
<td><p>一个轴 gyrometers。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_TYPE_GYROMETER_2D</p></td>
<td><p>两个轴 gyrometers。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_GYROMETER_3D</p></td>
<td><p>三个轴 gyrometers。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_TYPE_MOTION_DETECTOR</p></td>
<td><p>运动检测程序，如安全系统中使用。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_SPEEDOMETER</p></td>
<td><p>速率的运动传感器。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idplatformdefineddatafieldsspanspan-idplatformdefineddatafieldsspanplatform-defined-data-fields"></a><span id="platform_defined_data_fields"></span><span id="PLATFORM_DEFINED_DATA_FIELDS"></span>平台定义的数据字段

此类别包括以下平台定义的数据字段。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>数据类型</th>
<th>在任务栏的搜索框中键入</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_ACCELERATION_X_G</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>X 轴加速，请在<em>g</em>s。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_ACCELERATION_Y_G</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>Y 轴加速，请在<em>g</em>s。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_ACCELERATION_Z_G</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>Z 轴加速，请在<em>g</em>s。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_ANGULAR_ACCELERATION_X_DEGREES_PER_SECOND</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>Gyrometric x 轴的加速，以度为单位每秒。 平方值。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_ANGULAR_ACCELERATION_Y_DEGREES_PER_SECOND</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>Gyrometric y 轴加速，以度为单位每秒平方值。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_ANGULAR_ACCELERATION_Z_DEGREES_PER_SECOND</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>Gyrometric z 轴加速，以度为单位每秒平方值。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_ANGULAR_VELOCITY_X_DEGREES_PER_SECOND</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>Gyrometric x 轴方向，以度为单位每秒的速度。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Y_DEGREES_PER_SECOND</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>Gyrometric y 轴方向，以度为单位每秒的速度。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Z_DEGREES_PER_SECOND</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>Gyrometric z 轴方向，以度为单位每秒的速度。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_MOTION_STATE</p></td>
<td><p><strong>VT_BOOL</strong></p></td>
<td><p><strong>VARIANT_TRUE</strong>如果检测到动作，否则<strong>VARIANT_FALSE</strong>。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_SPEED_METERS_PER_SECOND</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>速度以米 / 秒为单位。</p></td>
</tr>
</tbody>
</table>

 

**重要**  每个平台定义动作数据类型**PROPERTYKEY**基于一种常见**GUID**名为传感器\_数据\_类型\_运动\_GUID。 由于它是保留的基值，请勿使用此**GUID**来定义你自己属性的密钥。

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 7</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>无受支持的版本</p></td>
</tr>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows 7 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Sensors.h</td>
</tr>
</tbody>
</table>

 

 





