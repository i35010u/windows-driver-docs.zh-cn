---
title: 传感器\_类别\_光
description: 传感器\_类别\_浅类别包含提供有关光的特征的信息的传感器。
ms.assetid: 56bb4869-3752-437d-89c9-829e6fb01043
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
ms.openlocfilehash: b4ca05c45f2f7c03d93c450bc41a6febf266d8ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370323"
---
# <a name="sensorcategorylight"></a>传感器\_类别\_光


传感器\_类别\_浅类别包含提供有关光的特征的信息的传感器。

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
<td><p>SENSOR_TYPE_AMBIENT_LIGHT</p></td>
<td><p>环境光线传感器。</p></td>
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
<td><p>SENSOR_DATA_TYPE_LIGHT_CHROMACITY</p></td>
<td><p><strong>VT_VECTOR</strong>|<strong>VT_UI1</strong></p></td>
<td><p>为浮点值的计数数组色度。</p>
<p>向量类型的数据始终序列化为 VT_UI1 （无符号，单字节字符的一个数组）。 此数据字段必须为 IEEE 四字节实际值 (VT_R4) 包含每个值。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_DATA_TYPE_LIGHT_LEVEL_LUX</p></td>
<td><p><strong>VT_R4</strong></p></td>
<td><p>Lux 中 illuminance 级别。</p>
<p></p>
<p>请注意，设备驱动程序需要以处理此数据字段的一种类型的 VT_UI4。 （此要求存在有关 Windows 8 之前制造的光线传感器）。</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_DATA_TYPE_LIGHT_TEMPERATURE_KELVIN</p></td>
<td><p><strong>VT_R4</strong></p></td>
<td><p>开氏颜色温度。</p></td>
</tr>
</tbody>
</table>

 

**重要**  每个平台定义光线数据类型**PROPERTYKEY**基于一种常见**GUID**名为传感器\_数据\_类型\_光\_GUID。 由于它是保留的基值，请勿使用此**GUID**来定义你自己属性的密钥。

 

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
<td><p>Version</p></td>
<td><p>在 Windows 7 中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Sensors.h</td>
</tr>
</tbody>
</table>

 

 





