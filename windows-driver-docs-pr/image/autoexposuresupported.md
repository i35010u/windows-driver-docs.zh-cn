---
title: AutoExposureSupported 元素
description: 必需的 AutoExposureSupported 元素指定扫描设备是否支持自动调整各种曝光度设置。
keywords:
- AutoExposureSupported 元素图像设备
topic_type:
- apiref
api_name:
- wscn AutoExposureSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30da2fbbe926b4308cbc458465a283e24476d035
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828719"
---
# <a name="autoexposuresupported-element"></a>AutoExposureSupported 元素


必需的 **AutoExposureSupported** 元素指定扫描设备是否支持自动调整各种曝光度设置。

<a name="usage"></a>使用情况
-----

```xml
<wscn:AutoExposureSupported>
  text
</wscn:AutoExposureSupported>
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

[**隐患**](exposure.md)

如果扫描设备支持自动调整各种 [**曝光度**](exposure.md) 设置，则 WSD 扫描服务应返回 1 (**true**) ;否则，它应返回 0 (**false**) 。

不能扩展此元素的允许值。

## <a name="see-also"></a>请参阅


[**DeviceSettings**](devicesettings.md)

[**隐患**](exposure.md)

 

 






