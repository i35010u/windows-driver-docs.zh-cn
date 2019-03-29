---
title: ContrastSupported 元素
description: 所需的 ContrastSupported 元素指定扫描设备是否支持扫描的对比度设置的用户控件。
ms.assetid: 9b865f9f-b5f6-4bb3-9f24-3df896845e96
keywords:
- ContrastSupported 元素成像设备
topic_type:
- apiref
api_name:
- wscn ContrastSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7296dc177769fd80357de7a705ab2ed587c64375
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567016"
---
# <a name="contrastsupported-element"></a>ContrastSupported 元素


所需**ContrastSupported**元素指定扫描设备是否支持扫描的对比度设置的用户控件。

<a name="usage"></a>用法
-----

```xml
<wscn:ContrastSupported>
  text
</wscn:ContrastSupported>
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

如果扫描设备允许用户控制的扫描的对比度设置，WSD 扫描服务应返回 1 (**，则返回 true**); 否则为它应返回 0 (**false**)。

不能扩展此元素允许的值。

## <a name="see-also"></a>请参阅


[**DeviceSettings**](devicesettings.md)

 

 






