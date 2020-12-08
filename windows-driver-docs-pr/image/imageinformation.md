---
title: ImageInformation 元素
description: 必需的 ImageInformation 元素包含有关通过使用当前正在验证的 ScanTicket 元素进行的扫描所产生的图像数据的信息。
keywords:
- ImageInformation 元素图像设备
topic_type:
- apiref
api_name:
- wscn ImageInformation
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c6aa35b9baa4c2c7ba664469eb18320664d9b00
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808205"
---
# <a name="imageinformation-element"></a>ImageInformation 元素


必需的 **ImageInformation** 元素包含有关通过使用当前正在验证的 [**ScanTicket**](scanticket.md) 元素进行的扫描所产生的图像数据的信息。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ImageInformation>
  child elements
</wscn:ImageInformation>
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
<td><p><a href="mediabackimageinfo.md" data-raw-source="[&lt;strong&gt;MediaBackImageInfo&lt;/strong&gt;](mediabackimageinfo.md)"><strong>MediaBackImageInfo</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="mediafrontimageinfo.md" data-raw-source="[&lt;strong&gt;MediaFrontImageInfo&lt;/strong&gt;](mediafrontimageinfo.md)"><strong>MediaFrontImageInfo</strong></a></p></td>
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
<td><p><a href="createscanjobresponse.md" data-raw-source="[&lt;strong&gt;CreateScanJobResponse&lt;/strong&gt;](createscanjobresponse.md)"><strong>CreateScanJobResponse</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="validationinfo.md" data-raw-source="[&lt;strong&gt;ValidationInfo&lt;/strong&gt;](validationinfo.md)"><strong>ValidationInfo</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

WSD 扫描服务通过 [**CreateScanJobResponse**](createscanjobresponse.md)操作元素返回 **ImageInformation** 元素。 扫描应用程序可以使用 **ImageInformation** 中指定的数据对图像文件中的图像进行解码。

## <a name="see-also"></a>请参阅


[**CreateScanJobResponse**](createscanjobresponse.md)

[**MediaBackImageInfo**](mediabackimageinfo.md)

[**MediaFrontImageInfo**](mediafrontimageinfo.md)

[**ValidationInfo**](validationinfo.md)

 

 






