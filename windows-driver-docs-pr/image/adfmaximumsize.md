---
title: ADFMaximumSize 元素
description: 必需的 ADFMaximumSize 元素指定最终用户可在自动文档送纸器的前端或背面)  (ADF 的最大大小的文档。
keywords:
- ADFMaximumSize 元素图像设备
topic_type:
- apiref
api_name:
- wscn ADFMaximumSize
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6da3f5233539f5e1f40e3ea771ff5bf273f548c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837763"
---
# <a name="adfmaximumsize-element"></a>ADFMaximumSize 元素


必需的 **ADFMaximumSize** 元素指定最终用户可在自动文档送纸器的前端或背面)  (ADF 的最大大小的文档。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ADFMaximumSize>
  child elements
</wscn:ADFMaximumSize>
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
<td><p><a href="height.md" data-raw-source="[&lt;strong&gt;Height&lt;/strong&gt;](height.md)"><strong>高度</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="width.md" data-raw-source="[&lt;strong&gt;Width&lt;/strong&gt;](width.md)"><strong>宽度</strong></a></p></td>
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
<td><p><a href="adfback.md" data-raw-source="[&lt;strong&gt;ADFBack&lt;/strong&gt;](adfback.md)"><strong>ADFBack</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="adffront.md" data-raw-source="[&lt;strong&gt;ADFFront&lt;/strong&gt;](adffront.md)"><strong>ADFFront</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

[**Width**](width.md)子元素指定 ADF 在快速扫描方向上支持的最大介质大小。 [**Height**](height.md)子元素指定 ADF 在慢速扫描方向上所支持的最大介质大小。

如果 **ADFMaximumSize** 元素的父元素为 [**ADFFront**](adffront.md)，则指定的最大大小适用于 ADF 的前端;否则，父元素为 [**ADFBack**](adfback.md) ，最大大小适用于 ADF 的背面。

所有介质尺寸都按1分之 (1/1000) 英寸度量。 **宽度** 和 **高度** 的可能值范围是从1到2147483648。

## <a name="see-also"></a>请参阅


[**ADFBack**](adfback.md)

[**ADFFront**](adffront.md)

[**高度**](height.md)

[**宽度**](width.md)

 

 






