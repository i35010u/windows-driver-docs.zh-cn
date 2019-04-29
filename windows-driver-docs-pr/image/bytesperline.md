---
title: BytesPerLine 元素
description: 所需的 BytesPerLine 元素生成的图像文件中指定每个扫描行的字节的数。
ms.assetid: 026187db-16b7-48fc-a9e4-fa32cdc73d98
keywords:
- BytesPerLine 元素成像设备
topic_type:
- apiref
api_name:
- wscn BytesPerLine
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a80f6388de8c74bf8c66b8ac7b2d8329c4f2d4f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373304"
---
# <a name="bytesperline-element"></a>BytesPerLine 元素


所需**BytesPerLine**元素生成的图像文件中指定的每个扫描行的字节数。

<a name="usage"></a>用法
-----

```xml
<wscn:BytesPerLine>
  text
</wscn:BytesPerLine>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 介于 0 到 2147483647 之间的整数值。

## <a name="child-elements"></a>子元素


没有子元素。

## <a name="parent-elements"></a>父元素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mediabackimageinfo.md" data-raw-source="[&lt;strong&gt;MediaBackImageInfo&lt;/strong&gt;](mediabackimageinfo.md)"><strong>MediaBackImageInfo</strong></a></p></td>
<td><p></p>
<p>MediaBackImageInfo</p></td>
</tr>
<tr class="even">
<td><p><a href="mediafrontimageinfo.md" data-raw-source="[&lt;strong&gt;MediaFrontImageInfo&lt;/strong&gt;](mediafrontimageinfo.md)"><strong>MediaFrontImageInfo</strong></a></p></td>
<td><p></p>
<p>MediaFrontImageInfo</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

WSD 扫描服务返回的整数值是数据像素和扫描程序会将添加到每个扫描行的任何填充所需的总字节数。

[**Format**](format.md)

**BytesPerLine**元素无效，仅当请求[**格式**](format.md)值是未压缩的文件格式。 如果文件格式指示压缩，扫描服务必须返回值为零**BytesPerLine**。

## <a name="see-also"></a>请参阅


[**Format**](format.md)

[**MediaBackImageInfo**](mediabackimageinfo.md)

[**MediaFrontImageInfo**](mediafrontimageinfo.md)

 

 






