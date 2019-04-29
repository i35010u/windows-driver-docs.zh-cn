---
title: 对于 DeviceCondition 和 ConditionHistoryEntry 元素的 name 元素
description: 所需的 Name 元素命名当前 DeviceCondition 或 ConditionHistoryEntry 元素中指定的错误条件。
ms.assetid: 1ac530ed-dc31-4af0-a89b-0860a36bbfeb
keywords:
- DeviceCondition 和 ConditionHistoryEntry 元素图像处理设备的名称元素
topic_type:
- apiref
api_name:
- wscn Name
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56b1a0f33954c40a54e4db398b3a98533d244316
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379663"
---
# <a name="name-element-for-devicecondition-and-conditionhistoryentry-element"></a>对于 DeviceCondition 和 ConditionHistoryEntry 元素的 name 元素


所需**名称**元素名称中指定的当前错误条件[ **DeviceCondition** ](devicecondition.md)或者[ **ConditionHistoryEntry** ](conditionhistoryentry.md)元素。

<a name="usage"></a>用法
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
<td><p>扫描设备校准及其内部组件进行准备，以便获取映像。</p></td>
</tr>
<tr class="even">
<td><p><span id="CoverOpen"></span><span id="coveropen"></span><span id="COVEROPEN"></span>CoverOpen</p></td>
<td><p>一个扫描设备上的多个后台处于打开状态。</p></td>
</tr>
<tr class="odd">
<td><p><span id="InputTrayEmpty"></span><span id="inputtrayempty"></span><span id="INPUTTRAYEMPTY"></span>InputTrayEmpty</p></td>
<td><p>自动文档送纸器 (ADF) 输入包含任何媒体。</p></td>
</tr>
<tr class="even">
<td><p><span id="InterlockOpen"></span><span id="interlockopen"></span><span id="INTERLOCKOPEN"></span>InterlockOpen</p></td>
<td><p>互锁处于打开状态。</p></td>
</tr>
<tr class="odd">
<td><p><span id="InternalStorageFull"></span><span id="internalstoragefull"></span><span id="INTERNALSTORAGEFULL"></span>InternalStorageFull</p></td>
<td><p>当前正在写入到的内部存储组件已满。</p></td>
</tr>
<tr class="even">
<td><p><span id="LampError"></span><span id="lamperror"></span><span id="LAMPERROR"></span>LampError</p></td>
<td><p>扫描程序 lamp 失败的原因和图像采集无法继续。</p></td>
</tr>
<tr class="odd">
<td><p><span id="LampWarming"></span><span id="lampwarming"></span><span id="LAMPWARMING"></span>LampWarming</p></td>
<td><p>扫描程序 lamp 正在预热进行准备，以便获取映像。</p></td>
</tr>
<tr class="even">
<td><p><span id="MediaJam"></span><span id="mediajam"></span><span id="MEDIAJAM"></span>MediaJam</p></td>
<td><p>媒体被印象中其中一个输入源，因此图像获取失败。</p></td>
</tr>
<tr class="odd">
<td><p><span id="MultipleFeedError"></span><span id="multiplefeederror"></span><span id="MULTIPLEFEEDERROR"></span>MultipleFeedError</p></td>
<td><p>ADF 是同时提供多个的介质。</p></td>
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

某些错误名称的有效值只有某些特定[**组件**](component.md)元素。

您都可以扩展和子集的允许的值为此元素。

## <a name="see-also"></a>请参阅


[**组件**](component.md)

[**ConditionHistoryEntry**](conditionhistoryentry.md)

[**DeviceCondition**](devicecondition.md)

 

 






