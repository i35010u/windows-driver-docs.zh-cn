---
title: ContentTypesSupported 元素
description: 所需的 ContentTypesSupported 元素包含描述在扫描仪支持的不同的文档内容类型的关键字的列表。
ms.assetid: f7ed2ba9-8cd9-486c-9bb0-3eb2c925450a
keywords:
- ContentTypesSupported 元素成像设备
topic_type:
- apiref
api_name:
- wscn ContentTypesSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 029bb0269a265bdb49c536d68eddb61bb1c93d0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525330"
---
# <a name="contenttypessupported-element"></a>ContentTypesSupported 元素


所需**ContentTypesSupported**元素包含描述在扫描仪支持的不同的文档内容类型的关键字的列表。

<a name="usage"></a>用法
-----

```xml
<wscn:ContentTypesSupported>
  child elements
</wscn:ContentTypesSupported>
```

<a name="attributes"></a>属性
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
<td><p><a href="contenttypevalue.md" data-raw-source="[&lt;strong&gt;ContentTypeValue&lt;/strong&gt;](contenttypevalue.md)"><strong>ContentTypeValue</strong></a></p></td>
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

每个[ **ContentTypeValue** ](contenttypevalue.md)中列出的元素**ContentTypesSupported**元素描述原始文档的主要特征。 客户端将选取的一种内容类型及其[ **ScanTicket** ](scanticket.md)启动一次扫描时此列表中。

## <a name="see-also"></a>另请参阅


[**ScanTicket**](scanticket.md)

 

 






