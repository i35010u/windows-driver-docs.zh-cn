---
title: ADFSupportsDuplex 元素
description: 所需的 ADFSupportsDuplex 元素指定附加的自动文档送纸器 (ADF) 是否支持扫描介质的两面。
ms.assetid: 0e85243a-5b15-4b51-9608-c8036639c735
keywords:
- ADFSupportsDuplex 元素成像设备
topic_type:
- apiref
api_name:
- wscn ADFSupportsDuplex
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85e2fc11b83db7de19411f95922f59037bf37cd2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525928"
---
# <a name="adfsupportsduplex-element"></a>ADFSupportsDuplex 元素


所需**ADFSupportsDuplex**元素指定附加的自动文档送纸器 (ADF) 是否支持扫描介质的两面。

<a name="usage"></a>用法
-----

```xml
<wscn:ADFSupportsDuplex>
  text
</wscn:ADFSupportsDuplex>
```

<a name="attributes"></a>属性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 一个布尔值，必须为 0，1，为 false，或，则返回 true。**false**或 **，则返回 true**

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
<td><p><a href="adf.md" data-raw-source="[&lt;strong&gt;ADF&lt;/strong&gt;](adf.md)"><strong>ADF</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

如果扫描设备已支持双工扫描 ADF，WSD 扫描服务应返回 1 (**，则返回 true**); 否则为它应返回 0 (**false**)。

不能扩展此元素允许的值。

## <a name="see-also"></a>另请参阅


[**ADF**](adf.md)

 

 






