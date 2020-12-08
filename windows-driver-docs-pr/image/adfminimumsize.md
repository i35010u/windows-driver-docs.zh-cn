---
title: ADFMinimumSize 元素
description: 必需的 ADFMinimumSize 元素指定最终用户可在自动文档送纸器的前端或背面扫描 (ADF) 的最小原始大小。
keywords:
- ADFMinimumSize 元素图像设备
topic_type:
- apiref
api_name:
- wscn ADFMinimumSize
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 188fdb3dd75b5717d42ba94cbd2a8da4db9b3088
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837759"
---
# <a name="adfminimumsize-element"></a>ADFMinimumSize 元素


必需的 **ADFMinimumSize** 元素指定最终用户可在自动文档送纸器的前端或背面扫描 (ADF) 的最小原始大小。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ADFMinimumSize>
  child elements
</wscn:ADFMinimumSize>
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

[**Width**](width.md)子元素指定 ADF 在快速扫描方向上支持的最小介质大小。 [**Height**](height.md)子元素指定 ADF 在慢速扫描方向上所支持的最小介质大小。

如果 **ADFMinimumSize** 元素的父元素为 [**ADFFront**](adffront.md)，则指定的大小适用于 ADF 的前端;否则，父元素为 [**ADFBack**](adfback.md) ，其大小适用于 ADF 的背面。

所有介质尺寸都以一分之几个 (1/1000) 英寸度量。 **宽度** 和 **高度** 的可能值范围是从1到2147483648。

## <a name="see-also"></a>请参阅


[**ADFBack**](adfback.md)

[**ADFFront**](adffront.md)

[**高度**](height.md)

[**宽度**](width.md)

 

 






