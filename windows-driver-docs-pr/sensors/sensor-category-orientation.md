---
title: 传感器\_类别\_方向
description: 传感器\_类别\_方向类别包含提供有关物理方向信息的传感器。
ms.assetid: F8089596-C68F-48B2-B4EF-FB7B8777F212
topic_type:
- apiref
api_name:
- SENSOR_TYPE_AGGREGATED_DEVICE_ORIENTATION
- SENSOR_TYPE_AGGREGATED_QUADRANT_ORIENTATION
- SENSOR_TYPE_AGGREGATED_SIMPLE_DEVICE_ORIENTATION
- SENSOR_TYPE_COMPASS_1D
- SENSOR_TYPE_COMPASS_2D
- SENSOR_TYPE_COMPASS_3D
- SENSOR_TYPE_DISTANCE_1D
- SENSOR_TYPE_DISTANCE_2D
- SENSOR_TYPE_DISTANCE_3D
- SENSOR_TYPE_INCLINOMETER_1D
- SENSOR_TYPE_INCLINOMETER_2D
- SENSOR_TYPE_INCLINOMETER_3D
- SENSOR_DATA_TYPE_ANGULAR_VELOCITY_X_DEGREES_PER_SECOND
- SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Y_DEGREES_PER_SECOND
- SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Z_DEGREES_PER_SECOND
- SENSOR_DATA_TYPE_TILT_X_DEGREES
- SENSOR_DATA_TYPE_TILT_Y_DEGREES
- SENSOR_DATA_TYPE_TILT_Z_DEGREES
- SENSOR_DATA_TYPE_DISTANCE_X_METERS
- SENSOR_DATA_TYPE_DISTANCE_Y_METERS
- SENSOR_DATA_TYPE_DISTANCE_Z_METERS
- SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_X_MILLIGAUSS
- SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_Y_MILLIGAUSS
- SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_Z_MILLIGAUSS
- SENSOR_DATA_TYPE_MAGNETIC_HEADING_X_DEGREES
- SENSOR_DATA_TYPE_MAGNETIC_HEADING_Y_DEGREES
- SENSOR_DATA_TYPE_MAGNETIC_HEADING_Z_DEGREES
- SENSOR_DATA_TYPE_MAGNETIC_HEADING_COMPENSATED_MAGNETIC_NORTH_DEGREES
- SENSOR_DATA_TYPE_MAGNETIC_HEADING_COMPENSATED_TRUE_NORTH_DEGREES
- SENSOR_DATA_TYPE_MAGNETIC_HEADING_MAGNETIC_NORTH_DEGREES
- SENSOR_DATA_TYPE_MAGNETIC_HEADING_TRUE_NORTH_DEGREES
- SENSOR_DATA_TYPE_QUADRANT_ANGLE_DEGREES
- SENSOR_DATA_TYPE_ROTATION_MATRIX
- SENSOR_DATA_TYPE_QUATERNION
- SENSOR_DATA_TYPE_SIMPLE_DEVICE_ORIENTATION
- SENSOR_DATA_TYPE_MAGNETOMETER_ACCURACY
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 611fc68432c5e1561d9f2399c43ea0da44ea8868
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561739"
---
# <a name="sensorcategoryorientation"></a>传感器\_类别\_方向


传感器\_类别\_方向类别包含提供有关物理方向信息的传感器。 罗盘提供导航方向，如基于磁北方。 Inclinometers 度量值增量的斜率或提升。 距离传感器测量某个对象接近传感器。

**平台定义的传感器类型**

此类别包括以下平台定义的传感器类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>传感器类型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span id="SENSOR_TYPE_AGGREGATED_DEVICE_ORIENTATION"></span><span id="sensor_type_aggregated_device_orientation"></span>
<strong>SENSOR_TYPE_AGGREGATED_DEVICE_ORIENTATION</strong></td>
<td><p>指定当前的设备方向，通过返回四元数，以及在某些情况下，旋转矩阵。 （旋转矩阵是可选的。）</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_AGGREGATED_QUADRANT_ORIENTATION"></span><span id="sensor_type_aggregated_quadrant_orientation"></span>
<strong>SENSOR_TYPE_AGGREGATED_QUADRANT_ORIENTATION</strong></td>
<td><p>指定以度为单位的当前设备方向。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_AGGREGATED_SIMPLE_DEVICE_ORIENTATION"></span><span id="sensor_type_aggregated_simple_device_orientation"></span>
<strong>SENSOR_TYPE_AGGREGATED_SIMPLE_DEVICE_ORIENTATION</strong></td>
<td><p>作为一个枚举，指定设备方向。 (此类型指定所使用的四个常规象限的其中一个设备方向：0 度，90 度顺时针旋转，计数器顺时针旋转、 计数器 180 和 270 度顺时针旋转计数器）。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_COMPASS_1D"></span><span id="sensor_type_compass_1d"></span>
<strong>SENSOR_TYPE_COMPASS_1D</strong> {A415F6C5-CB50-49D0-8E62-A8270BD7A26C}</td>
<td><p>一个轴罗盘。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_COMPASS_2D"></span><span id="sensor_type_compass_2d"></span>
<strong>SENSOR_TYPE_COMPASS_2D</strong> {15655CC0-997A-4D30-84DB-57CABA3648BB}</td>
<td><p>两个轴罗盘。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_COMPASS_3D"></span><span id="sensor_type_compass_3d"></span>
<strong>SENSOR_TYPE_COMPASS_3D</strong> {76B5CE0D-17DD-414D-93A1-E127F40BDF6E}</td>
<td><p>三个轴罗盘。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_DISTANCE_1D"></span><span id="sensor_type_distance_1d"></span>
<strong>SENSOR_TYPE_DISTANCE_1D</strong> {5F14AB2F-1407-4306-A93F-B1DBABE4F9C0}</td>
<td><p>一个轴距离的传感器。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_DISTANCE_2D"></span><span id="sensor_type_distance_2d"></span>
<strong>SENSOR_TYPE_DISTANCE_2D</strong> {5CF9A46C-A9A2-4E55-B6A1-A04AAFA95A92}</td>
<td><p>两个轴距离的传感器。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_DISTANCE_3D"></span><span id="sensor_type_distance_3d"></span>
<strong>SENSOR_TYPE_DISTANCE_3D</strong> {A20CAE31-0E25-4772-9FE5-96608A1354B2}</td>
<td><p>三个轴距离的传感器。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_INCLINOMETER_1D"></span><span id="sensor_type_inclinometer_1d"></span>
<strong>SENSOR_TYPE_INCLINOMETER_1D</strong> {B96F98C5-7A75-4BA7-94E9-AC868C966DD8}</td>
<td><p>一个轴 inclinometers。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_INCLINOMETER_2D"></span><span id="sensor_type_inclinometer_2d"></span>
<strong>SENSOR_TYPE_INCLINOMETER_2D</strong> {AB140F6D-83EB-4264-B70B-B16A5B256A01}</td>
<td><p>两个轴 inclinometers。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_INCLINOMETER_3D"></span><span id="sensor_type_inclinometer_3d"></span>
<strong>SENSOR_TYPE_INCLINOMETER_3D</strong> {B84919FB-EA85-4976-8444-6F6F5C6D31DB}</td>
<td><p>三个轴 inclinometers。</p></td>
</tr>
</tbody>
</table>

**平台定义的数据字段**

此类别的平台定义的属性键基于传感器\_数据\_类型\_方向\_GUID:

{1637D8A2-4248-4275-865D-558DE84AEDFD}

此类别包括以下平台定义的数据字段。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>数据字段名称和 PID</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_ANGULAR_VELOCITY_X_DEGREES_PER_SECOND"></span><span id="sensor_data_type_angular_velocity_x_degrees_per_second"></span>
<strong>SENSOR_DATA_TYPE_ANGULAR_VELOCITY_X_DEGREES_PER_SECOND</strong> (PID = 10)</td>
<td><p><strong>VT_R8</strong></p>
<p>陀螺测试仪感应 x 轴方向，以度为单位每秒的速度。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Y_DEGREES_PER_SECOND"></span><span id="sensor_data_type_angular_velocity_y_degrees_per_second"></span>
<strong>SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Y_DEGREES_PER_SECOND</strong> (PID = 11)</td>
<td><p><strong>VT_R8</strong></p>
<p>陀螺测试仪感应 y 轴方向，以度为单位每秒的速度。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Z_DEGREES_PER_SECOND"></span><span id="sensor_data_type_angular_velocity_z_degrees_per_second"></span>
<strong>SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Z_DEGREES_PER_SECOND</strong> (PID = 12)</td>
<td><p><strong>VT_R8</strong></p>
<p>陀螺测试仪感应 z 轴方向，以度为单位每秒的速度。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_TILT_X_DEGREES"></span><span id="sensor_data_type_tilt_x_degrees"></span>
<strong>SENSOR_DATA_TYPE_TILT_X_DEGREES</strong> (PID = 2)</td>
<td><p><strong>VT_R4</strong></p>
<p>倾斜仪 x 轴角度 （以度为单位）。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_TILT_Y_DEGREES"></span><span id="sensor_data_type_tilt_y_degrees"></span>
<strong>SENSOR_DATA_TYPE_TILT_Y_DEGREES</strong> (PID = 3)</td>
<td><p><strong>VT_R4</strong></p>
<p>倾斜仪 y 轴角度 （以度为单位）。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_TILT_Z_DEGREES"></span><span id="sensor_data_type_tilt_z_degrees"></span>
<strong>SENSOR_DATA_TYPE_TILT_Z_DEGREES</strong> (PID = 4)</td>
<td><p><strong>VT_R4</strong></p>
<p>倾斜仪 z 轴角度 （以度为单位）。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_DISTANCE_X_METERS"></span><span id="sensor_data_type_distance_x_meters"></span>
<strong>SENSOR_DATA_TYPE_DISTANCE_X_METERS</strong> (PID = 8)</td>
<td><p><strong>VT_R4</strong></p>
<p>X 轴距离，以米为单位。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_DISTANCE_Y_METERS"></span><span id="sensor_data_type_distance_y_meters"></span>
<strong>SENSOR_DATA_TYPE_DISTANCE_Y_METERS</strong> (PID = 9)</td>
<td><p><strong>VT_R4</strong></p>
<p>Y 轴的距离，以米为单位。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_DISTANCE_Z_METERS"></span><span id="sensor_data_type_distance_z_meters"></span>
<strong>SENSOR_DATA_TYPE_DISTANCE_Z_METERS</strong> (PID = 10)</td>
<td><p><strong>VT_R4</strong></p>
<p>Z 轴距离，以米为单位。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_X_MILLIGAUSS"></span><span id="sensor_data_type_magnetic_field_strength_x_milligauss"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_X_MILLIGAUSS</strong> (PID = 19)</td>
<td><p><strong>VT_R8</strong></p>
<p>磁力仪 milligauss 中的 x 轴字段长度。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_Y_MILLIGAUSS"></span><span id="sensor_data_type_magnetic_field_strength_y_milligauss"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_Y_MILLIGAUSS</strong> (PID = 20)</td>
<td><p><strong>VT_R8</strong></p>
<p>磁力仪 milligauss 中的 y 轴字段长度。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_Z_MILLIGAUSS"></span><span id="sensor_data_type_magnetic_field_strength_z_milligauss"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_Z_MILLIGAUSS</strong> (PID = 21)</td>
<td><p><strong>VT_R8</strong></p>
<p>磁力仪 milligauss 中的 z 轴字段长度。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_X_DEGREES"></span><span id="sensor_data_type_magnetic_heading_x_degrees"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_X_DEGREES</strong> (PID = 5)</td>
<td><p><strong>VT_R4</strong></p>
<p>罗盘 x 轴方向，以度为单位。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_Y_DEGREES"></span><span id="sensor_data_type_magnetic_heading_y_degrees"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_Y_DEGREES</strong> (PID = 6)</td>
<td><p><strong>VT_R4</strong></p>
<p>罗盘 y 轴方向，以度为单位。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_Z_DEGREES"></span><span id="sensor_data_type_magnetic_heading_z_degrees"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_Z_DEGREES</strong> (PID = 7)</td>
<td><p><strong>VT_R4</strong></p>
<p>罗盘 z 轴方向，以度为单位。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_COMPENSATED_MAGNETIC_NORTH_DEGREES_"></span><span id="sensor_data_type_magnetic_heading_compensated_magnetic_north_degrees_"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_COMPENSATED_MAGNETIC_NORTH_DEGREES</strong> (PID = 11)</td>
<td><p><strong>VT_R8</strong></p>
<p>补偿相对于地方，磁北的指南针标题以度为单位。 此补偿将导致标题角度而无法表示像指南针设备正努力在平面上级别地面 PC 所在的度量。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_COMPENSATED_TRUE_NORTH_DEGREES_"></span><span id="sensor_data_type_magnetic_heading_compensated_true_north_degrees_"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_COMPENSATED_TRUE_NORTH_DEGREES</strong> (PID = 12)</td>
<td><p><strong>VT_R8</strong></p>
<p>补偿相对于真北的指南针标题以度为单位。 此补偿将导致标题角度而无法表示像指南针设备正努力在平面上级别地面 PC 所在的度量。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_MAGNETIC_NORTH_DEGREES__"></span><span id="sensor_data_type_magnetic_heading_magnetic_north_degrees__"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_MAGNETIC_NORTH_DEGREES</strong> (PID = 13)</td>
<td><p><strong>VT_R8</strong></p>
<p>相对于以度为单位的地方，磁北 uncompensated 指南针标题。 标题角度的测量值，表示指南针设备安装相对于平面上进行度量。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_TRUE_NORTH_DEGREES___"></span><span id="sensor_data_type_magnetic_heading_true_north_degrees___"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_TRUE_NORTH_DEGREES</strong> (PID = 14)</td>
<td><p><strong>VT_R8</strong></p>
<p>相对于真北以度为单位的 uncompensated 指南针标题。 标题角度的测量值，表示指南针设备安装相对于平面上进行度量。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_QUADRANT_ANGLE_DEGREES"></span><span id="sensor_data_type_quadrant_angle_degrees"></span>
<strong>SENSOR_DATA_TYPE_QUADRANT_ANGLE_DEGREES</strong> (PID = 15)</td>
<td><p><strong>VT_R8</strong></p>
<p>聚合的象限的方向，以度为单位。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_ROTATION_MATRIX"></span><span id="sensor_data_type_rotation_matrix"></span>
<strong>SENSOR_DATA_TYPE_ROTATION_MATRIX</strong> (PID = 16)</td>
<td><p><strong>VT_VECTOR|VT_UI1</strong></p>
<p>计数数组，表示为一个 3x3 旋转矩阵在 3D 空间中设备的方向 (VT_VECTOR |VT_UI1)。</p>
<p>向量类型的数据始终序列化为 VT_UI1 （无符号，1 字节字符的一个数组）。 此数据字段必须包含每个值作为单精度浮点数 (VT_R4)。</p>
<p>此数组表示为一个矩阵：</p>
<img src="images/sensor-data-type-rotation-matrix.png" alt="rotation matrix" />
<p>这些值进行排序的旋转矩阵数据字段数组中，如下所示：M11,M12,M13,M21,M22,M23,M31,M32,M33</p>
<p>请注意，对于实现对现成的 Windows 8 的 HID 传感器类驱动程序支持的设备，此数据字段是可选的。 如果只有<strong>SENSOR_DATA_TYPE_QUATERNION</strong>实现<strong>SENSOR_DATA_TYPE_ROTATION_MATRIX</strong>计算，并填充每个数据报表发送。 设备未使用的内置 HID 传感器类驱动程序需要计算并公开这两<strong>SENSOR_DATA_TYPE_QUATERNION</strong>并<strong>SENSOR_DATA_TYPE_ROTATION_MATRIX</strong>传感器数据字段。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_QUATERNION"></span><span id="sensor_data_type_quaternion"></span>
<strong>SENSOR_DATA_TYPE_QUATERNION</strong> (PID = 17)</td>
<td><p><strong>VT_VECTOR|VT_UI1</strong></p>
<p>X、 y、 z、 w 四元数表示 3D 空间中设备的方向的值。 (VT_VECTOR |VT_UI1)。</p>
<p>向量类型的数据始终序列化为 VT_UI1 （无符号，1 字节字符的一个数组）。</p>
<p>此数据字段必须包含每个值作为单精度浮点数 (VT_R4)。</p>
<p>此数组中值的顺序是按如下所示: [x、 y、 z、 w]</p>
<p>四元数的 W 值仅限于 [0，1] 而不是完整 [-1，1]。</p>
<p>所有旋转必须正向 （和不能反向） 中所都述。</p>
<p>注意：四元数的输出应采用规范化格式。 当四元数表示采用规范化格式，值将满足以下条件：</p>
<img src="images/sensor-data-type-quaternion-formula.png" alt="quaternion formula" /></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_SIMPLE_DEVICE_ORIENTATION"></span><span id="sensor_data_type_simple_device_orientation"></span>
<strong>SENSOR_DATA_TYPE_SIMPLE_DEVICE_ORIENTATION</strong> (PID = 18)</td>
<td><p><strong>VT_UI4</strong></p>
<p>聚合的设备方向和指定为枚举。 （枚举值对应于四个象限之一。）</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETOMETER_ACCURACY"></span><span id="sensor_data_type_magnetometer_accuracy"></span>
<strong>SENSOR_DATA_TYPE_MAGNETOMETER_ACCURACY</strong> (PID = 22)</td>
<td><p><strong>VT_I4</strong></p>
<p>磁力仪准确性读数，指定为枚举。</p></td>
</tr>
</tbody>
</table>

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
<td><p>Header</p></td>
<td>Sensors.h</td>
</tr>
</tbody>
</table>

 

 





