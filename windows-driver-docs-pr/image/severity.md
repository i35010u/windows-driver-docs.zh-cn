---
title: 严重性元素
description: Required 严重性元素指定当前 DeviceCondition 或 ConditionHistoryEntry 元素的严重性级别。
keywords:
- 严重性元素图像处理设备
topic_type:
- apiref
api_name:
- wscn Severity
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5401e909d4a91023e0ba7357338c12561fa20065
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785173"
---
# <a name="severity-element"></a>严重性元素


Required **严重性** 元素指定当前 [**DeviceCondition**](devicecondition.md) 或 [**ConditionHistoryEntry**](conditionhistoryentry.md) 元素的严重性级别。

<a name="usage"></a>使用情况
-----

```xml
<wscn:Severity>
  text
</wscn:Severity>
```

<a name="attributes"></a>特性
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
<td><p><span id="Informational"></span><span id="informational"></span><span id="INFORMATIONAL"></span>条</p></td>
<td><p>此条件仅适用于用户信息，并且对映像采集过程没有明显影响。</p></td>
</tr>
<tr class="even">
<td><p><span id="Warning"></span><span id="warning"></span><span id="WARNING"></span>出现</p></td>
<td><p>这种情况目前不会影响处理，但是如果不参与，则条件可能会变得至关重要。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Critical"></span><span id="critical"></span><span id="CRITICAL"></span>来说</p></td>
<td><p>在解决此问题之前，设备无法继续处理。</p></td>
</tr>
</tbody>
</table>

 

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

WSD 扫描服务确定分配给每个错误条件的 **严重性** 级别。

可以扩展和子集化此元素的允许值。

## <a name="see-also"></a>请参阅


[**ConditionHistoryEntry**](conditionhistoryentry.md)

[**DeviceCondition**](devicecondition.md)

 

 






