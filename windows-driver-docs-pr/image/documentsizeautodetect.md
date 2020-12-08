---
title: DocumentSizeAutoDetect 元素
description: 可选的 DocumentSizeAutoDetect 元素指定扫描设备是否自动确定原始扫描介质的大小。
keywords:
- DocumentSizeAutoDetect 元素图像设备
topic_type:
- apiref
api_name:
- wscn DocumentSizeAutoDetect
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d89aaf8468eab4acd59890b146b53e028c34e96
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789883"
---
# <a name="documentsizeautodetect-element"></a>DocumentSizeAutoDetect 元素


可选的 **DocumentSizeAutoDetect** 元素指定扫描设备是否自动确定原始扫描介质的大小。

<a name="usage"></a>使用情况
-----

```xml
<wscn:DocumentSizeAutoDetect>
  text
</wscn:DocumentSizeAutoDetect>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 必须为0、false、1或 true 的布尔值。**falsetrue**

## <a name="child-elements"></a>子元素


没有任何子元素。

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
<td><p><a href="inputsize.md" data-raw-source="[&lt;strong&gt;InputSize&lt;/strong&gt;](inputsize.md)"><strong>InputSize</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

如果指定的文本值为1或 **true**，则扫描设备将自动确定原始扫描媒体的大小。 如果 **DocumentSizeAutoDetect** 元素与 [**ScanRegion**](scanregion.md) 元素一起指定，则如果扫描区域超出设备检测到的介质大小，则会将其忽略。

## <a name="see-also"></a>请参阅


[**ScanRegion**](scanregion.md)

[**InputSize**](inputsize.md)

 

 






