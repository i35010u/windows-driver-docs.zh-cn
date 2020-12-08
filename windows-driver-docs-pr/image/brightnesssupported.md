---
title: BrightnessSupported 元素
description: 必需的 BrightnessSupported 元素指定扫描设备是否支持用户控制扫描亮度设置。
keywords:
- BrightnessSupported 元素图像设备
topic_type:
- apiref
api_name:
- wscn BrightnessSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: db3e677c9332ddfbb74ea64afee67a33c923abde
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816239"
---
# <a name="brightnesssupported-element"></a>BrightnessSupported 元素


必需的 **BrightnessSupported** 元素指定扫描设备是否支持用户控制扫描亮度设置。

<a name="usage"></a>使用情况
-----

```xml
<wscn:BrightnessSupported>
  text
</wscn:BrightnessSupported>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 必须为0、1、false 或 true 的布尔值。**falsetrue**

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
<td><p><a href="devicesettings.md" data-raw-source="[&lt;strong&gt;DeviceSettings&lt;/strong&gt;](devicesettings.md)"><strong>DeviceSettings</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

如果扫描设备允许用户控制扫描亮度设置，则 WSD 扫描服务应返回 1 (**true**) ;否则，它应返回 0 (**false**) 。

不能扩展此元素的允许值。

## <a name="see-also"></a>请参阅


[**DeviceSettings**](devicesettings.md)

 

 






