---
title: JobId 元素
description: 所需的 JobId 元素在扫描仪中唯一标识作业。
keywords:
- JobId 元素图像处理设备
topic_type:
- apiref
api_name:
- wscn JobId
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d708346759e9a714d4c2aa191bfc7fc0f8e8821f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789877"
---
# <a name="jobid-element"></a>JobId 元素


所需的 **JobId** 元素在扫描仪中唯一标识作业。

<a name="usage"></a>使用情况
-----

```xml
<wscn:JobId>
  text
</wscn:JobId>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 1到2147483648之间的一个整数值。

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

WSD 扫描服务通过 [**CreateScanJobResponse**](createscanjobresponse.md)操作元素将 **JobId** 元素返回到客户端。 当客户端通过 [**RetrieveImageRequest**](retrieveimagerequest.md)操作元素启动扫描请求时，会使用返回的 **JobId** 。

**JobId** 不必是全局唯一的。 WSD 扫描服务不应重复使用最近分配的值，因此客户端不会将当前扫描作业与较旧的作业混淆。

不能为 **JobId** 元素扩展允许的值。

## <a name="see-also"></a>请参阅


[**CancelJobRequest**](canceljobrequest.md)

[**CreateScanJobResponse**](createscanjobresponse.md)

[**GetJobElementsRequest**](getjobelementsrequest.md)

[**JobEndState**](jobendstate.md)

[**JobStatus**](jobstatus.md)

[**JobSummary**](jobsummary.md)

[**RetrieveImageRequest**](retrieveimagerequest.md)

 

 






