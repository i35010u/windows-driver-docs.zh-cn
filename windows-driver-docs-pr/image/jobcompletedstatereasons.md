---
title: JobCompletedStateReasons 元素
description: 所需的 JobCompletedStateReasons 元素是有关如何以及为何扫描作业已完成的所有其他信息的集合。
ms.assetid: 678384b4-a023-4c79-a68a-4a2cc3a04a0e
keywords:
- JobCompletedStateReasons 元素成像设备
topic_type:
- apiref
api_name:
- wscn JobCompletedStateReasons
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e1c9c8bc56daa957ae99bb762e863bd2ad16c24
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563002"
---
# <a name="jobcompletedstatereasons-element"></a>JobCompletedStateReasons 元素


所需**JobCompletedStateReasons**元素是有关如何以及为何扫描作业已完成的所有其他信息的集合。

<a name="usage"></a>用法
-----

```xml
<wscn:JobCompletedStateReasons>
  child elements
</wscn:JobCompletedStateReasons>
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
<td><p><a href="jobstatereason.md" data-raw-source="[&lt;strong&gt;JobStateReason&lt;/strong&gt;](jobstatereason.md)"><strong>JobStateReason</strong></a></p></td>
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
<td><p><a href="jobendstate.md" data-raw-source="[&lt;strong&gt;JobEndState&lt;/strong&gt;](jobendstate.md)"><strong>JobEndState</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**JobCompletedStateReasons**元素包含零个或多[ **JobStateReason** ](jobstatereason.md)元素，其中每个包含如何或为什么扫描作业已完成的原因。 WSD 扫描服务发送**JobCompletedStateReasons**通过客户端元素[ **JobEndStateEvent** ](jobendstateevent.md)事件元素。

## <a name="see-also"></a>请参阅


[**JobEndState**](jobendstate.md)

[**JobEndStateEvent**](jobendstateevent.md)

[**JobStateReason**](jobstatereason.md)

 

 






