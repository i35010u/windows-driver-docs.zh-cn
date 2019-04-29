---
title: DocumentSizeAutoDetectSupported 元素
description: 所需的 DocumentSizeAutoDetectSupported 元素指示扫描设备是否可以检测到的原始媒体的大小。
ms.assetid: 38baea3d-85bf-44e1-86bf-349d17981efa
keywords:
- DocumentSizeAutoDetectSupported 元素成像设备
topic_type:
- apiref
api_name:
- wscn DocumentSizeAutoDetectSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec59f6f1847f0ce3653cc129d36956aeb1492070
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364509"
---
# <a name="documentsizeautodetectsupported-element"></a>DocumentSizeAutoDetectSupported 元素


所需**DocumentSizeAutoDetectSupported**元素指示扫描设备是否可以检测到的原始媒体的大小。

<a name="usage"></a>用法
-----

```xml
<wscn:DocumentSizeAutoDetectSupported>
  text
</wscn:DocumentSizeAutoDetectSupported>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 一个布尔值，必须为 0，1，为 false，或，则返回 true。**falsetrue**

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
<td><p><a href="devicesettings.md" data-raw-source="[&lt;strong&gt;DeviceSettings&lt;/strong&gt;](devicesettings.md)"><strong>DeviceSettings</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

如果扫描设备可以检测到的原始媒体的大小，WSD 扫描服务应返回 1 (**，则返回 true**); 否则为它应返回 0 (**false**)。

不能扩展此元素允许的值。

## <a name="see-also"></a>请参阅


[**DeviceSettings**](devicesettings.md)

 

 






