---
title: CancelJobRequest 元素
description: 所需的 CancelJobRequest 操作使客户端可以取消扫描作业。
keywords:
- CancelJobRequest 元素图像设备
topic_type:
- apiref
api_name:
- wscn CancelJobRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 200e7abed1281272d76b7cfe37d1a56cb84d456e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840981"
---
# <a name="canceljobrequest-element"></a>CancelJobRequest 元素


所需的 **CancelJobRequest** 操作使客户端可以取消扫描作业。

<a name="usage"></a>使用情况
-----

```xml
<wscn:CancelJobRequest>
  child elements
</wscn:CancelJobRequest>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

无

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
<td><p><a href="jobid.md" data-raw-source="[&lt;strong&gt;JobId&lt;/strong&gt;](jobid.md)"><strong>JobId</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

[**JobId**](jobid.md)

客户端可以取消扫描作业，从创建作业的时间到完成、取消或中止。 [**JobId**](jobid.md)元素标识客户端正在尝试取消的作业。

如果作业处于 "**挂起**" 或 "**活动**" 状态，则 WSD 扫描服务应将指定的作业移动到 **终止** 状态。 尝试取消已完成或已取消的作业或尝试取消客户端无权的任何作业是错误的。

[**常见的 Wsd 扫描服务操作错误代码**](common-wsd-scan-service-operation-error-codes.md)[Wsd 扫描服务操作错误报告](wsd-scan-service-operation-error-reporting.md)

此操作可以返回所有常见的 [**WSD 扫描服务操作错误代码**](common-wsd-scan-service-operation-error-codes.md)。 有关如何报告错误的详细信息，请参阅 [WSD 扫描服务操作错误报告](wsd-scan-service-operation-error-reporting.md)。

**CancelJobRequest** 也可以返回以下错误代码：

-   **ClientErrorJobIdNotFound**

## <a name="see-also"></a>请参阅


[**CancelJobResponse**](canceljobresponse.md)

[**JobId**](jobid.md)

 

 






