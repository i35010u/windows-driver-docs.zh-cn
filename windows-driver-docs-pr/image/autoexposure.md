---
title: AutoExposure 元素
description: 所需的 AutoExposure 元素指定 WSD 扫描服务应自动确定文档的曝光度设置。
ms.assetid: ccc2b246-cfa1-4d79-b968-7b4bbaad17ee
keywords:
- AutoExposure 元素成像设备
topic_type:
- apiref
api_name:
- wscn AutoExposure
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecfd7d6adfa3eea0602ad04e93ef464e973c1eb9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563722"
---
# <a name="autoexposure-element"></a>AutoExposure 元素


所需**AutoExposure**元素指定 WSD 扫描服务应自动确定文档的曝光度设置。

<a name="usage"></a>用法
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

必需。 一个布尔值，必须为 0，为 false，1 或 true。**falsetrue**

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
<td><p><a href="exposure.md" data-raw-source="[&lt;strong&gt;Exposure&lt;/strong&gt;](exposure.md)"><strong>风险</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

时的布尔值**AutoExposure**元素是 1 或**true**，扫描设备将使用图像处理技术来减少该文档的背景为白色。

当该值为 0 或**false**，设备应使用默认设置为每个的曝光度设置。

## <a name="see-also"></a>请参阅


[**风险**](exposure.md)

 

 






