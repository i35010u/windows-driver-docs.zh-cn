---
title: ContentTypesSupported 元素
description: 必需的 ContentTypesSupported 元素包含关键字列表，这些关键字描述了扫描程序支持的不同文档内容类型。
keywords:
- ContentTypesSupported 元素图像设备
topic_type:
- apiref
api_name:
- wscn ContentTypesSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6befd33cb39bc39c6bf42a41c0fee9a39fb77b73
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826847"
---
# <a name="contenttypessupported-element"></a>ContentTypesSupported 元素


必需的 **ContentTypesSupported** 元素包含关键字列表，这些关键字描述了扫描程序支持的不同文档内容类型。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ContentTypesSupported>
  child elements
</wscn:ContentTypesSupported>
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

**ContentTypesSupported** 元素中列出的每个 [**ContentTypeValue**](contenttypevalue.md)元素描述原始文档的主要特征。 启动扫描时，客户端将从此列表中为其 [**ScanTicket**](scanticket.md) 选择一个内容类型。

## <a name="see-also"></a>请参阅


[**ScanTicket**](scanticket.md)

 

 






