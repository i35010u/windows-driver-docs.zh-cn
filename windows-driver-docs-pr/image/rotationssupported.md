---
title: RotationsSupported 元素
description: 必需的 RotationsSupported 元素包含扫描仪支持的旋转值的列表，这些旋转值用于旋转扫描文档的每个图像。
keywords:
- RotationsSupported 元素图像设备
topic_type:
- apiref
api_name:
- wscn RotationsSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: efffd65a70f95c994c4101e96efbcdda10f15627
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790615"
---
# <a name="rotationssupported-element"></a>RotationsSupported 元素


必需的 **RotationsSupported** 元素包含扫描仪支持的旋转值的列表，这些旋转值用于旋转扫描文档的每个图像。

<a name="usage"></a>使用情况
-----

```xml
<wscn:RotationsSupported>
  child elements
</wscn:RotationsSupported>
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
<td><p><a href="rotationvalue.md" data-raw-source="[&lt;strong&gt;RotationValue&lt;/strong&gt;](rotationvalue.md)"><strong>RotationValue</strong></a></p></td>
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
<td><p><a href="devicesettings.md" data-raw-source="[&lt;strong&gt;DeviceSettings&lt;/strong&gt;](devicesettings.md)"><strong>DeviceSettings</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

在数据采集后，WSD 扫描服务必须将所有旋转值应用于扫描数据。 必须以顺时针方向应用所有旋转。

## <a name="see-also"></a>请参阅


[**DeviceSettings**](devicesettings.md)

[**RotationValue**](rotationvalue.md)

 

 






