---
title: ConditionHistoryEntry 元素
description: 所需的 ConditionHistoryEntry 元素上扫描程序提供有关过去的条件之一的详细信息。
ms.assetid: 2a5d52c2-6389-4afe-be6c-4645d62ccda0
keywords:
- ConditionHistoryEntry 元素成像设备
topic_type:
- apiref
api_name:
- wscn ConditionHistoryEntry wscn Id "..."
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d270449409f1722108ef2dbce7ab06e0b60f579
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373209"
---
# <a name="conditionhistoryentry-element"></a>ConditionHistoryEntry 元素


所需**ConditionHistoryEntry**元素上扫描程序提供有关过去的条件之一的详细信息。

<a name="usage"></a>用法
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
<th>特性</th>
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
<td><p><a href="cleartime.md" data-raw-source="[&lt;strong&gt;ClearTime&lt;/strong&gt;](cleartime.md)"><strong>ClearTime</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="component.md" data-raw-source="[&lt;strong&gt;Component&lt;/strong&gt;](component.md)"><strong>组件</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="name-element-for-devicecondition-and-conditionhistoryentry.md" data-raw-source="[&lt;strong&gt;Name forParents DeviceCondition and ConditionHistoryEntry&lt;/strong&gt;](name-element-for-devicecondition-and-conditionhistoryentry.md)"><strong>名称 forParents DeviceCondition 和 ConditionHistoryEntry</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="severity.md" data-raw-source="[&lt;strong&gt;Severity&lt;/strong&gt;](severity.md)"><strong>严重级别</strong></a></p></td>
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

WSD 扫描服务指定中的唯一标识符**Id**此特性**ConditionHistoryEntry**元素。 可以使用客户端**Id**，以及值[**时间**](time.md)元素，以确定错误条件是新的或具有已得到解决。 WSD 扫描服务不重复使用尽可能长时间的标识符。 此延迟可确保，客户端可以准确地跟踪的单个**ConditionHistoryEntry**元素。

不能扩展的允许的值为**Id**。

## <a name="see-also"></a>请参阅


[**ClearTime**](cleartime.md)

[**组件**](component.md)

[**ConditionHistory**](conditionhistory.md)

[**DeviceCondition**](devicecondition.md)

[**名称 forParents DeviceCondition 和 ConditionHistoryEntry**](name-element-for-devicecondition-and-conditionhistoryentry.md)

[**严重级别**](severity.md)

[**时间**](time.md)

 

 






