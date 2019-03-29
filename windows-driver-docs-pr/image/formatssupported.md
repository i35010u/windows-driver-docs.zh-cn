---
title: FormatsSupported 元素
description: 所需的 FormatsSupported 元素是列出在扫描仪支持的文档文件格式的元素的集合。
ms.assetid: bb4b6630-f865-4ec7-b7d1-8be424eea345
keywords:
- FormatsSupported 元素成像设备
topic_type:
- apiref
api_name:
- wscn FormatsSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bad45d7596eaa74b301cac0ee71f9cde250329a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568356"
---
# <a name="formatssupported-element"></a>FormatsSupported 元素


所需**FormatsSupported**元素是列出在扫描仪支持的文档文件格式的元素的集合。

<a name="usage"></a>用法
-----

```xml
<wscn:FormatsSupported>
  child elements
</wscn:FormatsSupported>
```

<a name="attributes"></a>特性
----------

没有特性。

## <a name="child-elements"></a>子元素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="formatvalue.md" data-raw-source="[&lt;strong&gt;FormatValue&lt;/strong&gt;](formatvalue.md)"><strong>FormatValue</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="devicesettings.md" data-raw-source="[&lt;strong&gt;DeviceSettings&lt;/strong&gt;](devicesettings.md)"><strong>DeviceSettings</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

每个[ **FormatValue** ](formatvalue.md)元素指定描述的文件类型和压缩类型的文件格式。

## <a name="see-also"></a>请参阅


[**DeviceSettings**](devicesettings.md)

[**FormatValue**](formatvalue.md)

 

 






