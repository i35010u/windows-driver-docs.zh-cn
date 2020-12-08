---
title: 传感器 \_ 类别 \_ 方向
description: 传感器 \_ 类别 \_ 方向类别包含提供有关物理方向的信息的传感器。
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
ms.openlocfilehash: 3e92e2f4fb33c16a711ba18e3b19a907893bbfed
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812199"
---
# <a name="sensor_category_orientation"></a>传感器 \_ 类别 \_ 方向


传感器 \_ 类别 \_ 方向类别包含提供有关物理方向的信息的传感器。 Compasses 提供了导航方向，如那些基于北亚的导航方向。 Inclinometers 度量斜率或提升。 距离传感器测量某个对象对传感器的接近程度。

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
<td><p>通过返回四元数，在某些情况下，通过返回一个旋转矩阵来指定当前的设备方向。  (旋转矩阵是可选的。 ) </p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_AGGREGATED_QUADRANT_ORIENTATION"></span><span id="sensor_type_aggregated_quadrant_orientation"></span>
<strong>SENSOR_TYPE_AGGREGATED_QUADRANT_ORIENTATION</strong></td>
<td><p>指定当前的设备方向（以度为单位）。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_AGGREGATED_SIMPLE_DEVICE_ORIENTATION"></span><span id="sensor_type_aggregated_simple_device_orientation"></span>
<strong>SENSOR_TYPE_AGGREGATED_SIMPLE_DEVICE_ORIENTATION</strong></td>
<td><p>将设备方向指定为枚举。 此类型 (使用四个一般象限之一指定设备方向：0度、90度、顺时针、180-逆时针和270度计数器顺时针。 ) </p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_COMPASS_1D"></span><span id="sensor_type_compass_1d"></span>
<strong>SENSOR_TYPE_COMPASS_1D</strong> {A415F6C5-CB50-49D0-8E62-A8270BD7A26C}</td>
<td><p>单轴 compasses。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_COMPASS_2D"></span><span id="sensor_type_compass_2d"></span>
<strong>SENSOR_TYPE_COMPASS_2D</strong> {15655CC0-997A-4D30-84DB-57CABA3648BB}</td>
<td><p>两轴 compasses。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_COMPASS_3D"></span><span id="sensor_type_compass_3d"></span>
<strong>SENSOR_TYPE_COMPASS_3D</strong> {76B5CE0D-17DD-414D-93A1-E127F40BDF6E}</td>
<td><p>三轴 compasses。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_DISTANCE_1D"></span><span id="sensor_type_distance_1d"></span>
<strong>SENSOR_TYPE_DISTANCE_1D</strong> {5F14AB2F-1407-4306-A93F-B1DBABE4F9C0}</td>
<td><p>单轴距离传感器。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_DISTANCE_2D"></span><span id="sensor_type_distance_2d"></span>
<strong>SENSOR_TYPE_DISTANCE_2D</strong> {5CF9A46C-A9A2-4E55-B6A1-A04AAFA95A92}</td>
<td><p>两轴距离传感器。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_DISTANCE_3D"></span><span id="sensor_type_distance_3d"></span>
<strong>SENSOR_TYPE_DISTANCE_3D</strong> {A20CAE31-0E25-4772-9FE5-96608A1354B2}</td>
<td><p>三轴距离传感器。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_INCLINOMETER_1D"></span><span id="sensor_type_inclinometer_1d"></span>
<strong>SENSOR_TYPE_INCLINOMETER_1D</strong> {B96F98C5-7A75-4BA7-94E9-AC868C966DD8}</td>
<td><p>单轴 inclinometers。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_INCLINOMETER_2D"></span><span id="sensor_type_inclinometer_2d"></span>
<strong>SENSOR_TYPE_INCLINOMETER_2D</strong> {AB140F6D-83EB-4264-B70B-B16A5B256A01}</td>
<td><p>两轴 inclinometers。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_INCLINOMETER_3D"></span><span id="sensor_type_inclinometer_3d"></span>
<strong>SENSOR_TYPE_INCLINOMETER_3D</strong> {B84919FB-EA85-4976-8444-6F6F5C6D31DB}</td>
<td><p>三轴 inclinometers。</p></td>
</tr>
</tbody>
</table>

**平台定义的数据字段**

此类别的平台定义的属性键基于传感器 \_ 数据 \_ 类型 \_ 方向 \_ GUID：

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
<strong>SENSOR_DATA_TYPE_ANGULAR_VELOCITY_X_DEGREES_PER_SECOND</strong> (PID = 10) </td>
<td><p>VT_R8</p>
<p>陀螺测试仪 x 轴速度，以度/秒为单位。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Y_DEGREES_PER_SECOND"></span><span id="sensor_data_type_angular_velocity_y_degrees_per_second"></span>
<strong>SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Y_DEGREES_PER_SECOND</strong> (PID = 11) </td>
<td><p>VT_R8</p>
<p>陀螺测试仪 y 轴速度，以度/秒为单位。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Z_DEGREES_PER_SECOND"></span><span id="sensor_data_type_angular_velocity_z_degrees_per_second"></span>
<strong>SENSOR_DATA_TYPE_ANGULAR_VELOCITY_Z_DEGREES_PER_SECOND</strong> (PID = 12) </td>
<td><p>VT_R8</p>
<p>陀螺测试仪 z 轴速度，以度/秒为单位。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_TILT_X_DEGREES"></span><span id="sensor_data_type_tilt_x_degrees"></span>
<strong>SENSOR_DATA_TYPE_TILT_X_DEGREES</strong> (PID = 2) </td>
<td><p>VT_R4</p>
<p>倾斜仪 x 轴角度，以度为单位。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_TILT_Y_DEGREES"></span><span id="sensor_data_type_tilt_y_degrees"></span>
<strong>SENSOR_DATA_TYPE_TILT_Y_DEGREES</strong> (PID = 3) </td>
<td><p>VT_R4</p>
<p>倾斜仪 y 轴角度，以度为单位。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_TILT_Z_DEGREES"></span><span id="sensor_data_type_tilt_z_degrees"></span>
<strong>SENSOR_DATA_TYPE_TILT_Z_DEGREES</strong> (PID = 4) </td>
<td><p>VT_R4</p>
<p>倾斜仪 z 轴角度，以度为单位。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_DISTANCE_X_METERS"></span><span id="sensor_data_type_distance_x_meters"></span>
<strong>SENSOR_DATA_TYPE_DISTANCE_X_METERS</strong> (PID = 8) </td>
<td><p>VT_R4</p>
<p>X 轴距离（以米为单位）。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_DISTANCE_Y_METERS"></span><span id="sensor_data_type_distance_y_meters"></span>
<strong>SENSOR_DATA_TYPE_DISTANCE_Y_METERS</strong> (PID = 9) </td>
<td><p>VT_R4</p>
<p>Y 轴距离（以米为单位）。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_DISTANCE_Z_METERS"></span><span id="sensor_data_type_distance_z_meters"></span>
<strong>SENSOR_DATA_TYPE_DISTANCE_Z_METERS</strong> (PID = 10) </td>
<td><p>VT_R4</p>
<p>Z 轴距离（以米为单位）。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_X_MILLIGAUSS"></span><span id="sensor_data_type_magnetic_field_strength_x_milligauss"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_X_MILLIGAUSS</strong> (PID = 19) </td>
<td><p>VT_R8</p>
<p>磁力仪 x 轴字段强度，在 milligauss 中。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_Y_MILLIGAUSS"></span><span id="sensor_data_type_magnetic_field_strength_y_milligauss"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_Y_MILLIGAUSS</strong> (PID = 20) </td>
<td><p>VT_R8</p>
<p>磁力仪 y 轴字段强度，在 milligauss 中。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_Z_MILLIGAUSS"></span><span id="sensor_data_type_magnetic_field_strength_z_milligauss"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_FIELD_STRENGTH_Z_MILLIGAUSS</strong> (PID = 21) </td>
<td><p>VT_R8</p>
<p>磁力仪 z 轴字段强度，在 milligauss 中。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_X_DEGREES"></span><span id="sensor_data_type_magnetic_heading_x_degrees"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_X_DEGREES</strong> (PID = 5) </td>
<td><p>VT_R4</p>
<p>罗盘 x 轴标题，以度为单位。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_Y_DEGREES"></span><span id="sensor_data_type_magnetic_heading_y_degrees"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_Y_DEGREES</strong> (PID = 6) </td>
<td><p>VT_R4</p>
<p>指南针 y 轴标题，以度为单位。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_Z_DEGREES"></span><span id="sensor_data_type_magnetic_heading_z_degrees"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_Z_DEGREES</strong> (PID = 7) </td>
<td><p>VT_R4</p>
<p>罗盘 z 轴标题，以度为单位。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_COMPENSATED_MAGNETIC_NORTH_DEGREES_"></span><span id="sensor_data_type_magnetic_heading_compensated_magnetic_north_degrees_"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_COMPENSATED_MAGNETIC_NORTH_DEGREES</strong> (PID = 11) </td>
<td><p>VT_R8</p>
<p>相对于北部的方向补偿罗盘标题。 此补偿会使标头角度的测量结果表示为：罗盘设备在计算机所在的地面上进行平齐。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_COMPENSATED_TRUE_NORTH_DEGREES_"></span><span id="sensor_data_type_magnetic_heading_compensated_true_north_degrees_"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_COMPENSATED_TRUE_NORTH_DEGREES</strong> (PID = 12) </td>
<td><p>VT_R8</p>
<p>相对于真北部的补偿罗盘标题（以度为单位）。 此补偿会使标头角度的测量结果表示为：罗盘设备在计算机所在的地面上进行平齐。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_MAGNETIC_NORTH_DEGREES__"></span><span id="sensor_data_type_magnetic_heading_magnetic_north_degrees__"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_MAGNETIC_NORTH_DEGREES</strong> (PID = 13) </td>
<td><p>VT_R8</p>
<p>相对于北部的 Uncompensated 罗盘标题。 标题角度的度量单位表示为相对于安装罗盘设备的平面。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_TRUE_NORTH_DEGREES___"></span><span id="sensor_data_type_magnetic_heading_true_north_degrees___"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_TRUE_NORTH_DEGREES</strong> (PID = 14) </td>
<td><p>VT_R8</p>
<p>相对于真北部的 Uncompensated 罗盘标题（以度为单位）。 标题角度的度量单位表示为相对于安装罗盘设备的平面。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_QUADRANT_ANGLE_DEGREES"></span><span id="sensor_data_type_quadrant_angle_degrees"></span>
<strong>SENSOR_DATA_TYPE_QUADRANT_ANGLE_DEGREES</strong> (PID = 15) </td>
<td><p>VT_R8</p>
<p>聚合的象限方向，以度为单位。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_ROTATION_MATRIX"></span><span id="sensor_data_type_rotation_matrix"></span>
<strong>SENSOR_DATA_TYPE_ROTATION_MATRIX</strong> (PID = 16) </td>
<td><p><strong>VT_VECTOR |VT_UI1</strong></p>
<p>计数数组，表示三维空间中设备的方向作为3x3 旋转矩阵 (VT_VECTOR |VT_UI1) 。</p>
<p>矢量类型的数据始终序列化为 VT_UI1 (一个) 的无符号、1字节字符数组。 此数据字段必须包含每个值作为单精度浮点型 (VT_R4) 。</p>
<p>此数组表示为矩阵：</p>
<img src="images/sensor-data-type-rotation-matrix.png" alt="rotation matrix" />
<p>这些值在轮换矩阵数据字段数组中进行排序，如下所示： M11、M12、M13、M21、M22、M23、M31、M32-16ms、M33</p>
<p>请注意，对于实现对内置 Windows 8 HID 传感器类驱动程序的支持的设备，此数据字段是可选的。 如果仅实现 <strong>SENSOR_DATA_TYPE_QUATERNION</strong> ，则将为发送的每个数据报表计算并填充 <strong>SENSOR_DATA_TYPE_ROTATION_MATRIX</strong> 。 不使用内置 HID 传感器类驱动程序的设备需要计算和公开 <strong>SENSOR_DATA_TYPE_QUATERNION</strong> 和 <strong>SENSOR_DATA_TYPE_ROTATION_MATRIX</strong> 的传感器数据字段。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_QUATERNION"></span><span id="sensor_data_type_quaternion"></span>
<strong>SENSOR_DATA_TYPE_QUATERNION</strong> (PID = 17) </td>
<td><p><strong>VT_VECTOR |VT_UI1</strong></p>
<p>表示设备在三维空间中的方向的四元数的 x、y、z 和 w 值。  (VT_VECTOR |VT_UI1) 。</p>
<p>矢量类型的数据始终序列化为 VT_UI1 (一个) 的无符号、1字节字符数组。</p>
<p>此数据字段必须包含每个值作为单精度浮点型 (VT_R4) 。</p>
<p>此数组中值的顺序如下： [x，y，z，w]</p>
<p>四元数的 W 值限制为 [0，1]，而不是完整的 [-1，1]。</p>
<p>必须以正向方向 (而不是反向) 来指定所有旋转。</p>
<p>注意：四元数的输出应为规范化格式。 当四元数以标准化格式表示时，这些值将满足以下各项：</p>
<img src="images/sensor-data-type-quaternion-formula.png" alt="quaternion formula" /></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_SIMPLE_DEVICE_ORIENTATION"></span><span id="sensor_data_type_simple_device_orientation"></span>
<strong>SENSOR_DATA_TYPE_SIMPLE_DEVICE_ORIENTATION</strong> (PID = 18) </td>
<td><p>VT_UI4</p>
<p>聚合的设备方向，指定为枚举。  (枚举值对应于四个象限之一。 ) </p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETOMETER_ACCURACY"></span><span id="sensor_data_type_magnetometer_accuracy"></span>
<strong>SENSOR_DATA_TYPE_MAGNETOMETER_ACCURACY</strong> (PID = 22) </td>
<td><p>VT_I4</p>
<p>磁力仪准确性读取，指定为枚举。</p></td>
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
<td><p>Windows 7</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>无受支持的版本</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>传感器。h</td>
</tr>
</tbody>
</table>

 

 





