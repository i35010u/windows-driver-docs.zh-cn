---
title: CancelJobRequest 元素
description: 所需的 CancelJobRequest 操作允许客户端取消扫描作业。
ms.assetid: 781fae32-2827-48d8-8aed-7f437326919d
keywords:
- CancelJobRequest 元素成像设备
topic_type:
- apiref
api_name:
- wscn CancelJobRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3028dc3472eb3cd74a87e6c9e2812a9a77b57297
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520149"
---
# <a name="canceljobrequest-element"></a>CancelJobRequest 元素


所需**CancelJobRequest**操作启用客户端，若要取消扫描作业。

<a name="usage"></a>用法
-----

```xml
<wscn:CancelJobRequest>
  child elements
</wscn:CancelJobRequest>
```

<a name="attributes"></a>属性
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

客户端可以取消将扫描作业从最它是已完成、 取消的或已中止的时间创建的作业的时间。 [ **JobId** ](jobid.md)元素标识客户端尝试取消该作业。

WSD 扫描服务应移动到指定的作业**正在终止**状态的作业是否已在**挂起**或**Active**状态。 它是错误尝试取消已完成或已取消作业或尝试取消客户端不具有权限的任何作业。

[**常见的 WSD 扫描服务操作错误代码**](common-wsd-scan-service-operation-error-codes.md)[WSD 扫描服务操作错误报告](wsd-scan-service-operation-error-reporting.md)

此操作可以返回的所有[**常见 WSD 扫描服务操作的错误代码**](common-wsd-scan-service-operation-error-codes.md)。 有关如何对报告错误的详细信息，请参阅[WSD 扫描服务操作错误报告](wsd-scan-service-operation-error-reporting.md)。

**CancelJobRequest**还可以返回以下错误代码：

-   **ClientErrorJobIdNotFound**

## <a name="see-also"></a>另请参阅


[**CancelJobResponse**](canceljobresponse.md)

[**JobId**](jobid.md)

 

 






