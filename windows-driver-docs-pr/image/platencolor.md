---
title: PlatenColor 元素
description: 必需的 PlatenColor 元素包含一个 ColorEntry 元素列表，这些元素描述了影印的颜色处理功能。
keywords:
- PlatenColor 元素图像设备
topic_type:
- apiref
api_name:
- wscn PlatenColor
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec53acb4472fcb17a81859a9930af540f4b0577a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841081"
---
# <a name="platencolor-element"></a>PlatenColor 元素


必需的 **PlatenColor** 元素包含一个 [**ColorEntry**](colorentry.md) 元素列表，这些元素描述了影印的颜色处理功能。

<a name="usage"></a>使用情况
-----

```xml
<wscn:PlatenColor>
  child elements
</wscn:PlatenColor>
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
<td><p><a href="platen.md" data-raw-source="[&lt;strong&gt;Platen&lt;/strong&gt;](platen.md)"><strong>Platen</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**PlatenColor** 元素包含确定平板影印支持的颜色处理和购置类型所需的信息。 描述每个像素所需的信息量取决于特定的 [**ColorEntry**](colorentry.md) 关键字。 黑白图像需要每个像素 (bpp) ，而灰度和彩色图像需要更多的信息。 确切的信息量由扫描设备的颜色空间和技术功能决定。

返回的扫描数据的另一个重要方面是获取的数据的 photometric 解释。 扫描设备返回的所有图像数据都需要在白色显示黑色，其中黑色表示为0，白色表示为1。

## <a name="see-also"></a>请参阅


[**ColorEntry**](colorentry.md)

[**Platen**](platen.md)

 

 






