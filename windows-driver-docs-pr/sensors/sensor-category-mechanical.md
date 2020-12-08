---
title: 传感器 \_ 类别 \_ 机械
description: 传感器 \_ 类别 \_ 机械类别包含提供与机制相关的信息的传感器。
keywords:
- SENSOR_CATEGORY_MECHANICAL 传感器设备
topic_type:
- apiref
api_name:
- SENSOR_CATEGORY_MECHANICAL
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: a54bc3a07d3c023b1b1e74d524f3ef2cbefbc5aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812207"
---
# <a name="sensor_category_mechanical"></a>传感器 \_ 类别 \_ 机械


传感器 \_ 类别 \_ 机械类别包含提供与机制相关的信息的传感器。

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
<td><p>SENSOR_TYPE_BOOLEAN_SWITCH</p></td>
<td><p>两状态开关 (关闭或) 。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_FORCE</p></td>
<td><p>强制传感器。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_TYPE_MULTIVALUE_SWITCH</p></td>
<td><p>多位置开关。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_PRESSURE</p></td>
<td><p>压力传感器。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_TYPE_SCALE</p></td>
<td><p>权重传感器。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_STRAIN</p></td>
<td><p>紧张传感器。</p></td>
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
<td><p>SENSOR_DATA_TYPE_ABSOLUTE_PRESSURE_PASCAL</p></td>
<td><p>VT_R8</p></td>
<td><p>绝对压力，采用帕斯卡。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_BOOLEAN_SWITCH_STATE</p></td>
<td><p>VT_BOOL</p></td>
<td><p>SENSOR_TYPE_BOOLEAN_SWITCH 的状态字段。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_FORCE_NEWTONS</p></td>
<td><p>VT_R8</p></td>
<td><p>强制，在 newtons 中。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_GAUGE_PRESSURE_PASCAL</p></td>
<td><p>VT_R8</p></td>
<td><p>相对仪表压力，采用帕斯卡。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_MULTIVALUE_SWITCH_STATE</p></td>
<td><p>VT_R8</p></td>
<td><p>SENSOR_TYPE_MULTIVALUE_SWITCH 的状态字段。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_STRAIN</p></td>
<td><p>VT_R8</p></td>
<td><p>压力.</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_WEIGHT_KILOGRAMS</p></td>
<td><p>VT_R8</p></td>
<td><p>权重，以千克为重量。</p></td>
</tr>
</tbody>
</table>

 

**重要提示**  每个平台定义的机械数据类型 **PROPERTYKEY** 均基于一个名为 "传感器 **GUID** \_ 数据类型" \_ \_ 机械 \_ guid 的通用 GUID。 由于这是保留的基值，请不要使用此 **GUID** 来定义自己的属性键。

 

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

 

 





