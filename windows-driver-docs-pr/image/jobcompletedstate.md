---
title: JobCompletedState 元素
description: 所需的 JobCompletedState 元素指定作业的最终作业状态。
ms.assetid: 41dc029b-2315-465a-8490-1f4e50db0188
keywords:
- JobCompletedState 元素成像设备
topic_type:
- apiref
api_name:
- wscn JobCompletedState
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3fe870e85fe31bd6689ae712e9732c11324cb17
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381646"
---
# <a name="jobcompletedstate-element"></a>JobCompletedState 元素


所需**JobCompletedState**元素指定作业的最终作业状态。

<a name="usage"></a>用法
-----

```xml
<wscn:JobCompletedState>
  text
</wscn:JobCompletedState>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 以下值之一从[ **JobState** ](jobstate.md)元素：

-   已中止
-   Canceled
-   已完成
-   终止

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
<td><p><a href="jobendstate.md" data-raw-source="[&lt;strong&gt;JobEndState&lt;/strong&gt;](jobendstate.md)"><strong>JobEndState</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

WSD 扫描服务发送**JobCompletedState**向客户端中的元素[ **JobEndStateEvent** ](jobendstateevent.md)事件元素。

## <a name="see-also"></a>请参阅


[**JobEndState**](jobendstate.md)

[**JobEndStateEvent**](jobendstateevent.md)

[**JobState**](jobstate.md)

 

 






