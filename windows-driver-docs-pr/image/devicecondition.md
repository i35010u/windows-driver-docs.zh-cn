---
title: DeviceCondition 元素
description: 可选 DeviceCondition 元素提供有关扫描程序的当前处于活动状态的条件之一的详细信息。
ms.assetid: 5e68462f-afa9-40d4-843a-7d15fb7c98e3
keywords:
- DeviceCondition 元素成像设备
topic_type:
- apiref
api_name:
- wscn DeviceCondition wscn Id "..."
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92558cbe7ec9c321fe27a6b19895dbccaf58db86
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556008"
---
# <a name="devicecondition-element"></a>DeviceCondition 元素


可选**DeviceCondition**元素提供有关扫描程序的当前处于活动状态的条件之一的详细信息。

<a name="usage"></a>用法
-----

```xml
<wscn:DeviceCondition wscn:Id="..."
  Id = "xs:string">
  child elements
</wscn:DeviceCondition wscn:Id="...">
```

<a name="attributes"></a>属性
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
<th>在任务栏的搜索框中键入</th>
<th>必需</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>Id</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>必需。 一个从 1 到 2147483648 整数。</p></td>
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
<td><p><a href="component.md" data-raw-source="[&lt;strong&gt;Component&lt;/strong&gt;](component.md)"><strong>组件</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="name-element-for-devicecondition-and-conditionhistoryentry.md" data-raw-source="[&lt;strong&gt;Name Elementfor DeviceCondition and ConditionHistoryEntry&lt;/strong&gt;](name-element-for-devicecondition-and-conditionhistoryentry.md)"><strong>名称 Elementfor DeviceCondition 和 ConditionHistoryEntry</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="severity.md" data-raw-source="[&lt;strong&gt;Severity&lt;/strong&gt;](severity.md)"><strong>严重级别</strong></a></p></td>
</tr>
<tr class="even">
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
<td><p><a href="activeconditions.md" data-raw-source="[&lt;strong&gt;ActiveConditions&lt;/strong&gt;](activeconditions.md)"><strong>ActiveConditions</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

WSD 扫描服务指定中的唯一标识符**Id**此特性**DeviceCondition**元素。 可以使用客户端**Id**，以及值[**时间**](time.md)元素，以确定错误条件是新的或具有已得到解决。 WSD 扫描服务不重复使用尽可能长时间的标识符。 此延迟可确保，客户端可以准确地跟踪的单个**DeviceCondition**元素。

WSD 扫描服务将通过发送有关扫描程序的状态更改通知客户端[ **ScannerStatusConditionEvent** ](scannerstatusconditionevent.md)事件。 客户端可以直接查询扫描程序的状态，通过调用[ **GetScannerElementsRequest** ](getscannerelementsrequest.md)操作。

## <a name="see-also"></a>另请参阅


[**ActiveConditions**](activeconditions.md)

[**组件**](component.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**名称 Elementfor DeviceCondition 和 ConditionHistoryEntry**](name-element-for-devicecondition-and-conditionhistoryentry.md)

[**ScannerStatusConditionEvent**](scannerstatusconditionevent.md)

[**严重级别**](severity.md)

[**时间**](time.md)

 

 






