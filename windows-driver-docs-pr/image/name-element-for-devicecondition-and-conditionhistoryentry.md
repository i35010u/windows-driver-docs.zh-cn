---
title: DeviceCondition 和 ConditionHistoryEntry 元素的 Name 元素
description: 必需的 Name 元素命名 DeviceCondition 或 ConditionHistoryEntry 元素中指定的当前错误条件。
keywords:
- DeviceCondition 和 ConditionHistoryEntry 元素图像处理设备的 Name 元素
topic_type:
- apiref
api_name:
- wscn Name
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b640e5e1e6b3f7b840d3fdacfd814e03cdebbe69
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827119"
---
# <a name="name-element-for-devicecondition-and-conditionhistoryentry-element"></a>DeviceCondition 和 ConditionHistoryEntry 元素的 Name 元素


必需的 **Name** 元素命名 [**DeviceCondition**](devicecondition.md) 或 [**ConditionHistoryEntry**](conditionhistoryentry.md) 元素中指定的当前错误条件。

<a name="usage"></a>使用情况
-----

```xml
<wscn:Name>
  text
</wscn:Name>
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
<td><p><span id="Calibrating"></span><span id="calibrating"></span><span id="CALIBRATING"></span>校准</p></td>
<td><p>扫描设备正在校准其内部组件，以便准备获取映像。</p></td>
</tr>
<tr class="even">
<td><p><span id="CoverOpen"></span><span id="coveropen"></span><span id="COVEROPEN"></span>CoverOpen</p></td>
<td><p>扫描设备中的一个或多个内容已打开。</p></td>
</tr>
<tr class="odd">
<td><p><span id="InputTrayEmpty"></span><span id="inputtrayempty"></span><span id="INPUTTRAYEMPTY"></span>InputTrayEmpty</p></td>
<td><p>自动文档送纸器 (ADF) 输入没有介质。</p></td>
</tr>
<tr class="even">
<td><p><span id="InterlockOpen"></span><span id="interlockopen"></span><span id="INTERLOCKOPEN"></span>InterlockOpen</p></td>
<td><p>互锁处于打开状态。</p></td>
</tr>
<tr class="odd">
<td><p><span id="InternalStorageFull"></span><span id="internalstoragefull"></span><span id="INTERNALSTORAGEFULL"></span>InternalStorageFull</p></td>
<td><p>当前写入的内部存储组件已满。</p></td>
</tr>
<tr class="even">
<td><p><span id="LampError"></span><span id="lamperror"></span><span id="LAMPERROR"></span>LampError</p></td>
<td><p>扫描仪灯出现故障，无法继续进行图像采集。</p></td>
</tr>
<tr class="odd">
<td><p><span id="LampWarming"></span><span id="lampwarming"></span><span id="LAMPWARMING"></span>LampWarming</p></td>
<td><p>扫描仪灯正在预热，准备获取映像。</p></td>
</tr>
<tr class="even">
<td><p><span id="MediaJam"></span><span id="mediajam"></span><span id="MEDIAJAM"></span>MediaJam</p></td>
<td><p>媒体在一个输入源中卡住，因此图像采集失败。</p></td>
</tr>
<tr class="odd">
<td><p><span id="MultipleFeedError"></span><span id="multiplefeederror"></span><span id="MULTIPLEFEEDERROR"></span>MultipleFeedError</p></td>
<td><p>ADF 同时送入了多片介质。</p></td>
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

某些错误名称仅对某些 [**组件**](component.md) 元素有效。

可以扩展和子集化此元素的允许值。

## <a name="see-also"></a>请参阅


[**组件**](component.md)

[**ConditionHistoryEntry**](conditionhistoryentry.md)

[**DeviceCondition**](devicecondition.md)

 

 






