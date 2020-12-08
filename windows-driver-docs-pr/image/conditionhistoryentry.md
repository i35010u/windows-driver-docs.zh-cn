---
title: ConditionHistoryEntry 元素
description: 必需的 ConditionHistoryEntry 元素提供有关扫描仪上过去的某个条件的详细信息。
keywords:
- ConditionHistoryEntry 元素图像设备
topic_type:
- apiref
api_name:
- wscn ConditionHistoryEntry wscn Id "..."
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75d42643ddc49e46af2d649b0e9da67b063b4a6c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830493"
---
# <a name="conditionhistoryentry-element"></a>ConditionHistoryEntry 元素


必需的 **ConditionHistoryEntry** 元素提供有关扫描仪上过去的某个条件的详细信息。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ConditionHistoryEntry wscn:Id="..."
  Id = "xs:string">
  child elements
</wscn:ConditionHistoryEntry wscn:Id="...">
```

<a name="attributes"></a>特性
----------

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>类型</th>
<th>必须</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>识别</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>必需。 1到2147483648之间的一个整数。</p></td>
</tr>
</tbody>
</table>

## <a name="child-elements"></a>子元素


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
<td><p><a href="cleartime.md" data-raw-source="[&lt;strong&gt;ClearTime&lt;/strong&gt;](cleartime.md)"><strong>ClearTime</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="component.md" data-raw-source="[&lt;strong&gt;Component&lt;/strong&gt;](component.md)"><strong>组件</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="name-element-for-devicecondition-and-conditionhistoryentry.md" data-raw-source="[&lt;strong&gt;Name forParents DeviceCondition and ConditionHistoryEntry&lt;/strong&gt;](name-element-for-devicecondition-and-conditionhistoryentry.md)"><strong>Name forParents DeviceCondition and ConditionHistoryEntry</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="severity.md" data-raw-source="[&lt;strong&gt;Severity&lt;/strong&gt;](severity.md)"><strong>严重性</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="time.md" data-raw-source="[&lt;strong&gt;Time&lt;/strong&gt;](time.md)"><strong>时间</strong></a></p></td>
</tr>
</tbody>
</table>

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
<td><p><a href="conditionhistory.md" data-raw-source="[&lt;strong&gt;ConditionHistory&lt;/strong&gt;](conditionhistory.md)"><strong>ConditionHistory</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

WSD 扫描服务指定此 **ConditionHistoryEntry** 元素的 **Id** 属性中的唯一标识符。 客户端可以使用 **Id** 和 [**时间**](time.md) 元素的值来确定错误条件是新的还是已消失。 WSD 扫描服务不得尽可能长地重复使用标识符。 此延迟可确保客户端能够准确地跟踪单个 **ConditionHistoryEntry** 元素。

不能扩展 **Id** 的允许值。

## <a name="see-also"></a>请参阅


[**ClearTime**](cleartime.md)

[**组件**](component.md)

[**ConditionHistory**](conditionhistory.md)

[**DeviceCondition**](devicecondition.md)

[**Name forParents DeviceCondition and ConditionHistoryEntry**](name-element-for-devicecondition-and-conditionhistoryentry.md)

[**严重性**](severity.md)

[**时间**](time.md)

 

 






