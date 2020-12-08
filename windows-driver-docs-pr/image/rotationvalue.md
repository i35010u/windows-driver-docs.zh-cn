---
title: RotationValue 元素
description: 必需的 RotationValue 元素指定扫描设备支持的单个旋转值。
keywords:
- RotationValue 元素图像设备
topic_type:
- apiref
api_name:
- wscn RotationValue
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 919e639230387c55131c6f8108198f703b1abbc0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790613"
---
# <a name="rotationvalue-element"></a>RotationValue 元素


必需的 **RotationValue** 元素指定扫描设备支持的单个旋转值。

<a name="usage"></a>使用情况
-----

```xml
<wscn:RotationValue>
  text
</wscn:RotationValue>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 必须为0、90、180或270的数字值。

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
<td><p><a href="rotationssupported.md" data-raw-source="[&lt;strong&gt;RotationsSupported&lt;/strong&gt;](rotationssupported.md)"><strong>RotationsSupported</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**RotationValue** 元素指定扫描程序应为扫描文档的每个图像旋转的度数。 所有旋转都按顺时针方向应用。

所有 WSD 扫描服务都必须支持值0。 可以扩展和子集化此元素的允许值。

## <a name="see-also"></a>请参阅


[**RotationsSupported**](rotationssupported.md)

 

 






