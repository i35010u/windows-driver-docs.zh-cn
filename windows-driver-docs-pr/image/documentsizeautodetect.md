---
title: DocumentSizeAutoDetect 元素
description: 可选 DocumentSizeAutoDetect 元素指定扫描设备是否会自动确定原始扫描媒体的大小。
ms.assetid: 509e96d8-c99b-4d6e-9117-b9aed199da2c
keywords:
- DocumentSizeAutoDetect 元素成像设备
topic_type:
- apiref
api_name:
- wscn DocumentSizeAutoDetect
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d93d6da03e3a1904a1e905e63ce223ef3500ea99
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364510"
---
# <a name="documentsizeautodetect-element"></a>DocumentSizeAutoDetect 元素


可选**DocumentSizeAutoDetect**元素指定扫描设备是否会自动确定原始扫描媒体的大小。

<a name="usage"></a>用法
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

必需。 一个布尔值，必须为 0，为 false，1 或 true。**falsetrue**

## <a name="child-elements"></a>子元素


没有子元素。

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

如果指定的文本值为 1 或 **，则返回 true**，扫描设备将自动确定原始扫描媒体的大小。 如果**DocumentSizeAutoDetect**元素指定连同[ **ScanRegion** ](scanregion.md)元素中，扫描区域将被忽略，如果它在外部媒体大小检测到的设备。

## <a name="see-also"></a>请参阅


[**ScanRegion**](scanregion.md)

[**InputSize**](inputsize.md)

 

 






