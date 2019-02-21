---
title: BrightnessSupported 元素
description: 所需的 BrightnessSupported 元素指定扫描设备是否支持扫描亮度设置的用户控件。
ms.assetid: aa0eb627-694f-45a1-a923-07fc04b0612b
keywords:
- BrightnessSupported 元素成像设备
topic_type:
- apiref
api_name:
- wscn BrightnessSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 100c4d35c4eb69b1ecb30014d309ef306e24bb36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525322"
---
# <a name="brightnesssupported-element"></a>BrightnessSupported 元素


所需**BrightnessSupported**元素指定扫描设备是否支持扫描亮度设置的用户控件。

<a name="usage"></a>用法
-----

```xml
<wscn:BrightnessSupported>
  text
</wscn:BrightnessSupported>
```

<a name="attributes"></a>属性
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

如果扫描设备允许用户控制的扫描亮度设置，WSD 扫描服务应返回 1 (**，则返回 true**); 否则为它应返回 0 (**false**)。

不能扩展此元素允许的值。

## <a name="see-also"></a>另请参阅


[**DeviceSettings**](devicesettings.md)

 

 






