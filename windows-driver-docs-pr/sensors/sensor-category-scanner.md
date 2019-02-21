---
title: 传感器\_类别\_扫描程序
description: 传感器\_类别\_扫描程序类别包含提供通过扫描来获取的信息的传感器。
ms.assetid: ba7a44d0-1d89-4a6c-b046-c7cd02c457b3
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
ms.openlocfilehash: eb25e6437e2c5408b77880a108d13f29699cb48c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547662"
---
# <a name="sensorcategoryscanner"></a>传感器\_类别\_扫描程序


传感器\_类别\_扫描程序类别包含提供通过扫描来获取的信息的传感器。

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
<td><p>SENSOR_TYPE_BARCODE_SCANNER</p></td>
<td><p>使用光学扫描读取条形码的传感器。</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_TYPE_RFID_SCANNER</p></td>
<td><p>无线电频率扫描传感器 ID。</p></td>
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
<td><p>SENSOR_DATA_TYPE_RFID_TAG_40_BIT</p></td>
<td><p><strong>VT_UI8</strong></p></td>
<td><p>40 位射频 ID 标记值。</p></td>
</tr>
</tbody>
</table>

 

**重要**  每个平台定义的扫描程序的数据类型**PROPERTYKEY**基于一种常见**GUID**名为传感器\_数据\_类型\_扫描程序\_GUID。 由于它是保留的基值，请勿使用此**GUID**来定义你自己属性的密钥。

 

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

 

 





