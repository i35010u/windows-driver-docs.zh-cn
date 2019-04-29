---
title: RotationValue 元素
description: 所需的 RotationValue 元素指定扫描设备支持的单个旋转值。
ms.assetid: 89b8527a-309a-4344-bf6e-3155bb056acf
keywords:
- RotationValue 元素成像设备
topic_type:
- apiref
api_name:
- wscn RotationValue
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b3a4fea4c1227e64da3185174f91789e0642e03
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381579"
---
# <a name="rotationvalue-element"></a>RotationValue 元素


所需**RotationValue**元素指定扫描设备支持的单个旋转值。

<a name="usage"></a>用法
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

必需。 一个数字值，该值必须是 0、 90、 180 或 270。

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
<td><p><a href="rotationssupported.md" data-raw-source="[&lt;strong&gt;RotationsSupported&lt;/strong&gt;](rotationssupported.md)"><strong>RotationsSupported</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**RotationValue**元素指定的扫描程序应旋转扫描的文档的每个图像的度数。 按顺时针方向应用所有的旋转。

所有 WSD 扫描服务必须都支持的值为 0。 您都可以扩展和子集的允许的值为此元素。

## <a name="see-also"></a>请参阅


[**RotationsSupported**](rotationssupported.md)

 

 






