---
title: JobName 元素
description: 必需的 JobName 元素指定扫描作业的客户端提供的用户友好名称。
keywords:
- JobName 元素图像设备
topic_type:
- apiref
api_name:
- wscn JobName
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb89c329df1c5400b5668fb6e0d528d0b1509d2a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789871"
---
# <a name="jobname-element"></a>JobName 元素


必需的 **JobName** 元素指定扫描作业的客户端提供的用户友好名称。

<a name="usage"></a>使用情况
-----

```xml
<wscn:JobName>
  text
</wscn:JobName>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 任何有效的字符串。

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
<td><p><a href="jobdescription.md" data-raw-source="[&lt;strong&gt;JobDescription&lt;/strong&gt;](jobdescription.md)"><strong>JobDescription</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobendstate.md" data-raw-source="[&lt;strong&gt;JobEndState&lt;/strong&gt;](jobendstate.md)"><strong>JobEndState</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="jobsummary.md" data-raw-source="[&lt;strong&gt;JobSummary&lt;/strong&gt;](jobsummary.md)"><strong>JobSummary</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

客户端应提供一个值以帮助用户轻松区分他们所提交的作业。

WSD 扫描服务可以在其 [**DefaultScanTicket**](defaultscanticket.md)元素中提供默认的 **JobName** 名称。 可以采用特定于实现的方式来设置此名称。

提交作业的用户的名称是在 [**JobOriginatingUserName**](joboriginatingusername.md) 元素中指定的。

## <a name="see-also"></a>请参阅


[**DefaultScanTicket**](defaultscanticket.md)

[**JobDescription**](jobdescription.md)

[**JobEndState**](jobendstate.md)

[**JobOriginatingUserName**](joboriginatingusername.md)

[**JobSummary**](jobsummary.md)

 

 






