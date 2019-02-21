---
title: PlatenColor 元素
description: 所需的 PlatenColor 元素包含描述处理辊功能的颜色的 ColorEntry 元素的列表。
ms.assetid: 97fd9926-e49d-4b4f-95aa-eb4142c353a3
keywords:
- PlatenColor 元素成像设备
topic_type:
- apiref
api_name:
- wscn PlatenColor
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e53812c0462a87a249d087387f762bbb90dcc1a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522803"
---
# <a name="platencolor-element"></a>PlatenColor 元素


所需**PlatenColor**元素包含一系列[ **ColorEntry** ](colorentry.md)描述处理辊功能的颜色的元素。

<a name="usage"></a>用法
-----

```xml
<wscn:PlatenColor>
  child elements
</wscn:PlatenColor>
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
<td><p><a href="platen.md" data-raw-source="[&lt;strong&gt;Platen&lt;/strong&gt;](platen.md)"><strong>辊</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**PlatenColor**元素包含确定色处理和获取平板辊支持的类型所需的信息。 描述每个像素所需的信息的量取决于特定于[ **ColorEntry** ](colorentry.md)关键字。 黑色和白色映像需要仅有一位每像素 (bpp)，而灰度和彩色图像需要更多的信息。 通过颜色空间并扫描设备的技术功能确定确切的信息量。

返回的扫描数据的另一个重要方面是测光获得的数据的解释。 需要为黑白色，其中 0 表示黑色和白色表示按 1 扫描设备返回的所有图像数据都。

## <a name="see-also"></a>另请参阅


[**ColorEntry**](colorentry.md)

[**辊**](platen.md)

 

 






