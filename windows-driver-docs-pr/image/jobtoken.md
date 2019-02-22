---
title: JobToken 元素
description: 所需的 JobToken 元素包含一个新的扫描作业的设备创建令牌。
ms.assetid: 09446fc0-074a-4f54-93fa-55b4dd467fad
keywords:
- JobToken 元素成像设备
topic_type:
- apiref
api_name:
- wscn JobToken
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d022c3307f292691c292c1a5eeea8e10178172d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519751"
---
# <a name="jobtoken-element"></a>JobToken 元素


所需**JobToken**元素包含一个新的扫描作业的设备创建令牌。

<a name="usage"></a>用法
-----

```xml
<wscn:JobToken>
  text
</wscn:JobToken>
```

<a name="attributes"></a>属性
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
<td><p><a href="createscanjobresponse.md" data-raw-source="[&lt;strong&gt;CreateScanJobResponse&lt;/strong&gt;](createscanjobresponse.md)"><strong>CreateScanJobResponse</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="retrieveimagerequest.md" data-raw-source="[&lt;strong&gt;RetrieveImageRequest&lt;/strong&gt;](retrieveimagerequest.md)"><strong>RetrieveImageRequest</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**JobToken**元素搭配[ **JobId** ](jobid.md)元素来唯一地表示特定扫描作业。 **JobToken**传递给扫描设备[ **RetrieveImageRequest** ](retrieveimagerequest.md)操作元素以启用该设备以验证扫描请求者实际创建扫描作业。

## <a name="see-also"></a>另请参阅


[**CreateScanJobResponse**](createscanjobresponse.md)

[**JobId**](jobid.md)

[**RetrieveImageRequest**](retrieveimagerequest.md)

 

 






