---
title: AutoExposure 元素
description: 必需的 AutoExposure 元素指定 WSD 扫描服务应自动确定文档的曝光设置。
keywords:
- AutoExposure 元素图像设备
topic_type:
- apiref
api_name:
- wscn AutoExposure
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9960e5652606502af6052ab165518ad9532af2fb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828723"
---
# <a name="autoexposure-element"></a>AutoExposure 元素


必需的 **AutoExposure** 元素指定 WSD 扫描服务应自动确定文档的曝光设置。

<a name="usage"></a>使用情况
-----

```xml
<wscn:AutoExposure>
  text
</wscn:AutoExposure>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 必须为0、false、1或 true 的布尔值。**falsetrue**

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
<td><p><a href="exposure.md" data-raw-source="[&lt;strong&gt;Exposure&lt;/strong&gt;](exposure.md)"><strong>隐患</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

当 **AutoExposure** 元素的布尔值为1或 **true** 时，扫描设备将使用图像处理技术将文档的背景减少到白色。

如果该值为0或 **false**，设备应使用每个曝光度设置的默认设置。

## <a name="see-also"></a>请参阅


[**隐患**](exposure.md)

 

 






