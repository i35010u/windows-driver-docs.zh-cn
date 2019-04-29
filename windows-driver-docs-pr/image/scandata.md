---
title: ScanData 元素
description: 所需的 ScanData 元素包含表示扫描的图像的二进制数据。
ms.assetid: 9b29224c-b1e1-4c64-8a4a-476f9d6eea45
keywords:
- ScanData 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScanData
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cffda2d8858992c2a73fbaeaa1d4dee1e2346a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364391"
---
# <a name="scandata-element"></a>ScanData 元素


所需**ScanData**元素包含表示扫描的图像的二进制数据。

<a name="usage"></a>用法
-----

```xml
<wscn:ScanData/>
```

<a name="attributes"></a>特性
----------

没有特性。

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
<td><p><a href="retrieveimageresponse.md" data-raw-source="[&lt;strong&gt;RetrieveImageResponse&lt;/strong&gt;](retrieveimageresponse.md)"><strong>RetrieveImageResponse</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**ScanData**元素包含**xop： 包括**元素，它指定扫描数据相对于 SOAP 信封/正文中的位置[ **RetrieveImageResponse** ](retrieveimageresponse.md)操作元素。 实际扫描数据追加到 SOAP 信封/正文作为二进制附件。

## <a name="see-also"></a>请参阅


[**RetrieveImageResponse**](retrieveimageresponse.md)

 

 






