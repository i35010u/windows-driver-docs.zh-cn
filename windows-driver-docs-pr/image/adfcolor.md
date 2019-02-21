---
title: ADFColor 元素
description: 所需的 ADFColor 元素包含处理自动文档送纸器 (ADF) 的前端或后端支持的功能的颜色的列表。
ms.assetid: b336c72e-9095-456e-8cb4-4018e72e29fa
keywords:
- ADFColor 元素成像设备
topic_type:
- apiref
api_name:
- wscn ADFColor
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c583d30d4b3a84d2afeea16676dd26e32073da8a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541069"
---
# <a name="adfcolor-element"></a>ADFColor 元素


所需**ADFColor**元素包含处理自动文档送纸器 (ADF) 的前端或后端支持的功能的颜色的列表。

<a name="usage"></a>用法
-----

```xml
<wscn:ADFColor>
  child elements
</wscn:ADFColor>
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
<td><p><a href="colorentry.md" data-raw-source="[&lt;strong&gt;ColorEntry&lt;/strong&gt;](colorentry.md)"><strong>ColorEntry</strong></a></p></td>
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

**ADFColor**元素包含确定色处理和获取扫描程序的 ADF 支持的类型所需的信息。 如果父元素是[ **ADFFront**](adffront.md)，指定的颜色信息适用于 ADF 的正面; 否则，为父元素[ **ADFBack**](adfback.md)和颜色信息适用于 ADF 的后端。

描述每个像素所需的信息的量取决于特定于[ **ColorEntry** ](colorentry.md)关键字。 黑色和白色映像需要仅有一位每像素 (bpp)，而灰度和彩色图像需要更多的信息。 通过颜色空间并扫描设备的技术功能确定确切的信息量。

返回的扫描数据的另一个重要方面是测光获得的数据的解释。 需要为黑白色，其中 0 表示黑色和白色表示按 1 扫描设备返回的所有图像数据都。

## <a name="see-also"></a>另请参阅


[**ADFBack**](adfback.md)

[**ADFFront**](adffront.md)

[**ColorEntry**](colorentry.md)

 

 






