---
title: JobToken 元素
description: 必需的 JobToken 元素包含用于新扫描作业的设备创建的令牌。
keywords:
- JobToken 元素图像设备
topic_type:
- apiref
api_name:
- wscn JobToken
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b2a5c6fde0811ce85983f9fa18e1f312ed85cbb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824119"
---
# <a name="jobtoken-element"></a>JobToken 元素


必需的 **JobToken** 元素包含用于新扫描作业的设备创建的令牌。

<a name="usage"></a>使用情况
-----

```xml
<wscn:JobToken>
  text
</wscn:JobToken>
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
<td><p><a href="createscanjobresponse.md" data-raw-source="[&lt;strong&gt;CreateScanJobResponse&lt;/strong&gt;](createscanjobresponse.md)"><strong>CreateScanJobResponse</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="retrieveimagerequest.md" data-raw-source="[&lt;strong&gt;RetrieveImageRequest&lt;/strong&gt;](retrieveimagerequest.md)"><strong>RetrieveImageRequest</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**JobToken** 元素与 [**JobId**](jobid.md)元素配对，以唯一表示特定扫描作业。 **JobToken** 会传递到 [**RetrieveImageRequest**](retrieveimagerequest.md) 操作元素中的扫描设备，以使设备能够验证扫描请求者是否确实创建了扫描作业。

## <a name="see-also"></a>请参阅


[**CreateScanJobResponse**](createscanjobresponse.md)

[**JobId**](jobid.md)

[**RetrieveImageRequest**](retrieveimagerequest.md)

 

 






