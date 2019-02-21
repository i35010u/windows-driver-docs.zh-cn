---
title: 严重性元素
description: 所需的严重性元素指定当前 DeviceCondition 或 ConditionHistoryEntry 元素的严重级别。
ms.assetid: 51c08a50-0c2b-40d9-883e-32460c2024ad
keywords:
- 严重性元素成像设备
topic_type:
- apiref
api_name:
- wscn Severity
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 151f43ce4cd552d1bed5d31a49fd29700d79451c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525847"
---
# <a name="severity-element"></a>严重性元素


所需**严重性**元素指定当前的严重性级别[ **DeviceCondition** ](devicecondition.md)或者[ **ConditionHistoryEntry** ](conditionhistoryentry.md)元素。

<a name="usage"></a>用法
-----

```xml
<wscn:Severity>
  text
</wscn:Severity>
```

<a name="attributes"></a>属性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 以下值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="Informational"></span><span id="informational"></span><span id="INFORMATIONAL"></span>信息性</p></td>
<td><p>这种情况是仅用于用户信息和图像采购流程没有明显影响。</p></td>
</tr>
<tr class="even">
<td><p><span id="Warning"></span><span id="warning"></span><span id="WARNING"></span>警告</p></td>
<td><p>这种情况不在当前正在影响处理，但该条件可能会变得严重如果它不应共同参加到。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Critical"></span><span id="critical"></span><span id="CRITICAL"></span>关键</p></td>
<td><p>设备无法继续处理，直到此问题得以解决。</p></td>
</tr>
</tbody>
</table>

 

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

WSD 扫描服务确定**严重性**分配给每个错误条件的级别。

您都可以扩展和子集的允许的值为此元素。

## <a name="see-also"></a>另请参阅


[**ConditionHistoryEntry**](conditionhistoryentry.md)

[**DeviceCondition**](devicecondition.md)

 

 






