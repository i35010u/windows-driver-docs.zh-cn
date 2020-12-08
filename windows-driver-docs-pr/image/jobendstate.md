---
title: JobEndState 元素
description: 必需的 JobEndState 元素描述当前扫描作业的最终状态。
keywords:
- JobEndState 元素图像设备
topic_type:
- apiref
api_name:
- wscn JobEndState
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 522a40f309b3c727e97420331aa7b0b7489e29a0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834539"
---
# <a name="jobendstate-element"></a>JobEndState 元素


必需的 **JobEndState** 元素描述当前扫描作业的最终状态。

<a name="usage"></a>使用情况
-----

```xml
<wscn:JobEndState>
  child elements
</wscn:JobEndState>
```

<a name="attributes"></a>特性
----------

没有特性。

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
<td><p><a href="jobcompletedstate.md" data-raw-source="[&lt;strong&gt;JobCompletedState&lt;/strong&gt;](jobcompletedstate.md)"><strong>JobCompletedState</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobcompletedstatereasons.md" data-raw-source="[&lt;strong&gt;JobCompletedStateReasons&lt;/strong&gt;](jobcompletedstatereasons.md)"><strong>JobCompletedStateReasons</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="jobcompletedtime.md" data-raw-source="[&lt;strong&gt;JobCompletedTime&lt;/strong&gt;](jobcompletedtime.md)"><strong>JobCompletedTime</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobid.md" data-raw-source="[&lt;strong&gt;JobId&lt;/strong&gt;](jobid.md)"><strong>JobId</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="jobname.md" data-raw-source="[&lt;strong&gt;JobName&lt;/strong&gt;](jobname.md)"><strong>JobName</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="joboriginatingusername.md" data-raw-source="[&lt;strong&gt;JobOriginatingUserName&lt;/strong&gt;](joboriginatingusername.md)"><strong>JobOriginatingUserName</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scanscompleted.md" data-raw-source="[&lt;strong&gt;ScansCompleted&lt;/strong&gt;](scanscompleted.md)"><strong>ScansCompleted</strong></a></p></td>
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
<td><p><a href="jobendstateevent.md" data-raw-source="[&lt;strong&gt;JobEndStateEvent&lt;/strong&gt;](jobendstateevent.md)"><strong>JobEndStateEvent</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**JobEndState** 元素包含一些子元素，这些子元素描述有关扫描作业的结束状态的各个方面。 WSD 扫描服务通过 [**JobEndStateEvent**](jobendstateevent.md)元素将 **JobEndState** 元素发送到客户端。

## <a name="see-also"></a>请参阅


[**JobCompletedState**](jobcompletedstate.md)

[**JobCompletedStateReasons**](jobcompletedstatereasons.md)

[**JobCompletedTime**](jobcompletedtime.md)

[**JobEndStateEvent**](jobendstateevent.md)

[**JobId**](jobid.md)

[**JobName**](jobname.md)

[**JobOriginatingUserName**](joboriginatingusername.md)

[**ScansCompleted**](scanscompleted.md)

 

 






