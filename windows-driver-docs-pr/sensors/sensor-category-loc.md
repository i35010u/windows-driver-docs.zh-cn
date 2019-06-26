---
title: 传感器\_类别\_位置
description: 传感器\_类别\_位置类别包含提供地理位置信息的传感器。
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
ms.openlocfilehash: c34eb2f500967ec240abe9a8e409210958d5bfa8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354458"
---
# <a name="sensorcategorylocation"></a>传感器\_类别\_位置


传感器\_类别\_位置类别包含提供地理位置信息的传感器。

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
<td><p>通过使用传输电视或无线电频率等传输位置信息的传感器。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_LOCATION_DEAD_RECKONING"></span><span id="sensor_type_location_dead_reckoning"></span>
<strong>SENSOR_TYPE_LOCATION_DEAD_RECKONING</strong> {1A37D538-F28B-42DA-9FCE-A9D0A2A6D829}</td>
<td><p>死信算帐传感器。 这些传感器首先计算当前的位置，并使用移动数据，然后更新当前的位置。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_LOCATION_GPS"></span><span id="sensor_type_location_gps"></span>
<strong>SENSOR_TYPE_LOCATION_GPS</strong> {ED4CA589-327A-4FF9-A560-91DA4B48275E}</td>
<td><p>全球定位系统传感器。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_LOCATION_LOOKUP"></span><span id="sensor_type_location_lookup"></span>
<strong>SENSOR_TYPE_LOCATION_LOOKUP</strong> {3B2EAE4A-72CE-436D-96D2-3C5B8570E987}</td>
<td><p>查找传感器，例如根据用户的 IP 地址提供信息。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_LOCATION_OTHER"></span><span id="sensor_type_location_other"></span>
<strong>SENSOR_TYPE_LOCATION_OTHER</strong> {9B2D0566-0368-4F71-B88D-533F132031DE}</td>
<td><p>其他位置传感器。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_TYPE_LOCATION_STATIC"></span><span id="sensor_type_location_static"></span>
<strong>SENSOR_TYPE_LOCATION_STATIC</strong> {095F8184-0FA9-4445-8E6E-B70F320B6B4C}</td>
<td><p>修复了位置传感器，如那些使用预设、 用户提供的信息。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_TYPE_LOCATION_TRIANGULATION"></span><span id="sensor_type_location_triangulation"></span>
<strong>SENSOR_TYPE_LOCATION_TRIANGULATION</strong> {691C341A-5406-4FE1-942F-2246CBEB39E0}</td>
<td><p>三角测量传感器，例如确定基于蜂窝电话塔 proximities 的当前位置。</p></td>
</tr>
</tbody>
</table>

**平台定义的数据字段**

此类别的平台定义的属性键基于传感器\_数据\_类型\_位置\_GUID:

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
<strong>SENSOR_DATA_TYPE_ADDRESS1</strong> (PID = 23)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>街道地址、 第一行。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_ADDRESS2"></span><span id="sensor_data_type_address2"></span>
<strong>SENSOR_DATA_TYPE_ADDRESS2</strong> (PID = 24)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>街道地址、 第二行。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_ALTITUDE_ANTENNA_SEALEVEL_METERS"></span><span id="sensor_data_type_altitude_antenna_sealevel_meters"></span>
<strong>SENSOR_DATA_TYPE_ALTITUDE_ANTENNA_SEALEVEL_METERS</strong> (PID = 36)</td>
<td><p><strong>VT_R8</strong></p>
<p>天线，引用到 sea 级别，以米为单位的海拔高度。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_ERROR_METERS"></span><span id="sensor_data_type_altitude_ellipsoid_error_meters"></span>
<strong>SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_ERROR_METERS</strong> (PID = 29)</td>
<td><p><strong>VT_R8</strong></p>
<p>海拔高度错误引用到世界大地坐标系 (WGS 84) 引用椭圆体，以米为单位。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_METERS"></span><span id="sensor_data_type_altitude_ellipsoid_meters"></span>
<strong>SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_METERS</strong> (PID = 5)</td>
<td><p><strong>VT_R8</strong></p>
<p>引用到世界大地坐标系 (WGS 84) 引用椭圆体，以米为单位的海拔高度。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_ALTITUDE_SEALEVEL_ERROR_METERS"></span><span id="sensor_data_type_altitude_sealevel_error_meters"></span>
<strong>SENSOR_DATA_TYPE_ALTITUDE_SEALEVEL_ERROR_METERS</strong> (PID = 30)</td>
<td><p><strong>VT_R8</strong></p>
<p>海拔高度错误引用到 sea 级别，以米为单位。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_ALTITUDE_SEALEVEL_METERS"></span><span id="sensor_data_type_altitude_sealevel_meters"></span>
<strong>SENSOR_DATA_TYPE_ALTITUDE_SEALEVEL_METERS</strong> (PID = 4)</td>
<td><p><strong>VT_R8</strong></p>
<p>引用到 sea 级别，以米为单位的海拔高度。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_CITY"></span><span id="sensor_data_type_city"></span>
<strong>SENSOR_DATA_TYPE_CITY</strong> (PID = 25)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>城市。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_COUNTRY_REGION"></span><span id="sensor_data_type_country_region"></span>
<strong>SENSOR_DATA_TYPE_COUNTRY_REGION</strong> (PID = 28)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>国家或地区，表示为 ISO 3166 1-alpha-2 国家/地区代码。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_DGPS_DATA_AGE"></span><span id="sensor_data_type_dgps_data_age"></span>
<strong>SENSOR_DATA_TYPE_DGPS_DATA_AGE</strong> (PID = 35)</td>
<td><p><strong>VT_R8</strong></p>
<p>以秒为单位的差异的 GPS 数据保留时间。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_DIFFERENTIAL_REFERENCE_STATION_ID"></span><span id="sensor_data_type_differential_reference_station_id"></span>
<strong>SENSOR_DATA_TYPE_DIFFERENTIAL_REFERENCE_STATION_ID</strong> (PID = 37)</td>
<td><p><strong>VT_I4</strong></p>
<p>差异引用工作站的 ID。 范围是 0000 到 1023年。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_ERROR_RADIUS_METERS"></span><span id="sensor_data_type_error_radius_meters"></span>
<strong>SENSOR_DATA_TYPE_ERROR_RADIUS_METERS</strong> (PID = 22)</td>
<td><p><strong>VT_R8</strong></p>
<p>纬度和经度值，以米为单位的准确性。 值为零意味着准确性级别未知。 位置 API 为为此字段提供一个非零值的传感器的优先级。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_FIX_QUALITY"></span><span id="sensor_data_type_fix_quality"></span>
<strong>SENSOR_DATA_TYPE_FIX_QUALITY</strong> (PID = 10)</td>
<td><p><strong>VT_I4</strong></p>
<p>修复质量</p>
<p>0 = 未修复</p>
<p>1 = GPS</p>
<p>2 = DGPS</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_FIX_TYPE"></span><span id="sensor_data_type_fix_type"></span>
<strong>SENSOR_DATA_TYPE_FIX_TYPE</strong> (PID = 11)</td>
<td><p><strong>VT_I4</strong></p>
<p>修复类型</p>
<p>0 = 未修复</p>
<p>1 = GPS SPS 模式下，有效的修补程序</p>
<p>2 = DGPS SPS 模式下，有效的修补程序</p>
<p>3 = GPS PPS 模式下，有效的修补程序</p>
<p>4 = 实时运动</p>
<p>5 = float RTK</p>
<p>6 = 估计 （死信推测）</p>
<p>7 = 手动输入的模式</p>
<p>8 = 模拟器模式</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_GEOIDAL_SEPARATION"></span><span id="sensor_data_type_geoidal_separation"></span>
<strong>SENSOR_DATA_TYPE_GEOIDAL_SEPARATION</strong> (PID = 34)</td>
<td><p><strong>VT_R8</strong></p>
<p>按照 WGS-84 椭圆体和平均值之间的差异 sea 级别。 值小于零表示该 mean sea 级别低于引用椭圆体。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_GPS_OPERATION_MODE"></span><span id="sensor_data_type_gps_operation_mode"></span>
<strong>SENSOR_DATA_TYPE_GPS_OPERATION_MODE</strong> (PID = 32)</td>
<td><p><strong>VT_I4</strong></p>
<p>操作模式。</p>
<p>0 = 手动。 GPS 传感器设置为在二维或三维模式下操作。</p>
<p>1 = automatic。 GPS 传感器可以自动为二维和三维模式之间切换。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_GPS_SELECTION_MODE"></span><span id="sensor_data_type_gps_selection_mode"></span>
<strong>SENSOR_DATA_TYPE_GPS_SELECTION_MODE</strong> (PID = 31)</td>
<td><p><strong>VT_I4</strong></p>
<p>选择模式。</p>
<p>0 = Autonomous。</p>
<p>1 = DGPS.</p>
<p>2 = 估计 （死信推测）。</p>
<p>3 = 手动输入。</p>
<p>4 = 模拟器。</p>
<p>5 = 数据无效。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_GPS_STATUS"></span><span id="sensor_data_type_gps_status"></span>
<strong>SENSOR_DATA_TYPE_GPS_STATUS</strong> (PID = 33)</td>
<td><p><strong>VT_I4</strong></p>
<p>当前数据状态。</p>
<p>1 = 数据是否有效。</p>
<p>2 = 数据无效。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_HORIZONAL_DILUTION_OF_PRECISION"></span><span id="sensor_data_type_horizonal_dilution_of_precision"></span>
<strong>SENSOR_DATA_TYPE_HORIZONAL_DILUTION_OF_PRECISION</strong> (PID = 13)</td>
<td><p><strong>VT_R8</strong></p>
<p>水平了精度系数。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_LATITUDE_DEGREES"></span><span id="sensor_data_type_latitude_degrees"></span>
<strong>SENSOR_DATA_TYPE_LATITUDE_DEGREES</strong> (PID = 2)</td>
<td><p><strong>VT_R8</strong></p>
<p>纬度。 北部为正。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_LONGITUDE_DEGREES"></span><span id="sensor_data_type_longitude_degrees"></span>
<strong>SENSOR_DATA_TYPE_LONGITUDE_DEGREES</strong> (PID = 3)</td>
<td><p><strong>VT_R8</strong></p>
<p>度的经度。 东部为正。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_HEADING_DEGREES"></span><span id="sensor_data_type_magnetic_heading_degrees"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_HEADING_DEGREES</strong> (PID = 8)</td>
<td><p><strong>VT_R8</strong></p>
<p>相对于磁北方，以度为单位的标题。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_MAGNETIC_VARIATION"></span><span id="sensor_data_type_magnetic_variation"></span>
<strong>SENSOR_DATA_TYPE_MAGNETIC_VARIATION</strong> (PID = 9)</td>
<td><p><strong>VT_R8</strong></p>
<p>磁变体。 东部为正。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_NMEA_SENTENCE"></span><span id="sensor_data_type_nmea_sentence"></span>
<strong>SENSOR_DATA_TYPE_NMEA_SENTENCE</strong> (PID = 38)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>当前的 NMEA 句子字符串。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_POSITION_DILUTION_OF_PRECISION"></span><span id="sensor_data_type_position_dilution_of_precision"></span>
<strong>SENSOR_DATA_TYPE_POSITION_DILUTION_OF_PRECISION</strong> (PID = 12)</td>
<td><p><strong>VT_R8</strong></p>
<p>位置了精度系数。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_POSTALCODE"></span><span id="sensor_data_type_postalcode"></span>
<strong>SENSOR_DATA_TYPE_POSTALCODE</strong> (PID = 27)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>邮政编码。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_IN_VIEW"></span><span id="sensor_data_type_satellites_in_view"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_IN_VIEW</strong> (PID = 17)</td>
<td><p><strong>VT_I4</strong></p>
<p>在视图中的附属项的数目。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_AZIMUTH"></span><span id="sensor_data_type_satellites_in_view_azimuth"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_AZIMUTH</strong> (PID = 20)</td>
<td><p><strong>VT_VECTOR|VT_UI1</strong></p>
<p>计数数组，其中包含在视图中的每个附属方位。</p>
<p>向量类型的数据始终序列化为<strong>VT_UI1</strong> （无符号，1 字节字符的一个数组）。 此数据字段实际上包含 IEEE 8 字节实际值为每个值 (<strong>| VT_ R8</strong>)。 使用-1 作为占位符的空值。</p>
<p>有关使用与数组一起使用的信息，请参阅<a href="https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types" data-raw-source="[Retrieving Vector Types](https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types)">检索矢量类型</a>。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_ELEVATION"></span><span id="sensor_data_type_satellites_in_view_elevation"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_ELEVATION</strong> (PID = 19)</td>
<td><p><strong>VT_VECTOR|VT_UI1</strong></p>
<p>计数数组，其中包含的每个附属提升视图中。</p>
<p>向量类型的数据始终序列化为<strong>VT_UI1</strong> （无符号，1 字节字符的一个数组）。 此数据字段实际上包含 IEEE 8 字节实际值为每个值 (<strong>VT_R8</strong>)。 使用-91 作为占位符的空值。</p>
<p>有关使用与数组一起使用的信息，请参阅<a href="https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types" data-raw-source="[Retrieving Vector Types](https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types)">检索矢量类型</a>。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_ID"></span><span id="sensor_data_type_satellites_in_view_id"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_ID</strong> (PID = 39)</td>
<td><p><strong>VT_VECTOR|VT_UI1</strong></p>
<p>统计视图中包含的每个附属 ID 的数组。</p>
<p>向量类型的数据始终序列化为<strong>VT_UI1</strong> （无符号，1 字节字符的一个数组）。 此数据字段实际上包含每个值为 4 字节无符号整数 (<strong>VT_UI4</strong>)。</p>
<p>有关使用与数组一起使用的信息，请参阅<a href="https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types" data-raw-source="[Retrieving Vector Types](https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types)">检索矢量类型</a>。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_PRNS"></span><span id="sensor_data_type_satellites_in_view_prns"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_PRNS</strong> (PID = 18)</td>
<td><p><strong>VT_VECTOR|VT_UI1</strong></p>
<p>计数数组，其中包含的附属项的伪随机噪音代码视图中。</p>
<p>向量类型的数据始终序列化为<strong>VT_UI1</strong> （无符号，1 字节字符的一个数组）。 此数据字段实际上包含每个值为 4 字节无符号整数 (<strong>VT_UI4</strong>)。 使用零 (0) 作为占位符的空值。</p>
<p>有关使用与数组一起使用的信息，请参阅<a href="https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types" data-raw-source="[Retrieving Vector Types](https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types)">检索矢量类型</a>。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_USED_PRNS_AND_CONSTELLATIONS"></span><span id="sensor_data_type_satellites_used_prns_and_constellations"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_USED_PRNS_AND_CONSTELLATIONS</strong> (PID = 41)</td>
<td><p><strong>VT_VECTOR|VT_UI2</strong></p>
<p>计数数组，其中包含解决方案中使用的附属项的伪随机噪音代码。</p>
<p>向量类型的数据始终序列化为<strong>VT_UI2</strong> （无符号的 2 字节字符数组）。 此数据字段必须包含每个值为 4 字节无符号整数 (<strong>VT_UI4</strong>)。 使用零 (0) 作为占位符的空值。</p>
<p>有关使用与数组一起使用的信息，请参阅<a href="https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types" data-raw-source="[Retrieving Vector Types](https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types)">检索矢量类型</a>。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_STN_RATIO"></span><span id="sensor_data_type_satellites_in_view_stn_ratio"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_IN_VIEW_STN_RATIO</strong> (PID = 21)</td>
<td><p><strong>VT_VECTOR|VT_UI1</strong></p>
<p>计数数组视图中包含的附属项干扰信号比率。</p>
<p>向量类型的数据始终序列化为<strong>VT_UI1</strong> （无符号，1 字节字符的一个数组）。 此数据字段实际上包含 IEEE 8 字节实际值为每个值 (<strong>VT_R8</strong>)。 使用零 (0) 作为占位符的空值。</p>
<p>此属性是必需的所有的 GPS 设备必须支持。</p>
<p>有关使用与数组一起使用的信息，请参阅<a href="https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types" data-raw-source="[Retrieving Vector Types](https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types)">检索矢量类型</a>。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_USED_COUNT"></span><span id="sensor_data_type_satellites_used_count"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_USED_COUNT</strong> (PID = 15)</td>
<td><p><strong>VT_I4</strong></p>
<p>在解决方案中使用的附属项的数目。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_SATELLITES_USED_PRNS"></span><span id="sensor_data_type_satellites_used_prns"></span>
<strong>SENSOR_DATA_TYPE_SATELLITES_USED_PRNS</strong> (PID = 16)</td>
<td><p><strong>VT_VECTOR|VT_UI1</strong></p>
<p>计数数组，其中包含解决方案中使用的附属项的伪随机噪音代码。</p>
<p>向量类型的数据始终序列化为<strong>VT_UI1</strong> （无符号，1 字节字符的一个数组）。 此数据字段必须包含每个值为 4 字节无符号整数 (<strong>VT_UI4</strong>)。 使用零 (0) 作为占位符的空值。</p>
<p>有关使用与数组一起使用的信息，请参阅<a href="https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types" data-raw-source="[Retrieving Vector Types](https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types)">检索矢量类型</a>。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_SPEED_KNOTS"></span><span id="sensor_data_type_speed_knots"></span>
<strong>SENSOR_DATA_TYPE_SPEED_KNOTS</strong> (PID = 6)</td>
<td><p><strong>VT_R8</strong></p>
<p>中的节点的速度。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_STATE_PROVINCE"></span><span id="sensor_data_type_state_province"></span>
<strong>SENSOR_DATA_TYPE_STATE_PROVINCE</strong> (PID = 26)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>省/市/自治区。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_DATA_TYPE_TRUE_HEADING_DEGREES"></span><span id="sensor_data_type_true_heading_degrees"></span>
<strong>SENSOR_DATA_TYPE_TRUE_HEADING_DEGREES</strong> (PID = 7)</td>
<td><p><strong>VT_R8</strong></p>
<p>标题时，相对于真北，以度为单位。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_DATA_TYPE_VERTICAL_DILUTION_OF_PRECISION"></span><span id="sensor_data_type_vertical_dilution_of_precision"></span>
<strong>SENSOR_DATA_TYPE_VERTICAL_DILUTION_OF_PRECISION</strong> (PID = 14)</td>
<td><p><strong>VT_R8</strong></p>
<p>垂直了精度系数。</p></td>
</tr>
</tbody>
</table>

 

 





