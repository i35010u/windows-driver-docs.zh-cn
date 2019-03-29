---
title: JobOriginatingUserName 元素
description: 所需的 JobOriginatingUserName 元素指定提交扫描作业的用户的名称。
ms.assetid: ba2dd472-1ac0-40bd-816c-02abc093b6ed
keywords:
- JobOriginatingUserName 元素成像设备
topic_type:
- apiref
api_name:
- wscn JobOriginatingUserName
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0158fdb766871484a1d408d28460340b71c8a1a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561897"
---
# <a name="joboriginatingusername-element"></a>JobOriginatingUserName 元素


所需**JobOriginatingUserName**元素指定提交扫描作业的用户的名称。

<a name="usage"></a>用法
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

必需。 任何有效字符的字符串。

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

如果有的话，客户端或安全基础结构，提供**JobOriginatingUserName**元素。 客户端应提供一个值，以帮助用户轻松区分他们已提交的作业和其他用户提交的作业。

WSD 扫描服务可以提供默认值**JobOriginatingUserName**名称在其[ **DefaultScanTicket** ](defaultscanticket.md)元素。 您可以以特定于实现的方式设置此名称。

中指定的作业名称[ **JobName** ](jobname.md)元素。

## <a name="see-also"></a>请参阅


[**DefaultScanTicket**](defaultscanticket.md)

[**JobDescription**](jobdescription.md)

[**JobEndState**](jobendstate.md)

[**JobName**](jobname.md)

[**JobSummary**](jobsummary.md)

 

 






