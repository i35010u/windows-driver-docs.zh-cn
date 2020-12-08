---
title: 传感器 \_ 类别 \_ 运动
description: 传感器 \_ 类别 \_ 运动类别包含的传感器提供与物理移动相关的信息。
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
ms.openlocfilehash: 4b7f5ef357c5098b0cf657fd3ae5beec1d51da0d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812195"
---
# <a name="sensor_category_motion"></a>传感器 \_ 类别 \_ 运动


传感器 \_ 类别 \_ 运动类别包含的传感器提供与物理移动相关的信息。 加速感应器衡量传感器的加速度，包括 gravitational 加速。 运动检测程序，例如安全系统中的人机移动检测、对移动对象的意义。 角度速度变化的 Gyrometers。 里程表度量速度。

### <a name="span-idplatform_defined_sensor_typesspanspan-idplatform_defined_sensor_typesspanplatform-defined-sensor-types"></a><span id="platform_defined_sensor_types"></span><span id="PLATFORM_DEFINED_SENSOR_TYPES"></span>平台定义的传感器类型

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
<td><p>单轴加速感应器。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_ACCELEROMETER_2D</p></td>
<td><p>两轴加速感应器。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_TYPE_ACCELEROMETER_3D</p></td>
<td><p>三轴加速感应器。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_GYROMETER_1D</p></td>
<td><p>单轴 gyrometers。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_TYPE_GYROMETER_2D</p></td>
<td><p>两轴 gyrometers。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_GYROMETER_3D</p></td>
<td><p>三轴 gyrometers。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_TYPE_MOTION_DETECTOR</p></td>
<td><p>运动检测程序，例如安全系统中使用的。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_SPEEDOMETER</p></td>
<td><p>运动频率传感器。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idplatform_defined_data_fieldsspanspan-idplatform_defined_data_fieldsspanplatform-defined-data-fields"></a><span id="platform_defined_data_fields"></span><span id="PLATFORM_DEFINED_DATA_FIELDS"></span>平台定义的数据字段

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
<th>类型</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_ACCELERATION_X_G</p></td>
<td><p>VT_R8</p></td>
<td><p>X 轴加速，在 <em>g</em>s 中。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_ACCELERATION_Y_G</p></td>
<td><p>VT_R8</p></td>
<td><p>Y 轴加速，在 <em>g</em>s 中。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_ACCELERATION_Z_G</p></td>
<td><p>VT_R8</p></td>
<td><p>Z 轴加速，在 <em>g</em>s 中。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_ANGULAR_ACCELERATION_X_DEGREES_PER_SECOND</p></td>
<td><p>VT_R8</p></td>
<td><p>Gyrometric x 轴加速度，以度/秒为单位。 平方.</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_ANGULAR_ACCELERATION_Y_DEGREES_PER_SECOND</p></td>
<td><p>VT_R8</p></td>
<td><p>Gyrometric y 轴加速度，以度/秒为单位。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_ANGULAR_ACCELERATION_Z_DEGREES_PER_SECOND</p></td>
<td><p>VT_R8</p></td>
<td><p>Gyrometric z 轴加速度，以度/秒为单位。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_ANGULAR_VELOCITY_X_DEGREES_PER_SECOND</p></td>
<td><p>VT_R8</p></td>
<td><p>Gyrometric x 轴速度，以度/秒为单位。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Y_DEGREES_PER_SECOND</p></td>
<td><p>VT_R8</p></td>
<td><p>Gyrometric y 轴速度，以度/秒为单位。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Z_DEGREES_PER_SECOND</p></td>
<td><p>VT_R8</p></td>
<td><p>Gyrometric z 轴速度，以度/秒为单位。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_MOTION_STATE</p></td>
<td><p>VT_BOOL</p></td>
<td><p><strong>VARIANT_TRUE</strong> 如果检测到动作，则为; 否则 <strong>VARIANT_FALSE</strong>。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_SPEED_METERS_PER_SECOND</p></td>
<td><p>VT_R8</p></td>
<td><p>速度以米/秒为单位。</p></td>
</tr>
</tbody>
</table>

 

**重要提示**  每个平台定义的运动数据类型 **PROPERTYKEY** 均基于一个名为 "传感器 **GUID** \_ 数据 \_ 类型 \_ 运动 GUID" 的通用 GUID \_ 。 由于这是保留的基值，请不要使用此 **GUID** 来定义自己的属性键。

 

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
<td><p>Windows 7</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>无受支持的版本</p></td>
</tr>
<tr class="odd">
<td><p>版本</p></td>
<td><p>适用于 Windows 7。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>传感器。h</td>
</tr>
</tbody>
</table>

 

 





