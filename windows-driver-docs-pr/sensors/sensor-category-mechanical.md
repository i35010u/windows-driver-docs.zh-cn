---
title: 传感器\_类别\_机械
description: 传感器\_类别\_机械类别包含提供机制与相关的信息的传感器。
ms.assetid: 0ae66a5b-6564-4e2c-a6a1-c88c7e853a38
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
ms.openlocfilehash: 9c8b3ae3814050d922287f8c1fd6831e50afa87e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543900"
---
# <a name="sensorcategorymechanical"></a>传感器\_类别\_机械


传感器\_类别\_机械类别包含提供机制与相关的信息的传感器。

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
<td><p>SENSOR_TYPE_BOOLEAN_SWITCH</p></td>
<td><p>两种状态切换 （关闭或打开）。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_FORCE</p></td>
<td><p>强制传感器。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_TYPE_MULTIVALUE_SWITCH</p></td>
<td><p>多个位置的开关。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_PRESSURE</p></td>
<td><p>压力的传感器。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_TYPE_SCALE</p></td>
<td><p>权重的传感器。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_STRAIN</p></td>
<td><p>压力的传感器。</p></td>
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
<td><p>SENSOR_DATA_TYPE_ABSOLUTE_PRESSURE_PASCAL</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>绝对压力，帕斯卡中。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_BOOLEAN_SWITCH_STATE</p></td>
<td><p><strong>VT_BOOL</strong></p></td>
<td><p>SENSOR_TYPE_BOOLEAN_SWITCH 状态字段。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_FORCE_NEWTONS</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>强制以牛顿为单位。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_GAUGE_PRESSURE_PASCAL</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>相对仪表压力，帕斯卡中。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_MULTIVALUE_SWITCH_STATE</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>SENSOR_TYPE_MULTIVALUE_SWITCH 状态字段。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_STRAIN</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>疲劳。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_WEIGHT_KILOGRAMS</p></td>
<td><p><strong>VT_R8</strong></p></td>
<td><p>千克中的权重。</p></td>
</tr>
</tbody>
</table>

 

**重要**  每个平台定义机械数据类型**PROPERTYKEY**基于一种常见**GUID**名为传感器\_数据\_类型\_机械\_GUID。 由于它是保留的基值，请勿使用此**GUID**来定义你自己属性的密钥。

 

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

 

 





