---
title: 组件元素
description: 所需的组件元素标识当前 DeviceCondition 或 ConditionHistoryEntry 元素描述的组件。
ms.assetid: 1204d8c6-40a2-4b0b-bf86-a739ae96f54a
keywords:
- 组件元素成像设备
topic_type:
- apiref
api_name:
- wscn Component
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08304753deae656990fe1fb629758695a4152a42
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373213"
---
# <a name="component-element"></a>组件元素


所需**组件**元素标识的组件的当前[ **DeviceCondition** ](devicecondition.md)或者[ **ConditionHistoryEntry** ](conditionhistoryentry.md)元素描述。

<a name="usage"></a>用法
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
-   Film
-   MediaPath
-   Platen

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
<td><p><a href="conditionhistoryentry.md" data-raw-source="[&lt;strong&gt;ConditionHistoryEntry&lt;/strong&gt;](conditionhistoryentry.md)"><strong>ConditionHistoryEntry</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="devicecondition.md" data-raw-source="[&lt;strong&gt;DeviceCondition&lt;/strong&gt;](devicecondition.md)"><strong>DeviceCondition</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

您都可以扩展和子集的允许的值为此元素。

## <a name="see-also"></a>请参阅


[**ConditionHistoryEntry**](conditionhistoryentry.md)

[**DeviceCondition**](devicecondition.md)

 

 






