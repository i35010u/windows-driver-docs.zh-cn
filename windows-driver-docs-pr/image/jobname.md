---
title: JobName 元素
description: 所需的 JobName 元素指定扫描作业的客户端提供的、 用户友好名称。
ms.assetid: b6d2baba-6a2e-4971-880b-9a4df66dc1ae
keywords:
- JobName 元素成像设备
topic_type:
- apiref
api_name:
- wscn JobName
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0160e44812155cac4ac16a1ef4f3c2b97f8775a3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348805"
---
# <a name="jobname-element"></a>JobName 元素


所需**JobName**元素指定扫描作业的客户端提供的、 用户友好名称。

<a name="usage"></a>用法
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

客户端应提供一个值，以帮助用户轻松区分他们已提交的作业。

WSD 扫描服务可以提供默认值**JobName**名称在其[ **DefaultScanTicket** ](defaultscanticket.md)元素。 您可以以特定于实现的方式设置此名称。

中指定的提交该作业的用户名称[ **JobOriginatingUserName** ](joboriginatingusername.md)元素。

## <a name="see-also"></a>请参阅


[**DefaultScanTicket**](defaultscanticket.md)

[**JobDescription**](jobdescription.md)

[**JobEndState**](jobendstate.md)

[**JobOriginatingUserName**](joboriginatingusername.md)

[**JobSummary**](jobsummary.md)

 

 






