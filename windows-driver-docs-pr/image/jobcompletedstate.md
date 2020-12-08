---
title: JobCompletedState 元素
description: 必需的 JobCompletedState 元素指定作业的最终作业状态。
keywords:
- JobCompletedState 元素图像设备
topic_type:
- apiref
api_name:
- wscn JobCompletedState
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad6ed5b1927b513286d13dac7ad9a294e12cb07c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799545"
---
# <a name="jobcompletedstate-element"></a>JobCompletedState 元素


必需的 **JobCompletedState** 元素指定作业的最终作业状态。

<a name="usage"></a>使用情况
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

必需。 [**JobState**](jobstate.md)元素中的以下值之一：

-   Aborted
-   已取消
-   已完成
-   正在终止

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
<td><p><a href="jobendstate.md" data-raw-source="[&lt;strong&gt;JobEndState&lt;/strong&gt;](jobendstate.md)"><strong>JobEndState</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

WSD 扫描服务将 **JobCompletedState** 元素发送到 [**JobEndStateEvent**](jobendstateevent.md) 事件元素中的客户端。

## <a name="see-also"></a>请参阅


[**JobEndState**](jobendstate.md)

[**JobEndStateEvent**](jobendstateevent.md)

[**JobState**](jobstate.md)

 

 






