---
title: AutoExposureSupported 元素
description: 所需的 AutoExposureSupported 元素指定扫描设备是否支持自动调整各种的曝光度设置。
ms.assetid: 36ef003f-b049-4eb2-8fe3-53aa77db3065
keywords:
- AutoExposureSupported 元素成像设备
topic_type:
- apiref
api_name:
- wscn AutoExposureSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07406e332e01fbce4353a3cbe36f89dfe0e2cc9f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373363"
---
# <a name="autoexposuresupported-element"></a>AutoExposureSupported 元素


所需**AutoExposureSupported**元素指定扫描设备是否支持自动调整各种的曝光度设置。

<a name="usage"></a>用法
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

[**风险**](exposure.md)

如果扫描设备支持的各种自动调整[**暴露**](exposure.md)设置，WSD 扫描服务应返回 1 (**true**); 否则为它应返回 0 (**false**)。

不能扩展此元素允许的值。

## <a name="see-also"></a>请参阅


[**DeviceSettings**](devicesettings.md)

[**风险**](exposure.md)

 

 






