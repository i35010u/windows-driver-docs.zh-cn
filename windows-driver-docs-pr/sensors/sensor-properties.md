---
title: 传感器属性
description: 传感器和位置平台定义标识传感器属性的常量。 传感器制造商还可以定义自己的属性。
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
ms.openlocfilehash: f24c786004599f08ead29a7f5920ed9d28eef5a1
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423502"
---
# <a name="sensor-properties"></a>传感器属性


传感器和位置平台定义标识传感器属性的常量。 传感器制造商还可以定义自己的属性。

平台为传感器属性定义以下 **PROPERTYKEY** 值。 除非另有说明，否则这些属性是只读的。

每个平台定义的传感器属性**PROPERTYKEY**基于一个名为 "传感器**GUID** \_ 属性 \_ 公用 guid \_ " 的通用 guid：

{7F8383EC-D3EC-495C-A8CF-B8BBE85C2920}.

**重要提示**   不要使用此基值来定义自己的属性键。

 

指定为读/写的属性的值可由客户端应用程序指定。 指定为 static 的属性的值不能随时间而更改。 传感器必须支持指定为 "必需" 的属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性键名称和 PID</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_ACCURACY_"></span><span id="sensor_property_accuracy_"></span>
<strong>SENSOR_PROPERTY_ACCURACY</strong> (PID = 17) </td>
<td><p>VT_UNKNOWN</p>
<p>只读。 包含传感器数据类型名称及其关联准确性的<a href="https://go.microsoft.com/fwlink/p/?linkid=134660" data-raw-source="[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=134660)">IPortableDeviceValues</a>对象。 准确性值表示可能与真实值之间的差异。 使用与数据字段相同的单位表示准确性值，但在其他情况下也是如此。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_CHANGE_SENSITIVITY"></span><span id="sensor_property_change_sensitivity"></span>
<strong>SENSOR_PROPERTY_CHANGE_SENSITIVITY</strong> (PID = 14) </td>
<td><p>VT_UNKNOWN</p>
<p>读/写。 包含传感器数据类型名称及其关联的更改敏感度值的<strong>IPortableDeviceValues</strong>对象。 更改敏感度值提供有关数据字段在引发 SENSOR_EVENT_DATA_UPDATED 事件之前应更改的量的请求。</p>
<p>通过使用与数据字段相同的单位来表示敏感度值，但在其他情况下也是如此。</p>
<p>对于某些传感器，更改敏感度会解释为实际值。 例如，SENSOR_DATA_TYPE_TEMPERATURE_CELSIUS 的更改敏感度值为2，表示对加或减2度摄氏的灵敏度。</p>
<p>对于其他传感器，如环境光线传感器 (ALS) ，更改敏感度将被解释为百分比。 因此，SENSOR_DATA_TYPE_LIGHT_LEVEL_LUX 的更改敏感度为2，则表示加上或减2% 的 LUX。</p>
<p>您可以将此值设置为请求特定的更改敏感度，但多个应用程序可能使用同一传感器。 因此，传感器基于其内部逻辑来确定真正的更改敏感度。 例如，传感器可能始终使用任何应用程序所请求的最小更改敏感度。</p>
<p>如果应用程序将此属性设置为 VT_NULL，则设备驱动程序应将 SENSOR_PROPERTY_CHANGE_SENSITIVITY 重置为其默认值。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_CONNECTION_TYPE"></span><span id="sensor_property_connection_type"></span>
<strong>SENSOR_PROPERTY_CONNECTION_TYPE</strong> (PID = 11) </td>
<td><p>VT_UI4</p>
<p>只读。 包含当前连接类型的<a href="/windows/win32/api/sensorsapi/ne-sensorsapi-_midl___midl_itf_sensorsapi_0000_0000_0002" data-raw-source="[&lt;strong&gt;SensorConnectionType&lt;/strong&gt;](/windows/win32/api/sensorsapi/ne-sensorsapi-__midl___midl_itf_sensorsapi_0000_0000_0002)"><strong>SensorConnectionType</strong></a>值。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL"></span><span id="sensor_property_current_report_interval"></span>
<strong>SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL</strong> (PID = 13) </td>
<td><p>VT_UI4</p>
<p>读/写。 传感器数据报表生成的当前运行时间（以毫秒为单位）。</p>
<p>如果将值设置为零，则表示驱动程序返回：默认报表间隔，或者是最小报表间隔。 如果仅有一个客户端连接，则驱动程序应返回默认报告间隔。 如果连接了多个客户端，则驱动程序应返回其中任何一个客户端所请求的最小间隔。</p>
<p>应用程序可以将此值设置为请求特定的报表间隔，但多个应用程序可能使用同一个驱动程序。 因此，驱动程序将基于内部逻辑来确定真实的报表时间间隔。 例如，驱动程序可能始终使用由任何调用方请求的最短报表间隔。</p>
<p>有关如何使用此属性的示例，请参阅 <a href="/windows/desktop/SensorsAPI/using-sensor-api-events" data-raw-source="[Using Sensor API Events](/windows/desktop/SensorsAPI/using-sensor-api-events)">使用传感器 API 事件</a>。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_DESCRIPTION"></span><span id="sensor_property_description"></span>
<strong>SENSOR_PROPERTY_DESCRIPTION</strong> (PID = 10) </td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>只读。 传感器描述字符串。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_DEVICE_PATH"></span><span id="sensor_property_device_path"></span>
<strong>SENSOR_PROPERTY_DEVICE_PATH</strong> (PID = 15) </td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>只读。 唯一标识与传感器关联的设备实例。 你可以使用此属性来确定设备是否包含多个传感器。</p>
<p>设备驱动程序无需支持此属性，因为平台在不查询驱动程序的情况下向应用程序提供此值。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_FRIENDLY_NAME"></span><span id="sensor_property_friendly_name"></span>
<strong>SENSOR_PROPERTY_FRIENDLY_NAME</strong> (PID = 9) </td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>只读。 必需，static。 设备的友好名称。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_LIGHT_RESPONSE_CURVE"></span><span id="sensor_property_light_response_curve"></span>
<strong>SENSOR_PROPERTY_LIGHT_RESPONSE_CURVE</strong> (PID = 16) </td>
<td><p><strong>VT_VECTOR |VT_UI1</strong></p>
<p>只读。 一个计数数组，其中包含一对值，这些值提供在环境光线级别与偏移量之间的映射。 这些值表示为百分比。 Windows 中的自适应亮度功能将这些值应用于用户的当前显示亮度首选项。</p>
<p>矢量类型的数据始终序列化为 <strong>VT_UI1</strong> (一个) 的无符号、1字节字符数组。 此属性实际包含每个值作为4字节无符号整数 (<strong>VT_UI4) </strong>。 有关使用数组的信息，请参阅 <a href="/windows/desktop/SensorsAPI/retrieving-vector-types" data-raw-source="[Retrieving Vector Types](/windows/desktop/SensorsAPI/retrieving-vector-types)">检索矢量类型</a>。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_LOCATION_DESIRED_ACCURACY"></span><span id="sensor_property_location_desired_accuracy"></span>
<strong>SENSOR_PROPERTY_LOCATION_DESIRED_ACCURACY</strong> (PID = 19) </td>
<td><p>VT_UI4</p>
<p>读/写。 <a href="/previous-versions/windows/desktop/legacy/dd756639(v=vs.85)" data-raw-source="[&lt;strong&gt;LOCATION_DESIRED_ACCURACY&lt;/strong&gt;](/previous-versions/windows/desktop/legacy/dd756639(v=vs.85))"><strong>LOCATION_DESIRED_ACCURACY</strong></a>枚举中的一个值，该值指示客户端应用程序请求的准确性处理的类型。</p>
<p><strong>LOCATION_DESIRED_ACCURACY_DEFAULT</strong> (0) 指示传感器应使用其可优化电源使用情况和其他成本注意事项的准确性。</p>
<p><strong>LOCATION_DESIRED_ACCURACY_HIGH</strong> (1) 指示传感器应提供最准确的报告。 这包括使用可能收费的服务或消耗更高级别的电池电量或连接带宽。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_MANUFACTURER"></span><span id="sensor_property_manufacturer"></span>
<strong>SENSOR_PROPERTY_MANUFACTURER</strong> (PID = 6) </td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>只读。 必需，static。 制作者类的名称。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_MIN_REPORT_INTERVAL"></span><span id="sensor_property_min_report_interval"></span>
<strong>SENSOR_PROPERTY_MIN_REPORT_INTERVAL</strong> (PID = 12) </td>
<td><p>VT_UI4</p>
<p>只读。 必需，static。 硬件支持的传感器数据报表生成的最小时间间隔（毫秒）。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_MODEL"></span><span id="sensor_property_model"></span>
<strong>SENSOR_PROPERTY_MODEL</strong> (PID = 7) </td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>只读。 必需，static。 传感器型号名称。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_PERSISTENT_UNIQUE_ID"></span><span id="sensor_property_persistent_unique_id"></span>
<strong>SENSOR_PROPERTY_PERSISTENT_UNIQUE_ID</strong> (PID = 5) </td>
<td><p><strong>VT_CLSID</strong></p>
<p>只读。 必需，static。 标识传感器的 <strong>GUID</strong> 。 对于设备上的每个传感器，此值必须是唯一的，对于在计算机上枚举的同一模型，此值必须是唯一的。 此属性包含通过调用 <a href="/windows/win32/api/sensorsapi/nf-sensorsapi-isensor-getid" data-raw-source="[&lt;strong&gt;ISensor::GetID&lt;/strong&gt;](/windows/win32/api/sensorsapi/nf-sensorsapi-isensor-getid)"><strong>ISensor：： GetID</strong></a> 获取的相同值。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_RANGE_MAXIMUM"></span><span id="sensor_property_range_maximum"></span>
<strong>SENSOR_PROPERTY_RANGE_MAXIMUM</strong> (PID = 21) </td>
<td><p><strong>VT_UKNOWN</strong></p>
<p>只读。 包含传感器数据字段名称及其关联的最大值的<strong>IPortableDeviceValues</strong>对象。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_RANGE_MINIMUM"></span><span id="sensor_property_range_minimum"></span>
<strong>SENSOR_PROPERTY_RANGE_MINIMUM</strong> (PID = 20) </td>
<td><p><strong>VT_UKNOWN</strong></p>
<p>只读。 包含传感器数据字段名称及其关联的最小值的<strong>IPortableDeviceValues</strong>对象。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_RESOLUTION"></span><span id="sensor_property_resolution"></span>
<strong>SENSOR_PROPERTY_RESOLUTION</strong> (PID = 18) </td>
<td><p><strong>VT_UKNOWN</strong></p>
<p>只读。 包含传感器数据字段名称及其关联解决方案的<strong>IPortableDeviceValues</strong>对象。 解析值表示在数据字段中更改的敏感度。</p>
<p>解析值使用与数据字段相同的单位来表示，但在其他情况下除外。</p></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_SERIAL_NUMBER"></span><span id="sensor_property_serial_number"></span>
<strong>SENSOR_PROPERTY_SERIAL_NUMBER</strong> (PID = 8) </td>
<td><p><strong>VT_LPWSTR</strong></p>
<p>只读。 必需，static。 传感器序列号。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_STATE"></span><span id="sensor_property_state"></span>
<strong>SENSOR_PROPERTY_STATE</strong> (PID = 3) </td>
<td><p>VT_UI4</p>
<p>只读。 必需。</p>
<p>包含当前传感器状态的<a href="/windows/win32/api/sensorsapi/ne-sensorsapi-_midl___midl_itf_sensorsapi_0000_0000_0001" data-raw-source="[&lt;strong&gt;SensorState&lt;/strong&gt;](/windows/win32/api/sensorsapi/ne-sensorsapi-__midl___midl_itf_sensorsapi_0000_0000_0001)"><strong>SensorState</strong></a>值。</p>
<div class="alert">
<strong>注意</strong>  若要更新此属性，请通过调用 <a href="/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange" data-raw-source="[&lt;strong&gt;ISensorClassExtension::PostStateChange&lt;/strong&gt;](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)"><strong>ISensorClassExtension：:P oststatechange</strong></a>引发状态更改事件。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td><span id="SENSOR_PROPERTY_TURN_ON_OFF_NMEA"></span><span id="sensor_property_turn_on_off_nmea"></span>
<strong>SENSOR_PROPERTY_TURN_ON_OFF_NMEA</strong> (PID = 3) </td>
<td><p>VT_UI4</p>
<p>读/写。 如果为 TRUE，则 NMEA 句子将包含在数据报表中。 如果为 False，则不包含 NMEA 句子。</p></td>
</tr>
<tr class="even">
<td><span id="SENSOR_PROPERTY_TYPE"></span><span id="sensor_property_type"></span>
<strong>SENSOR_PROPERTY_TYPE</strong> (PID = 2) </td>
<td><p><strong>VT_CLSID</strong></p>
<p>只读。 必需，static。 标识传感器类型的 <strong>GUID</strong> 。 在传感器中定义了平台定义的传感器类型。</p></td>
</tr>
</tbody>
</table>

所有传感器都必须支持以下 (WPD) 属性的 Windows 便携式设备。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性键</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span id="WPD_FUNCTIONAL_OBJECT_CATEGORY"></span><span id="wpd_functional_object_category"></span>
<strong>WPD_FUNCTIONAL_OBJECT_CATEGORY</strong></td>
<td><p><strong>VT_CLSID</strong></p>
<p>只读。 必需，static。 定义传感器类别。</p></td>
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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**GetProperties**](/windows/win32/api/sensorsapi/nf-sensorsapi-isensor-getproperties)

[**GetProperty**](/windows/win32/api/sensorsapi/nf-sensorsapi-isensor-getproperty)

[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=275070)

[**SetProperties**](/windows/win32/api/sensorsapi/nf-sensorsapi-isensor-setproperties)

