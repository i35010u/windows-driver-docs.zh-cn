---
title: ImageInformation 元素
description: 所需的 ImageInformation 元素包含有关从与当前正在验证 ScanTicket 元素进行扫描生成的图像数据的信息。
ms.assetid: 58a5dc09-07fa-4e31-93f1-7370dace3263
keywords:
- ImageInformation 元素成像设备
topic_type:
- apiref
api_name:
- wscn ImageInformation
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2629817079e25d5787f9be7ac64098b88f93aeed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327877"
---
# <a name="imageinformation-element"></a>ImageInformation 元素


所需**ImageInformation**元素包含有关生成的图像数据的使用进行扫描的信息[ **ScanTicket** ](scanticket.md)当前正在元素验证。

<a name="usage"></a>用法
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

WSD 扫描服务将返回**ImageInformation**通过元素[ **CreateScanJobResponse** ](createscanjobresponse.md)操作元素。 扫描应用程序可以使用中指定的数据**ImageInformation**进行解码的图像文件中的图像。

## <a name="see-also"></a>请参阅


[**CreateScanJobResponse**](createscanjobresponse.md)

[**MediaBackImageInfo**](mediabackimageinfo.md)

[**MediaFrontImageInfo**](mediafrontimageinfo.md)

[**ValidationInfo**](validationinfo.md)

 

 






