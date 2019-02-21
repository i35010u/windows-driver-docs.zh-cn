---
title: RotationsSupported 元素
description: 所需的 RotationsSupported 元素包含的扫描程序支持的旋转扫描的文档的每个图像的旋转值的列表。
ms.assetid: da72cc1e-40e8-46a1-8215-0a20a52a0e19
keywords:
- RotationsSupported 元素成像设备
topic_type:
- apiref
api_name:
- wscn RotationsSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f5b0acfc05ace3e31b055f896f0c0461122350c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522076"
---
# <a name="rotationssupported-element"></a>RotationsSupported 元素


所需**RotationsSupported**元素包含的扫描程序支持的旋转扫描的文档的每个图像的旋转值的列表。

<a name="usage"></a>用法
-----

```xml
<wscn:RotationsSupported>
  child elements
</wscn:RotationsSupported>
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

WSD 扫描服务必须在数据采集后将所有旋转值都应用于扫描数据。 必须按顺时针方向应用所有的旋转。

## <a name="see-also"></a>另请参阅


[**DeviceSettings**](devicesettings.md)

[**RotationValue**](rotationvalue.md)

 

 






