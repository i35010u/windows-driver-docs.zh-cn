---
title: JobDescription 元素
description: 所需的 JobDescription 元素包含当前标识作业的基本创建信息。
ms.assetid: 78b77a9b-2fe9-4261-996b-970e97c4c0a9
keywords:
- JobDescription 元素成像设备
topic_type:
- apiref
api_name:
- wscn JobDescription
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7acf05250ae0afebce5d3fbc54e486079b74b31
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363355"
---
# <a name="jobdescription-element"></a>JobDescription 元素


所需**JobDescription**元素包含当前标识作业的基本创建信息。

<a name="usage"></a>用法
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

客户端设置的值为所有**JobDescription**子元素并将其在提交[ **CreateScanJobRequest** ](createscanjobrequest.md)操作。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DefaultScanTicket**](defaultscanticket.md)

[**JobInformation**](jobinformation.md)

[**JobName**](jobname.md)

[**JobOriginatingUserName**](joboriginatingusername.md)

[**ScanTicket**](scanticket.md)

 

 






