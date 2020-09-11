---
title: 传感器 \_ 类别 \_ 位置
description: "\"传感器 \\_ 类别 \\_ 位置\" 类别包含的传感器提供地理位置信息。"
ms.assetid: 19B76F17-0575-42F2-ADEF-15932DCE7E06
topic_type:
- apiref
api_name:
- SENSOR_TYPE_LOCATION_BROADCAST
- SENSOR_TYPE_LOCATION_DEAD_RECKONING
- SENSOR_TYPE_LOCATION_GPS
- SENSOR_TYPE_LOCATION_LOOKUP
- SENSOR_TYPE_LOCATION_OTHER
- SENSOR_TYPE_LOCATION_STATIC
- SENSOR_TYPE_LOCATION_TRIANGULATION
- SENSOR_DATA_TYPE_ADDRESS1
- SENSOR_DATA_TYPE_ADDRESS2
- SENSOR_DATA_TYPE_ALTITUDE_ANTENNA_SEALEVEL_METERS
- SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_ERROR_METERS
- SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_METERS
- SENSOR_DATA_TYPE_ALTITUDE_SEALEVEL_ERROR_METERS
- SENSOR_DATA_TYPE_ALTITUDE_SEALEVEL_METERS
- SENSOR_DATA_TYPE_CITY
- SENSOR_DATA_TYPE_COUNTRY_REGION
- SENSOR_DATA_TYPE_DGPS_DATA_AGE
- SENSOR_DATA_TYPE_DIFFERENTIAL_REFERENCE_STATION_ID
- SENSOR_DATA_TYPE_ERROR_RADIUS_METERS
- SENSOR_DATA_TYPE_FIX_QUALITY
- SENSOR_DATA_TYPE_FIX_TYPE
- SENSOR_DATA_TYPE_GEOIDAL_SEPARATION
- SENSOR_DATA_TYPE_GPS_OPERATION_MODE
- SENSOR_DATA_TYPE_GPS_SELECTION_MODE
- SENSOR_DATA_TYPE_GPS_STATUS
- SENSOR_DATA_TYPE_HORIZONAL_DILUTION_OF_PRECISION
- SENSOR_DATA_TYPE_LATITUDE_DEGREES
- SENSOR_DATA_TYPE_LONGITUDE_DEGREES
- SENSOR_DATA_TYPE_MAGNETIC_HEADING_DEGREES
- SENSOR_DATA_TYPE_MAGNETIC_VARIATION
- SENSOR_DATA_TYPE_NMEA_SENTENCE
- SENSOR_DATA_TYPE_POSITION_DILUTION_OF_PRECISION
- SENSOR_DATA_TYPE_POSTALCODE
- SENSOR_DATA_TYPE_SATELLITES_IN_VIEW
- SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_AZIMUTH
- SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_ELEVATION
- SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_ID
- SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_PRNS
- SENSOR_DATA_TYPE_SATELLITES_USED_PRNS_AND_CONSTELLATIONS
- SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_STN_RATIO
- SENSOR_DATA_TYPE_SATELLITES_USED_COUNT
- SENSOR_DATA_TYPE_SATELLITES_USED_PRNS
- SENSOR_DATA_TYPE_SPEED_KNOTS
- SENSOR_DATA_TYPE_STATE_PROVINCE
- SENSOR_DATA_TYPE_TRUE_HEADING_DEGREES
- SENSOR_DATA_TYPE_VERTICAL_DILUTION_OF_PRECISION
api_type:
- NA
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: a464187cf0c7656f6f08fd01b0edd7f1e23986a4
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010629"
---
# <a name="sensor_category_location"></a>传感器 \_ 类别 \_ 位置


"传感器 \_ 类别 \_ 位置" 类别包含的传感器提供地理位置信息。

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
<td><span id="SENSOR_TYPE_LOCATION_BROADCAST"></span><span id="sensor_type_location_broadcast"></span>
<strong>SENSOR_TYPE_LOCATION_BROADCAST</strong> {D26988CF-5162-4039-BB17-4C58B698E44A}</td>
<td><p>传感器使用电视或射频等传输来传输位置信息。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_LOCATION_DEAD_RECKONING"></span><span id="sensor_type_location_dead_reckoning"></span>
<strong>SENSOR_TYPE_LOCATION_DEAD_RECKONING</strong> {1A37D538-F28B-42DA-9FCE-A9D0A2A6D829}</td>
<td><p>Reckoning 传感器。 这些传感器首先计算当前位置，然后使用运动数据更新当前位置。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_LOCATION_GPS"></span><span id="sensor_type_location_gps"></span>
<strong>SENSOR_TYPE_LOCATION_GPS</strong> {ED4CA589-327A-4FF9-A560-91DA4B48275E}</td>
<td><p>全局定位系统传感器。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_LOCATION_LOOKUP"></span><span id="sensor_type_location_lookup"></span>
<strong>SENSOR_TYPE_LOCATION_LOOKUP</strong> {3B2EAE4A-72CE-436D-96D2-3C5B8570E987}</td>
<td><p>查找传感器，如根据用户的 IP 地址提供信息的传感器。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_LOCATION_OTHER"></span><span id="sensor_type_location_other"></span>
<strong>SENSOR_TYPE_LOCATION_OTHER</strong> {9B2D0566-0368-4F71-B88D-533F132031DE}</td>
<td><p>其他位置传感器。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_LOCATION_STATIC"></span><span id="sensor_type_location_static"></span>
<strong>SENSOR_TYPE_LOCATION_STATIC</strong> {095F8184-0FA9-4445-8E6E-B70F320B6B4C}</td>
<td><p>固定位置传感器，如使用预设的用户提供的信息。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_LOCATION_TRIANGULATION"></span><span id="sensor_type_location_triangulation"></span>
<strong>SENSOR_TYPE_LOCATION_TRIANGULATION</strong> {691C341A-5406-4FE1-942F-2246CBEB39E0}</td>
<td><p>三角化传感器，如确定基于移动电话塔 proximities 的当前位置的传感器。</p></td>
</tr>
</tbody>
</table>

**平台定义的数据字段**

此类别的平台定义的属性键基于传感器 \_ 数据 \_ 类型 \_ 位置 \_ GUID：

{055C74D8-CA6F-47D6-95C6-1ED3637A0FF4}

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
<td><span id="SENSOR_DATA_TYPE_ADDRESS1"></span><span id="sensor_data_type_address1"></span>
<strong>SENSOR_DATA_TYPE_ADDRESS1</strong> (PID = 23) </td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>街道地址，第一行。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_ADDRESS2"></span><span id="sensor_data_type_address2"></span>
<strong>SENSOR_DATA_TYPE_ADDRESS2</strong> (PID = 24) </td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>街道地址，第二行。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_ALTITUDE_ANTENNA_SEALEVEL_METERS"></span><span id="sensor_data_type_altitude_antenna_sealevel_meters"></span>
<strong>SENSOR_DATA_TYPE_ALTITUDE_ANTENNA_SEALEVEL_METERS</strong> (PID = 36) </td>
<td><p>VT_R8</p>
<p>天线的海拔高度，以米为单位被引用。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_ERROR_METERS"></span><span id="sensor_data_type_altitude_ellipsoid_error_meters"></span>
<strong>SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_ERROR_METERS</strong> (PID = 29) </td>
<td><p>VT_R8</p>
<p>向 World 测量系统引用的高度错误 (WGS 84) 参考椭圆体，以米为单位。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_METERS"></span><span id="sensor_data_type_altitude_ellipsoid_meters"></span>
<strong>SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_METERS</strong> (PID = 5) </td>
<td><p>VT_R8</p>
<p>World 测量 System (WGS 84) 的高度引用椭圆体，以米为单位。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_ALTITUDE_SEALEVEL_ERROR_METERS"></span><span id="sensor_data_type_altitude_sealevel_error_meters"></span>
<strong>SENSOR_DATA_TYPE_ALTITUDE_SEALEVEL_ERROR_METERS</strong> (PID = 30) </td>
<td><p>VT_R8</p>
<p>向海平面引用了海拔错误，单位为米。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_ALTITUDE_SEALEVEL_METERS"></span><span id="sensor_data_type_altitude_sealevel_meters"></span>
<strong>SENSOR_DATA_TYPE_ALTITUDE_SEALEVEL_METERS</strong> (PID = 4) </td>
<td><p>VT_R8</p>
<p>高度引用海平面，以米为单位。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_CITY"></span><span id="sensor_data_type_city"></span>
<strong>SENSOR_DATA_TYPE_CITY</strong> (PID = 25) </td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>市县：</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_COUNTRY_REGION"></span><span id="sensor_data_type_country_region"></span>
<strong>SENSOR_DATA_TYPE_COUNTRY_REGION</strong> (PID = 28) </td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>国家或地区，以 ISO 3166 1-2 国家/地区代码表示。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_DGPS_DATA_AGE"></span><span id="sensor_data_type_dgps_data_age"></span>
<strong>SENSOR_DATA_TYPE_DGPS_DATA_AGE</strong> (PID = 35) </td>
<td><p>VT_R8</p>
<p>差异 GPS 数据的保留时间，以秒为单位。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_DIFFERENTIAL_REFERENCE_STATION_ID"></span><span id="sensor_data_type_differential_reference_station_id"></span>
<strong>SENSOR_DATA_TYPE_DIFFERENTIAL_REFERENCE_STATION_ID</strong> (PID = 37) </td>
<td><p>VT_I4</p>
<p>差异引用工作站的 ID。 范围为0000到1023。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_ERROR_RADIUS_METERS"></span><span id="sensor_data_type_error_radius_meters"></span>
<strong>SENSOR_DATA_TYPE_ERROR_RADIUS_METERS</strong> (PID = 22) </td>
<td><p>VT_R8</p>
<p>纬度值和经度值的准确性（以米为单位）。 如果值为零，则表示准确性级别未知。 Location API 为该字段提供非零值的传感器提供优先级。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_FIX_QUALITY"></span><span id="sensor_data_type_fix_quality"></span>
<strong>SENSOR_DATA_TYPE_FIX_QUALITY</strong> (PID = 10) </td>
<td><p>VT_I4</p>
<p>修复质量</p>
<p>0 = 无修补程序</p>
<p>1 = GPS</p>
<p>2 = DGPS</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_FIX_TYPE"></span><span id="sensor_data_type_fix_type"></span>
<strong>SENSOR_DATA_TYPE_FIX_TYPE</strong> (PID = 11) </td>
<td><p>VT_I4</p>
<p>修复类型</p>
<p>0 = 无修补程序</p>
<p>1 = GPS SPS 模式，修复有效</p>
<p>2 = DGPS SPS 模式，修复有效</p>
<p>3 = GPS PPS 模式，修复有效</p>
<p>4 = 实时运动</p>
<p>5 = Float RTK</p>
<p>6 = 估计 (死推测) </p>
<p>7 = 手动输入模式</p>
<p>8 = 模拟器模式</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_GEOIDAL_SEPARATION"></span><span id="sensor_data_type_geoidal_separation"></span>
<strong>SENSOR_DATA_TYPE_GEOIDAL_SEPARATION</strong> (PID = 34) </td>
<td><p>VT_R8</p>
<p>WGS-84 椭圆体和平均海平面级别之间的差异。 小于零的值指示平均海平面级别低于引用椭圆体。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_GPS_OPERATION_MODE"></span><span id="sensor_data_type_gps_operation_mode"></span>
<strong>SENSOR_DATA_TYPE_GPS_OPERATION_MODE</strong> (PID = 32) </td>
<td><p>VT_I4</p>
<p>操作模式。</p>
<p>0 = 手动。 GPS 传感器设置为在2-d 或3-d 模式下运行。</p>
<p>1 = 自动。 GPS 传感器可以在2-d 和3-d 模式之间自动切换。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_GPS_SELECTION_MODE"></span><span id="sensor_data_type_gps_selection_mode"></span>
<strong>SENSOR_DATA_TYPE_GPS_SELECTION_MODE</strong> (PID = 31) </td>
<td><p>VT_I4</p>
<p>选择模式。</p>
<p>0 = 自治。</p>
<p>1 = DGPS。</p>
<p>2 = 预计 (死推测) 。</p>
<p>3 = 手动输入。</p>
<p>4 = 模拟器。</p>
<p>5 = 数据无效。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_GPS_STATUS"></span><span id="sensor_data_type_gps_status"></span>
<strong>SENSOR_DATA_TYPE_GPS_STATUS</strong> (PID = 33) </td>
<td><p>VT_I4</p>
<p>当前数据状态。</p>
<p>1 = 数据有效。</p>
<p>2 = 数据无效。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_HORIZONAL_DILUTION_OF_PRECISION"></span><span id="sensor_data_type_horizonal_dilution_of_precision"></span>
<strong>SENSOR_DATA_TYPE_HORIZONAL_DILUTION_OF_PRECISION</strong> (PID = 13) </td>
<td><p>VT_R8</p>
<p>精度的水平 dilution。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_LATITUDE_DEGREES"></span><span id="sensor_data_type_latitude_degrees"></span>
<strong>SENSOR_DATA_TYPE_LATITUDE_DEGREES</strong> (PID = 2) </td>
<td><p>VT_R8</p>
<p>度纬度。 北部为正值。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_LONGITUDE_DEGREES"></span><span id="sensor_data_type_longitude_degrees"></span>
<strong>SENSOR_DATA_TYPE_LONGITUDE_DEGREES</strong> (PID = 3) </td>
<td><p>VT_R8</p>
<p>经度。 东为正值。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_DEGREES"></span><span id="sensor_data_type_magnetic_heading_degrees"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_DEGREES</strong> (PID = 8) </td>
<td><p>VT_R8</p>
<p>标题，相对于北部，以度为单位。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_VARIATION"></span><span id="sensor_data_type_magnetic_variation"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_VARIATION</strong> (PID = 9) </td>
<td><p>VT_R8</p>
<p>磁变体。 东为正值。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_NMEA_SENTENCE"></span><span id="sensor_data_type_nmea_sentence"></span>
<strong>SENSOR_DATA_TYPE_NMEA_SENTENCE</strong> (PID = 38) </td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>当前 NMEA 语句字符串。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_POSITION_DILUTION_OF_PRECISION"></span><span id="sensor_data_type_position_dilution_of_precision"></span>
<strong>SENSOR_DATA_TYPE_POSITION_DILUTION_OF_PRECISION</strong> (PID = 12) </td>
<td><p>VT_R8</p>
<p>精确位置 dilution。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_POSTALCODE"></span><span id="sensor_data_type_postalcode"></span>
<strong>SENSOR_DATA_TYPE_POSTALCODE</strong> (PID = 27) </td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>邮政编码。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_IN_VIEW"></span><span id="sensor_data_type_satellites_in_view"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_IN_VIEW</strong> (PID = 17) </td>
<td><p>VT_I4</p>
<p>视图中的附属项的数目。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_AZIMUTH"></span><span id="sensor_data_type_satellites_in_view_azimuth"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_AZIMUTH</strong> (PID = 20) </td>
<td><p><strong>VT_VECTOR |VT_UI1</strong></p>
<p>计数数组，其中包含每个附属项在视图中的 azimuth。</p>
<p>矢量类型的数据始终序列化为 <strong>VT_UI1</strong> (一个) 的无符号、1字节字符数组。 此数据字段实际包含每个值作为 IEEE 8 字节实数值 (<strong>VT_ R8</strong>) 。 如果为空值，请使用-1 作为占位符。</p>
<p>有关使用数组的信息，请参阅 <a href="https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types" data-raw-source="[Retrieving Vector Types](/windows/desktop/SensorsAPI/retrieving-vector-types)">检索矢量类型</a>。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_ELEVATION"></span><span id="sensor_data_type_satellites_in_view_elevation"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_ELEVATION</strong> (PID = 19) </td>
<td><p><strong>VT_VECTOR |VT_UI1</strong></p>
<p>计数数组，其中包含每个附属项在视图中的仰角。</p>
<p>矢量类型的数据始终序列化为 <strong>VT_UI1</strong> (一个) 的无符号、1字节字符数组。 此数据字段实际包含每个值作为 IEEE 8 字节实数值 (<strong>VT_R8</strong>) 。 使用-91 作为空值的占位符。</p>
<p>有关使用数组的信息，请参阅 <a href="https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types" data-raw-source="[Retrieving Vector Types](/windows/desktop/SensorsAPI/retrieving-vector-types)">检索矢量类型</a>。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_ID"></span><span id="sensor_data_type_satellites_in_view_id"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_ID</strong> (PID = 39) </td>
<td><p><strong>VT_VECTOR |VT_UI1</strong></p>
<p>计数数组，其中包含视图中每个附属项的 ID。</p>
<p>矢量类型的数据始终序列化为 <strong>VT_UI1</strong> (一个) 的无符号、1字节字符数组。 此数据字段实际包含每个值作为4字节无符号整数 (<strong>VT_UI4</strong>) 。</p>
<p>有关使用数组的信息，请参阅 <a href="https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types" data-raw-source="[Retrieving Vector Types](/windows/desktop/SensorsAPI/retrieving-vector-types)">检索矢量类型</a>。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_PRNS"></span><span id="sensor_data_type_satellites_in_view_prns"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_PRNS</strong> (PID = 18) </td>
<td><p><strong>VT_VECTOR |VT_UI1</strong></p>
<p>计数数组，其中包含视图中卫星的伪随机噪音代码。</p>
<p>矢量类型的数据始终序列化为 <strong>VT_UI1</strong> (一个) 的无符号、1字节字符数组。 此数据字段实际包含每个值作为4字节无符号整数 (<strong>VT_UI4</strong>) 。 使用零 (0) 作为空值的占位符。</p>
<p>有关使用数组的信息，请参阅 <a href="https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types" data-raw-source="[Retrieving Vector Types](/windows/desktop/SensorsAPI/retrieving-vector-types)">检索矢量类型</a>。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_USED_PRNS_AND_CONSTELLATIONS"></span><span id="sensor_data_type_satellites_used_prns_and_constellations"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_USED_PRNS_AND_CONSTELLATIONS</strong> (PID = 41) </td>
<td><p><strong>VT_VECTOR |VT_UI2</strong></p>
<p>计数数组，包含解决方案中使用的卫星的伪随机噪音代码。</p>
<p>矢量类型的数据始终序列化为 <strong>VT_UI2</strong> (未签名的2字节字符) 数组。 此数据字段必须包含每个值作为4字节无符号整数 (<strong>VT_UI4</strong>) 。 使用零 (0) 作为空值的占位符。</p>
<p>有关使用数组的信息，请参阅 <a href="https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types" data-raw-source="[Retrieving Vector Types](/windows/desktop/SensorsAPI/retrieving-vector-types)">检索矢量类型</a>。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_STN_RATIO"></span><span id="sensor_data_type_satellites_in_view_stn_ratio"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_STN_RATIO</strong> (PID = 21) </td>
<td><p><strong>VT_VECTOR |VT_UI1</strong></p>
<p>计数数组，其中包含在视图中的卫星的信噪比。</p>
<p>矢量类型的数据始终序列化为 <strong>VT_UI1</strong> (一个) 的无符号、1字节字符数组。 此数据字段实际包含每个值作为 IEEE 8 字节实数值 (<strong>VT_R8</strong>) 。 使用零 (0) 作为空值的占位符。</p>
<p>此属性是必需的，并且必须由所有 GPS 设备支持。</p>
<p>有关使用数组的信息，请参阅 <a href="https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types" data-raw-source="[Retrieving Vector Types](/windows/desktop/SensorsAPI/retrieving-vector-types)">检索矢量类型</a>。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_USED_COUNT"></span><span id="sensor_data_type_satellites_used_count"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_USED_COUNT</strong> (PID = 15) </td>
<td><p>VT_I4</p>
<p>解决方案中使用的附属项的数目。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_USED_PRNS"></span><span id="sensor_data_type_satellites_used_prns"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_USED_PRNS</strong> (PID = 16) </td>
<td><p><strong>VT_VECTOR |VT_UI1</strong></p>
<p>计数数组，包含解决方案中使用的卫星的伪随机噪音代码。</p>
<p>矢量类型的数据始终序列化为 <strong>VT_UI1</strong> (一个) 的无符号、1字节字符数组。 此数据字段必须包含每个值作为4字节无符号整数 (<strong>VT_UI4</strong>) 。 使用零 (0) 作为空值的占位符。</p>
<p>有关使用数组的信息，请参阅 <a href="https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types" data-raw-source="[Retrieving Vector Types](/windows/desktop/SensorsAPI/retrieving-vector-types)">检索矢量类型</a>。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_SPEED_KNOTS"></span><span id="sensor_data_type_speed_knots"></span>
<strong>SENSOR_DATA_TYPE_SPEED_KNOTS</strong> (PID = 6) </td>
<td><p>VT_R8</p>
<p>速度，在节点中。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_STATE_PROVINCE"></span><span id="sensor_data_type_state_province"></span>
<strong>SENSOR_DATA_TYPE_STATE_PROVINCE</strong> (PID = 26) </td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>省/市/自治区。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_TRUE_HEADING_DEGREES"></span><span id="sensor_data_type_true_heading_degrees"></span>
<strong>SENSOR_DATA_TYPE_TRUE_HEADING_DEGREES</strong> (PID = 7) </td>
<td><p>VT_R8</p>
<p>与 true 北部相关的标题，以度为单位。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_VERTICAL_DILUTION_OF_PRECISION"></span><span id="sensor_data_type_vertical_dilution_of_precision"></span>
<strong>SENSOR_DATA_TYPE_VERTICAL_DILUTION_OF_PRECISION</strong> (PID = 14) </td>
<td><p>VT_R8</p>
<p>精度的垂直 dilution。</p></td>
</tr>
</tbody>
</table>

 

