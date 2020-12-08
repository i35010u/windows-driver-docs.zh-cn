---
title: JobOriginatingUserName 元素
description: 必需的 JobOriginatingUserName 元素指定提交扫描作业的用户的名称。
keywords:
- JobOriginatingUserName 元素图像设备
topic_type:
- apiref
api_name:
- wscn JobOriginatingUserName
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: abad3c27248e74dc440d64c0cc1a7af48747bdce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789869"
---
# <a name="joboriginatingusername-element"></a>JobOriginatingUserName 元素


必需的 **JobOriginatingUserName** 元素指定提交扫描作业的用户的名称。

<a name="usage"></a>使用情况
-----

```xml
<wscn:JobOriginatingUserName>
  text
</wscn:JobOriginatingUserName>
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

客户端或安全基础结构（如果有）提供了 **JobOriginatingUserName** 元素。 客户端应提供一个值，以帮助用户轻松区分其所提交的作业和其他用户提交的作业。

WSD 扫描服务可以在其 [**DefaultScanTicket**](defaultscanticket.md)元素中提供默认的 **JobOriginatingUserName** 名称。 可以采用特定于实现的方式来设置此名称。

在 [**JobName**](jobname.md) 元素中指定作业的名称。

## <a name="see-also"></a>请参阅


[**DefaultScanTicket**](defaultscanticket.md)

[**JobDescription**](jobdescription.md)

[**JobEndState**](jobendstate.md)

[**JobName**](jobname.md)

[**JobSummary**](jobsummary.md)

 

 






