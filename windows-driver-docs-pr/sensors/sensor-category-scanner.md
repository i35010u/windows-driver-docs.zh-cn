---
title: 传感器 \_ 类别 \_ 扫描器
description: 传感器 \_ 类别 \_ 扫描器类别包含的传感器提供通过扫描获得的信息。
keywords:
- SENSOR_CATEGORY_SCANNER 传感器设备
topic_type:
- apiref
api_name:
- SENSOR_CATEGORY_SCANNER
api_location:
- Sensors.h
api_type:
- HeaderDef
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: a8dd3acf33059c094358413da4fb8dbd2cce0963
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812191"
---
# <a name="sensor_category_scanner"></a>传感器 \_ 类别 \_ 扫描器


传感器 \_ 类别 \_ 扫描器类别包含的传感器提供通过扫描获得的信息。

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
<td><p>SENSOR_TYPE_BARCODE_SCANNER</p></td>
<td><p>使用光学扫描读取条码的传感器。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_RFID_SCANNER</p></td>
<td><p>射频 ID 扫描传感器。</p></td>
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
<td><p>SENSOR_DATA_TYPE_RFID_TAG_40_BIT</p></td>
<td><p>VT_UI8</p></td>
<td><p>40位射频 ID 标记值。</p></td>
</tr>
</tbody>
</table>

 

**重要提示**  每个平台定义的扫描程序数据类型 **PROPERTYKEY** 均基于一个名为 "传感器 **GUID** \_ 数据 \_ 类型 \_ 扫描器 \_ guid" 的通用 GUID。 由于这是保留的基值，请不要使用此 **GUID** 来定义自己的属性键。

 

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

 

 





