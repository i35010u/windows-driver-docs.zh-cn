---
title: JobId 元素
description: 所需的 JobId 元素唯一地标识扫描程序中的作业。
ms.assetid: ae9199c1-c45a-4147-b4f0-f37a9a0f1b22
keywords:
- JobId 元素成像设备
topic_type:
- apiref
api_name:
- wscn JobId
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c69e5f27152036cf8d1a220205228b9d37802d91
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542103"
---
# <a name="jobid-element"></a>JobId 元素


所需**JobId**元素唯一地标识扫描程序中的作业。

<a name="usage"></a>用法
-----

```xml
<wscn:JobId>
  text
</wscn:JobId>
```

<a name="attributes"></a>属性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 介于 1 到 2147483648 的整数值。

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
<td><p><a href="canceljobrequest.md" data-raw-source="[&lt;strong&gt;CancelJobRequest&lt;/strong&gt;](canceljobrequest.md)"><strong>CancelJobRequest</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="createscanjobresponse.md" data-raw-source="[&lt;strong&gt;CreateScanJobResponse&lt;/strong&gt;](createscanjobresponse.md)"><strong>CreateScanJobResponse</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="getjobelementsrequest.md" data-raw-source="[&lt;strong&gt;GetJobElementsRequest&lt;/strong&gt;](getjobelementsrequest.md)"><strong>GetJobElementsRequest</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobendstate.md" data-raw-source="[&lt;strong&gt;JobEndState&lt;/strong&gt;](jobendstate.md)"><strong>JobEndState</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"><strong>JobStatus</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobsummary.md" data-raw-source="[&lt;strong&gt;JobSummary&lt;/strong&gt;](jobsummary.md)"><strong>JobSummary</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="retrieveimagerequest.md" data-raw-source="[&lt;strong&gt;RetrieveImageRequest&lt;/strong&gt;](retrieveimagerequest.md)"><strong>RetrieveImageRequest</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

WSD 扫描服务将返回**JobId**通过在客户端元素[ **CreateScanJobResponse** ](createscanjobresponse.md)操作元素。 客户端使用返回**JobId**当它启动的扫描请求通过[ **RetrieveImageRequest** ](retrieveimagerequest.md)操作元素。

**JobId**不需要是全局唯一的。 WSD 扫描服务不应重复使用最近分配的值，以便客户端不会将具有较早的作业的当前扫描作业相混淆。

不能扩展的允许的值为**JobId**元素。

## <a name="see-also"></a>另请参阅


[**CancelJobRequest**](canceljobrequest.md)

[**CreateScanJobResponse**](createscanjobresponse.md)

[**GetJobElementsRequest**](getjobelementsrequest.md)

[**JobEndState**](jobendstate.md)

[**JobStatus**](jobstatus.md)

[**JobSummary**](jobsummary.md)

[**RetrieveImageRequest**](retrieveimagerequest.md)

 

 






