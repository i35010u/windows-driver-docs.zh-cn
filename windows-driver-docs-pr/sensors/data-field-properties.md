---
title: 数据字段属性
description: 本主题介绍用于仅数据字段的传感器属性。
ms.assetid: A7FA02AA-7B7B-45B4-A432-4B4ED69CB19C
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9797282dafe6f2db5b2a8408b963d783781ac16c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378575"
---
# <a name="data-field-properties"></a>数据字段属性


本主题介绍用于仅数据字段的传感器属性。

下表显示了传感器属性。 因为这些属性适用于任何数据字段，类型可以不同的数据字段根据这些属性要引用，请参阅[传感器数据字段](sensor-data-fields.md)主题，了解详细信息。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>属性键</th>
<th>在任务栏的搜索框中键入</th>
<th>访问 （R/O，R/W）</th>
<th>必需/可选</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PKEY_SensorDataField_Resolution</p></td>
<td><p>请参阅数据字段键入。</p></td>
<td><p>R/O</p></td>
<td><p>这取决于数据字段，需要此数据字段密钥请参阅有关的属性列表<a href="required-data-field-properties.md" data-raw-source="[Required data field properties](required-data-field-properties.md)">所需数据字段属性</a>主题。</p></td>
<td><p>数据字段的分辨率。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorDataField_RangeMinimum</p></td>
<td><p>请参阅数据字段键入。</p></td>
<td><p>R/O</p></td>
<td><p>这取决于数据字段，需要此数据字段密钥请参阅有关的属性列表<a href="required-data-field-properties.md" data-raw-source="[Required data field properties](required-data-field-properties.md)">所需数据字段属性</a>主题。</p></td>
<td><p>数据字段的最小值。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_SensorDataField_RangeMaximum</p></td>
<td><p>请参阅数据字段键入。</p></td>
<td><p>R/O</p></td>
<td><p>这取决于数据字段，需要此数据字段密钥请参阅有关的属性列表<a href="required-data-field-properties.md" data-raw-source="[Required data field properties](required-data-field-properties.md)">所需数据字段属性</a>主题。</p></td>
<td><p>数据字段的最大值。</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要求


**标头：** Sensorsdef.h

## <a name="related-topics"></a>相关主题


[所需的数据字段属性](required-data-field-properties.md)

[传感器数据字段](sensor-data-fields.md)

[传感器属性](sensor-properties2.md)

 

 






