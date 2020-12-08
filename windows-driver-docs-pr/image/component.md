---
title: Component 元素
description: 必需的组件元素标识当前 DeviceCondition 或 ConditionHistoryEntry 元素描述的组件。
keywords:
- 组件元素图像处理设备
topic_type:
- apiref
api_name:
- wscn Component
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ca2893c6b74ca1f3ef06dce290420ffe2fc1d54
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783921"
---
# <a name="component-element"></a>Component 元素


必需的 **组件** 元素标识当前 [**DeviceCondition**](devicecondition.md) 或 [**ConditionHistoryEntry**](conditionhistoryentry.md) 元素描述的组件。

<a name="usage"></a>使用情况
-----

```xml
<wscn:Component>
  text
</wscn:Component>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 以下值之一：

-   ADF
-   胶片
-   MediaPath
-   Platen

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
<td><p><a href="conditionhistoryentry.md" data-raw-source="[&lt;strong&gt;ConditionHistoryEntry&lt;/strong&gt;](conditionhistoryentry.md)"><strong>ConditionHistoryEntry</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="devicecondition.md" data-raw-source="[&lt;strong&gt;DeviceCondition&lt;/strong&gt;](devicecondition.md)"><strong>DeviceCondition</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

可以扩展和子集化此元素的允许值。

## <a name="see-also"></a>请参阅


[**ConditionHistoryEntry**](conditionhistoryentry.md)

[**DeviceCondition**](devicecondition.md)

 

 






