---
title: ADFSupportsDuplex 元素
description: 必需的 ADFSupportsDuplex 元素指定附加的自动文档送纸器 (ADF) 是否支持扫描介质的两侧。
keywords:
- ADFSupportsDuplex 元素图像设备
topic_type:
- apiref
api_name:
- wscn ADFSupportsDuplex
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 954d4da42de44b6f8d2dd92233fde49226e58569
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819627"
---
# <a name="adfsupportsduplex-element"></a>ADFSupportsDuplex 元素


必需的 **ADFSupportsDuplex** 元素指定附加的自动文档送纸器 (ADF) 是否支持扫描介质的两侧。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ADFSupportsDuplex>
  text
</wscn:ADFSupportsDuplex>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 必须为0、1、false 或 true 的布尔值。**false** 或 **true**

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
<td><p><a href="adf.md" data-raw-source="[&lt;strong&gt;ADF&lt;/strong&gt;](adf.md)"><strong>ADF</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

如果扫描设备的 ADF 支持双工扫描，则 WSD 扫描服务应返回 1 (**true**) ;否则，它应返回 0 (**false**) 。

不能扩展此元素的允许值。

## <a name="see-also"></a>请参阅


[**ADF**](adf.md)

 

 






