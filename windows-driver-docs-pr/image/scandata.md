---
title: ScanData 元素
description: 必需的 ScanData 元素包含表示扫描图像的二进制数据。
keywords:
- ScanData 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScanData
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fba24e3dbdfea737f3127e22686795b14673133
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839537"
---
# <a name="scandata-element"></a>ScanData 元素


必需的 **ScanData** 元素包含表示扫描图像的二进制数据。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ScanData/>
```

<a name="attributes"></a>特性
----------

没有特性。

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
<td><p><a href="retrieveimageresponse.md" data-raw-source="[&lt;strong&gt;RetrieveImageResponse&lt;/strong&gt;](retrieveimageresponse.md)"><strong>RetrieveImageResponse</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**ScanData** 元素包含一个 **xop： Include** 元素，该元素指定扫描数据相对于 [**RetrieveImageResponse**](retrieveimageresponse.md)操作元素的 SOAP 信封/正文的位置。 实际扫描数据以二进制附件的形式追加到 SOAP 信封/正文。

## <a name="see-also"></a>请参阅


[**RetrieveImageResponse**](retrieveimageresponse.md)

 

 






