---
title: BytesPerLine 元素
description: 必需的 BytesPerLine 元素指定生成的图像文件中每个扫描行的字节数。
keywords:
- BytesPerLine 元素图像设备
topic_type:
- apiref
api_name:
- wscn BytesPerLine
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d70898350b00251356332e356c3bcc2c78c7ed0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804177"
---
# <a name="bytesperline-element"></a>BytesPerLine 元素


必需的 **BytesPerLine** 元素指定生成的图像文件中每个扫描行的字节数。

<a name="usage"></a>使用情况
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

必需。 0到2147483647之间的整数值。

## <a name="child-elements"></a>子元素


没有任何子元素。

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

WSD 扫描服务返回的整数值是数据像素和扫描程序将添加到每个扫描行的任何空白所需的总字节数。

[**形式**](format.md)

仅当请求的 [**格式**](format.md)值为未压缩的文件格式时， **BytesPerLine** 元素才有效。 如果文件格式指示压缩，则扫描服务必须将 **BytesPerLine** 的值返回为零。

## <a name="see-also"></a>请参阅


[**形式**](format.md)

[**MediaBackImageInfo**](mediabackimageinfo.md)

[**MediaFrontImageInfo**](mediafrontimageinfo.md)

 

 






