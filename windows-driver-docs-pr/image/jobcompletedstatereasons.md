---
title: JobCompletedStateReasons 元素
description: 必需的 JobCompletedStateReasons 元素是有关扫描作业的完成方式和原因的所有其他信息的集合。
keywords:
- JobCompletedStateReasons 元素图像设备
topic_type:
- apiref
api_name:
- wscn JobCompletedStateReasons
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14e7cd469bc7f6108e0f40eca0744eb07459f679
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799546"
---
# <a name="jobcompletedstatereasons-element"></a>JobCompletedStateReasons 元素


必需的 **JobCompletedStateReasons** 元素是有关扫描作业的完成方式和原因的所有其他信息的集合。

<a name="usage"></a>使用情况
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

**JobCompletedStateReasons** 元素包含零个或多个 [**JobStateReason**](jobstatereason.md)元素，其中每个元素都包含扫描作业的完成方式或原因。 WSD 扫描服务通过 [**JobEndStateEvent**](jobendstateevent.md)事件元素将 **JobCompletedStateReasons** 元素发送到客户端。

## <a name="see-also"></a>请参阅


[**JobEndState**](jobendstate.md)

[**JobEndStateEvent**](jobendstateevent.md)

[**JobStateReason**](jobstatereason.md)

 

 






