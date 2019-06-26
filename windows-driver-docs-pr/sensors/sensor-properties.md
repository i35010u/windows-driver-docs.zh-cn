---
title: 传感器属性
description: 传感器和位置平台定义一些常量，标识属性的传感器。 传感器制造商还可以定义其自己的属性。
ms.assetid: a9f88dad-a81d-45dc-b607-e7b4c5036774
topic_type:
- apiref
api_name:
- SENSOR_PROPERTY_ACCURACY
- SENSOR_PROPERTY_CHANGE_SENSITIVITY
- SENSOR_PROPERTY_CONNECTION_TYPE
- SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL
- SENSOR_PROPERTY_DESCRIPTION
- SENSOR_PROPERTY_DEVICE_PATH
- SENSOR_PROPERTY_FRIENDLY_NAME
- SENSOR_PROPERTY_LIGHT_RESPONSE_CURVE
- SENSOR_PROPERTY_LOCATION_DESIRED_ACCURACY
- SENSOR_PROPERTY_MANUFACTURER
- SENSOR_PROPERTY_MIN_REPORT_INTERVAL
- SENSOR_PROPERTY_MODEL
- SENSOR_PROPERTY_PERSISTENT_UNIQUE_ID
- SENSOR_PROPERTY_RANGE_MAXIMUM
- SENSOR_PROPERTY_RANGE_MINIMUM
- SENSOR_PROPERTY_RESOLUTION
- SENSOR_PROPERTY_SERIAL_NUMBER
- SENSOR_PROPERTY_STATE
- SENSOR_PROPERTY_TURN_ON_OFF_NMEA
- SENSOR_PROPERTY_TYPE
- WPD_FUNCTIONAL_OBJECT_CATEGORY
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 904dab515b04b4a838ec6ecb132e35b11c6dd3a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387178"
---
# <a name="sensor-properties"></a>传感器属性


传感器和位置平台定义一些常量，标识属性的传感器。 传感器制造商还可以定义其自己的属性。

平台定义了以下**PROPERTYKEY**传感器属性的值。 这些属性是只读的除非另有说明。

每个平台定义传感器属性**PROPERTYKEY**基于一种常见**GUID**名为传感器\_属性\_常见\_GUID:

{7F8383EC-D3EC-495C-A8CF-B8BBE85C2920}。

**重要**  不使用此基值来定义你自己属性的密钥。

 

指定为客户端应用程序时可以指定读/写属性的值。 指定为静态属性的值必须不随时间变化。 必须由传感器支持指定为所需的属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性的密钥名称和 PID</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_ACCURACY_"></span><span id="sensor_property_accuracy_"></span>
<strong>SENSOR_PROPERTY_ACCURACY</strong> (PID = 17)</td>
<td><p><strong>VT_UNKNOWN</strong></p>
<p>只读属性。 <a href="https://go.microsoft.com/fwlink/p/?linkid=134660" data-raw-source="[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=134660)">IPortableDeviceValues</a>对象，其中包含传感器数据类型名称和其关联的准确性。 准确性值表示从 true 值可能变体。 准确性值表示为数据字段，除非时有说明，否则使用相同的单位。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_CHANGE_SENSITIVITY"></span><span id="sensor_property_change_sensitivity"></span>
<strong>SENSOR_PROPERTY_CHANGE_SENSITIVITY</strong> (PID = 14)</td>
<td><p><strong>VT_UNKNOWN</strong></p>
<p>读/写。 <strong>IPortableDeviceValues</strong>包含传感器数据的类型名称及其关联的更改敏感度值的对象。 更改敏感度值提供有关所依据的数据字段应更改 SENSOR_EVENT_DATA_UPDATED 事件引发之前所占用的请求。</p>
<p>敏感度值表示其中有说明，否则，除使用数据字段的单位相同。</p>
<p>对于某些传感器，变化敏感度被解释为实际值。 例如，2 表示 SENSOR_DATA_TYPE_TEMPERATURE_CELSIUS 更改敏感度值表示敏感度加或减 2 摄氏度。</p>
<p>对于其他传感器，环境光线传感器 (ALS)，如变化敏感度被解释为百分比。 因此，2 表示 SENSOR_DATA_TYPE_LIGHT_LEVEL_LUX 变化敏感度表示加上或减去的 LUX 2%。</p>
<p>可以设置此值以请求特定更改敏感度，但多个应用程序可能正在使用相同的传感器。 因此，传感器确定 true 变化敏感度，基于其内部逻辑。 例如，传感器可能始终使用最小的变化敏感度的请求的任何应用程序。</p>
<p>如果应用程序将此属性设置为 VT_NULL，设备驱动程序应重置 SENSOR_PROPERTY_CHANGE_SENSITIVITY 为其默认值。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_CONNECTION_TYPE"></span><span id="sensor_property_connection_type"></span>
<strong>SENSOR_PROPERTY_CONNECTION_TYPE</strong> (PID = 11)</td>
<td><p><strong>VT_UI4</strong></p>
<p>只读属性。 <a href="https://docs.microsoft.com/windows/desktop/api/sensorsapi/ne-sensorsapi-__midl___midl_itf_sensorsapi_0000_0000_0002" data-raw-source="[&lt;strong&gt;SensorConnectionType&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/sensorsapi/ne-sensorsapi-__midl___midl_itf_sensorsapi_0000_0000_0002)"><strong>SensorConnectionType</strong> </a>值，该值包含当前的连接类型。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL"></span><span id="sensor_property_current_report_interval"></span>
<strong>SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL</strong> (PID = 13)</td>
<td><p><strong>VT_UI4</strong></p>
<p>读/写。 当前的运行时间的传感器数据报告生成，以毫秒为单位。</p>
<p>将值设置为零发出信号要返回的驱动程序： 默认报表时间间隔内，或最小的报告间隔。 如果只有一个客户端连接，则驱动程序应返回默认报表时间间隔。 如果多个客户端连接，则驱动程序应返回请求的任何这些客户端的最小时间间隔。</p>
<p>应用程序可以设置此值以请求特定的报告间隔，但多个应用程序可能正在使用相同的驱动程序。 因此，驱动程序确定，则返回 true 的报告间隔，基于内部逻辑。 例如，驱动程序可能会始终使用最短请求的任何调用方的报告间隔。</p>
<p>有关如何使用此属性的示例，请参阅<a href="https://docs.microsoft.com/windows/desktop/SensorsAPI/using-sensor-api-events" data-raw-source="[Using Sensor API Events](https://docs.microsoft.com/windows/desktop/SensorsAPI/using-sensor-api-events)">使用传感器 API 事件</a>。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_DESCRIPTION"></span><span id="sensor_property_description"></span>
<strong>SENSOR_PROPERTY_DESCRIPTION</strong> (PID = 10)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>只读属性。 传感器说明字符串。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_DEVICE_PATH"></span><span id="sensor_property_device_path"></span>
<strong>SENSOR_PROPERTY_DEVICE_PATH</strong> (PID = 15)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>只读属性。 唯一地标识传感器与之关联的设备实例。 此属性可用于确定设备是否包含多个传感器。</p>
<p>设备驱动程序不需要支持此属性，因为平台会提供此值设置为应用程序而无需查询驱动程序。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_FRIENDLY_NAME"></span><span id="sensor_property_friendly_name"></span>
<strong>SENSOR_PROPERTY_FRIENDLY_NAME</strong> (PID = 9)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>只读属性。 必需的静态。 设备的友好名称。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_LIGHT_RESPONSE_CURVE"></span><span id="sensor_property_light_response_curve"></span>
<strong>SENSOR_PROPERTY_LIGHT_RESPONSE_CURVE</strong> (PID = 16)</td>
<td><p><strong>VT_VECTOR|VT_UI1</strong></p>
<p>只读属性。 包含提供环境的亮度级别和偏移量之间的映射的值对的计数的数组。 这些值表示为百分比。 Windows 中的自适应亮度功能适用于用户的当前显示亮度首选项的这些值。</p>
<p>向量类型的数据始终序列化为<strong>VT_UI1</strong> （无符号，1 字节字符的一个数组）。 此属性实际包含每个值为 4 字节无符号整数 (<strong>VT_UI4)</strong>。 有关使用与数组一起使用的信息，请参阅<a href="https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types" data-raw-source="[Retrieving Vector Types](https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-vector-types)">检索矢量类型</a>。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_LOCATION_DESIRED_ACCURACY"></span><span id="sensor_property_location_desired_accuracy"></span>
<strong>SENSOR_PROPERTY_LOCATION_DESIRED_ACCURACY</strong> (PID = 19)</td>
<td><p><strong>VT_UI4</strong></p>
<p>读/写。 中的值<a href="https://docs.microsoft.com/previous-versions/windows/desktop/legacy/dd756639(v=vs.85)" data-raw-source="[&lt;strong&gt;LOCATION_DESIRED_ACCURACY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/dd756639(v=vs.85))"> <strong>LOCATION_DESIRED_ACCURACY</strong> </a>枚举，指示准确性处理请求的客户端应用程序的类型。</p>
<p><strong>LOCATION_DESIRED_ACCURACY_DEFAULT</strong> (0) 指示传感器应使用它可以为其优化的电源和其他成本考虑事项的准确性。</p>
<p><strong>LOCATION_DESIRED_ACCURACY_HIGH</strong> (1) 指示传感器，应提供可能最准确的报告。 这包括使用可能收费的服务或消耗更高级别的电池电量或连接带宽。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_MANUFACTURER"></span><span id="sensor_property_manufacturer"></span>
<strong>SENSOR_PROPERTY_MANUFACTURER</strong> (PID = 6)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>只读属性。 必需的静态。 制造商的名称。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_MIN_REPORT_INTERVAL"></span><span id="sensor_property_min_report_interval"></span>
<strong>SENSOR_PROPERTY_MIN_REPORT_INTERVAL</strong> (PID = 12)</td>
<td><p><strong>VT_UI4</strong></p>
<p>只读属性。 必需的静态。 硬件传感器数据生成报告，以毫秒为单位支持最小时间间隔。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_MODEL"></span><span id="sensor_property_model"></span>
<strong>SENSOR_PROPERTY_MODEL</strong> (PID = 7)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>只读属性。 必需的静态。 传感器模型名称。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_PERSISTENT_UNIQUE_ID"></span><span id="sensor_property_persistent_unique_id"></span>
<strong>SENSOR_PROPERTY_PERSISTENT_UNIQUE_ID</strong> (PID = 5)</td>
<td><p><strong>VT_CLSID</strong></p>
<p>只读属性。 必需的静态。 一个<strong>GUID</strong>标识传感器。 此值必须是唯一的设备，或者跨多个设备作为枚举在计算机上的同一模型的每个传感器。 此属性包含通过调用获取的相同值<a href="https://docs.microsoft.com/windows/desktop/api/sensorsapi/nf-sensorsapi-isensor-getid" data-raw-source="[&lt;strong&gt;ISensor::GetID&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/sensorsapi/nf-sensorsapi-isensor-getid)"> <strong>ISensor::GetID</strong> </a> 。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_RANGE_MAXIMUM"></span><span id="sensor_property_range_maximum"></span>
<strong>SENSOR_PROPERTY_RANGE_MAXIMUM</strong> (PID = 21)</td>
<td><p><strong>VT_UKNOWN</strong></p>
<p>只读属性。 <strong>IPortableDeviceValues</strong>包含传感器数据字段的名称及其关联的最大值的对象。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_RANGE_MINIMUM"></span><span id="sensor_property_range_minimum"></span>
<strong>SENSOR_PROPERTY_RANGE_MINIMUM</strong> (PID = 20)</td>
<td><p><strong>VT_UKNOWN</strong></p>
<p>只读属性。 <strong>IPortableDeviceValues</strong>包含传感器数据字段的名称及其关联的最小值的对象。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_RESOLUTION"></span><span id="sensor_property_resolution"></span>
<strong>SENSOR_PROPERTY_RESOLUTION</strong> (PID = 18)</td>
<td><p><strong>VT_UKNOWN</strong></p>
<p>只读属性。 <strong>IPortableDeviceValues</strong>对象，其中包含传感器数据字段名称和及其相关联的解决方法。 解决方法的值表示数据字段中更改的敏感度。</p>
<p>使用的相同单位为数据字段中，除时有说明，否则表示的分辨率值。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_SERIAL_NUMBER"></span><span id="sensor_property_serial_number"></span>
<strong>SENSOR_PROPERTY_SERIAL_NUMBER</strong> (PID = 8)</td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>只读属性。 必需的静态。 传感器序列号。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_STATE"></span><span id="sensor_property_state"></span>
<strong>SENSOR_PROPERTY_STATE</strong> (PID = 3)</td>
<td><p><strong>VT_UI4</strong></p>
<p>只读属性。 必需。</p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/sensorsapi/ne-sensorsapi-__midl___midl_itf_sensorsapi_0000_0000_0001" data-raw-source="[&lt;strong&gt;SensorState&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/sensorsapi/ne-sensorsapi-__midl___midl_itf_sensorsapi_0000_0000_0001)"><strong>SensorState</strong> </a>值，该值包含当前的传感器状态。</p>
<div class="alert">
<strong>请注意</strong>若要更新此属性，引发状态更改事件，通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange" data-raw-source="[&lt;strong&gt;ISensorClassExtension::PostStateChange&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)"> <strong>ISensorClassExtension::PostStateChange</strong></a>。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_TURN_ON_OFF_NMEA"></span><span id="sensor_property_turn_on_off_nmea"></span>
<strong>SENSOR_PROPERTY_TURN_ON_OFF_NMEA</strong> (PID = 3)</td>
<td><p><strong>VT_UI4</strong></p>
<p>读/写。 如果为 TRUE，将在数据报表中包含 NMEA 句子。 如果为 False，则不包含 NMEA 句子。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_TYPE"></span><span id="sensor_property_type"></span>
<strong>SENSOR_PROPERTY_TYPE</strong> (PID = 2)</td>
<td><p><strong>VT_CLSID</strong></p>
<p>只读属性。 必需的静态。 一个<strong>GUID</strong>标识的传感器类型。 平台定义的传感器类型 Sensors.h 中定义。</p></td>
</tr>
</tbody>
</table>

以下 Windows 便携式设备 (WPD) 属性必须受所有传感器。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性键</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span id="WPD_FUNCTIONAL_OBJECT_CATEGORY"></span><span id="wpd_functional_object_category"></span>
<strong>WPD_FUNCTIONAL_OBJECT_CATEGORY</strong></td>
<td><p><strong>VT_CLSID</strong></p>
<p>只读属性。 必需的静态。 定义的传感器类别。</p></td>
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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**GetProperties**](https://docs.microsoft.com/windows/desktop/api/sensorsapi/nf-sensorsapi-isensor-getproperties)

[**GetProperty**](https://docs.microsoft.com/windows/desktop/api/sensorsapi/nf-sensorsapi-isensor-getproperty)

[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=275070)

[**SetProperties**](https://docs.microsoft.com/windows/desktop/api/sensorsapi/nf-sensorsapi-isensor-setproperties)

 

 






