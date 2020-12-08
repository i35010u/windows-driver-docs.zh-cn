---
title: JobDescription 元素
description: 必需的 JobDescription 元素包含当前标识作业的基本创建信息。
keywords:
- JobDescription 元素图像设备
topic_type:
- apiref
api_name:
- wscn JobDescription
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9191b462cf5717b6c18ce74008d6bb5e4da6cac3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834547"
---
# <a name="jobdescription-element"></a>JobDescription 元素


必需的 **JobDescription** 元素包含当前标识作业的基本创建信息。

<a name="usage"></a>使用情况
-----

```xml
<wscn:JobDescription>
  child elements
</wscn:JobDescription>
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
<td><p><a href="jobinformation.md" data-raw-source="[&lt;strong&gt;JobInformation&lt;/strong&gt;](jobinformation.md)"><strong>JobInformation</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobname.md" data-raw-source="[&lt;strong&gt;JobName&lt;/strong&gt;](jobname.md)"><strong>JobName</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="joboriginatingusername.md" data-raw-source="[&lt;strong&gt;JobOriginatingUserName&lt;/strong&gt;](joboriginatingusername.md)"><strong>JobOriginatingUserName</strong></a></p></td>
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
<td><p><a href="defaultscanticket.md" data-raw-source="[&lt;strong&gt;DefaultScanTicket&lt;/strong&gt;](defaultscanticket.md)"><strong>DefaultScanTicket</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanticket.md" data-raw-source="[&lt;strong&gt;ScanTicket&lt;/strong&gt;](scanticket.md)"><strong>ScanTicket</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

客户端设置所有 **JobDescription** 子元素的值，并在 [**CreateScanJobRequest**](createscanjobrequest.md) 操作中提交这些值。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DefaultScanTicket**](defaultscanticket.md)

[**JobInformation**](jobinformation.md)

[**JobName**](jobname.md)

[**JobOriginatingUserName**](joboriginatingusername.md)

[**ScanTicket**](scanticket.md)

 

 






