---
title: 传感器 \_ 类别 \_ 指示灯
description: 传感器 \_ 类别 \_ 轻型类别包含的传感器提供了有关光线特征的信息。
keywords:
- SENSOR_CATEGORY_LIGHT 传感器设备
topic_type:
- apiref
api_name:
- SENSOR_CATEGORY_LIGHT
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: d7663bfca5c82b4d94affee5f078eb16945fdb2d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812213"
---
# <a name="sensor_category_light"></a>传感器 \_ 类别 \_ 指示灯


传感器 \_ 类别 \_ 轻型类别包含的传感器提供了有关光线特征的信息。

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
<td><p>SENSOR_TYPE_AMBIENT_LIGHT</p></td>
<td><p>环境光线传感器。</p></td>
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
<td><p>SENSOR_DATA_TYPE_LIGHT_CHROMACITY</p></td>
<td><p><strong>VT_VECTOR</strong> |<strong>VT_UI1</strong></p></td>
<td><p>Chromaticity 作为浮点值的计数数组。</p>
<p>矢量类型的数据始终序列化为 VT_UI1 (一个) 的无符号、单字节字符数组。 此数据字段必须包含每个值作为 IEEE 四字节实数值 (VT_R4) 。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_LIGHT_LEVEL_LUX</p></td>
<td><p>VT_R4</p></td>
<td><p>Illuminance 级别，在 lux 中。</p>
<p></p>
<p>请注意，设备驱动程序还需要使用一种类型的 VT_UI4 来处理此数据字段。  (在 Windows 8 之前制造的轻型传感器存在此要求。 ) </p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_LIGHT_TEMPERATURE_KELVIN</p></td>
<td><p>VT_R4</p></td>
<td><p>开氏度的色温。</p></td>
</tr>
</tbody>
</table>

 

**重要提示**  每个平台定义的轻型数据类型 **PROPERTYKEY** 均基于一个名为 "传感器 **GUID** \_ 数据 \_ 类型 \_ 轻型 guid" 的通用 GUID \_ 。 由于这是保留的基值，请不要使用此 **GUID** 来定义自己的属性键。

 

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

 

 





