---
title: NumberOfLines 元素
description: 必需的 NumberOfLines 元素描述最终输出图像的准确高度（以像素为单位）。
keywords:
- NumberOfLines 元素图像设备
topic_type:
- apiref
api_name:
- wscn NumberOfLines
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc56d5e0a82eeadecb0bb91b4acd80fb79f45748
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829639"
---
# <a name="numberoflines-element"></a>NumberOfLines 元素


必需的 **NumberOfLines** 元素描述最终输出图像的准确高度（以像素为单位）。

<a name="usage"></a>使用情况
-----

```xml
<wscn:NumberOfLines>
  text
</wscn:NumberOfLines>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 介于1到2147483647之间的整数值。

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
<td><p><a href="mediabackimageinfo.md" data-raw-source="[&lt;strong&gt;MediaBackImageInfo&lt;/strong&gt;](mediabackimageinfo.md)"><strong>MediaBackImageInfo</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="mediafrontimageinfo.md" data-raw-source="[&lt;strong&gt;MediaFrontImageInfo&lt;/strong&gt;](mediafrontimageinfo.md)"><strong>MediaFrontImageInfo</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

指定的值描述最终输出图像的准确高度（以像素为单位）或行数，将为正在验证的当前 [**ScanTicket**](scanticket.md) 设置生成该输出图像。 此高度包括旋转以及扫描程序在将扫描图像传输到客户端之前可能会对其执行的任何调整。

## <a name="see-also"></a>请参阅


[**MediaBackImageInfo**](mediabackimageinfo.md)

[**MediaFrontImageInfo**](mediafrontimageinfo.md)

[**ScanTicket**](scanticket.md)

 

 






