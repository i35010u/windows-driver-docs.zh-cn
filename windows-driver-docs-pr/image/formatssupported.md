---
title: FormatsSupported 元素
description: 必需的 FormatsSupported 元素是一个元素集合，其中列出了扫描程序支持的文档文件格式。
ms.assetid: bb4b6630-f865-4ec7-b7d1-8be424eea345
keywords:
- FormatsSupported 元素图像设备
topic_type:
- apiref
api_name:
- wscn FormatsSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bad45d7596eaa74b301cac0ee71f9cde250329a
ms.sourcegitcommit: dff3834724bd5204c4a47204540fe8125dd37b20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2019
ms.locfileid: "70750044"
---
# <a name="formatssupported-element"></a>FormatsSupported 元素


必需的**FormatsSupported**元素是一个元素集合，其中列出了扫描程序支持的文档文件格式。

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

每个[**FormatValue**](formatvalue.md)元素指定一种文件格式，用于描述文件类型和压缩类型。

## <a name="see-also"></a>请参阅


[**DeviceSettings**](devicesettings.md)

[**FormatValue**](formatvalue.md)

 

 






