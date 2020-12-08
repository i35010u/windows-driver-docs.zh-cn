---
title: DeviceCondition 元素
description: 可选的 DeviceCondition 元素提供有关扫描仪的当前活动状态的详细信息。
keywords:
- DeviceCondition 元素图像设备
topic_type:
- apiref
api_name:
- wscn DeviceCondition wscn Id "..."
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f16339e12eed2f57af0b2245a97c7c1970efa111
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824557"
---
# <a name="devicecondition-element"></a>DeviceCondition 元素


可选的 **DeviceCondition** 元素提供有关扫描仪的当前活动状态的详细信息。

<a name="usage"></a>使用情况
-----

```xml
<wscn:DeviceCondition wscn:Id="..."
  Id = "xs:string">
  child elements
</wscn:DeviceCondition wscn:Id="...">
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
<td><p><a href="component.md" data-raw-source="[&lt;strong&gt;Component&lt;/strong&gt;](component.md)"><strong>组件</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="name-element-for-devicecondition-and-conditionhistoryentry.md" data-raw-source="[&lt;strong&gt;Name Elementfor DeviceCondition and ConditionHistoryEntry&lt;/strong&gt;](name-element-for-devicecondition-and-conditionhistoryentry.md)"><strong>Name Elementfor DeviceCondition and ConditionHistoryEntry</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="severity.md" data-raw-source="[&lt;strong&gt;Severity&lt;/strong&gt;](severity.md)"><strong>严重性</strong></a></p></td>
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

WSD 扫描服务指定此 **DeviceCondition** 元素的 **Id** 属性中的唯一标识符。 客户端可以使用 **Id** 和 [**时间**](time.md) 元素的值来确定错误条件是新的还是已消失。 WSD 扫描服务不得尽可能长地重复使用标识符。 此延迟可确保客户端能够准确地跟踪单个 **DeviceCondition** 元素。

WSD 扫描服务通过发送 [**ScannerStatusConditionEvent**](scannerstatusconditionevent.md) 事件向客户端通知扫描程序状态的更改。 客户端可以通过调用 [**GetScannerElementsRequest**](getscannerelementsrequest.md) 操作直接查询扫描程序的状态。

## <a name="see-also"></a>请参阅


[**ActiveConditions**](activeconditions.md)

[**组件**](component.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**Name Elementfor DeviceCondition and ConditionHistoryEntry**](name-element-for-devicecondition-and-conditionhistoryentry.md)

[**ScannerStatusConditionEvent**](scannerstatusconditionevent.md)

[**严重性**](severity.md)

[**时间**](time.md)

 

 






