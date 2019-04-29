---
title: PixelsPerLine 元素
description: 所需的 PixelsPerLine 元素描述的确切宽度，以像素为单位，最终输出图像。
ms.assetid: aad46ca7-025e-4f50-9bc5-7f584a7bf684
keywords:
- PixelsPerLine 元素成像设备
topic_type:
- apiref
api_name:
- wscn PixelsPerLine
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: beb284b4f16157c775febd4ede0838f122f43f81
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375853"
---
# <a name="pixelsperline-element"></a>PixelsPerLine 元素


所需**PixelsPerLine**元素描述的确切宽度，以像素为单位，最终输出图像。

<a name="usage"></a>用法
-----

```xml
<wscn:PixelsPerLine>
  text
</wscn:PixelsPerLine>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 一个从 1 到 2147483647 范围内的整数值。

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
<td><p><a href="mediabackimageinfo.md" data-raw-source="[&lt;strong&gt;MediaBackImageInfo&lt;/strong&gt;](mediabackimageinfo.md)"><strong>MediaBackImageInfo</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="mediafrontimageinfo.md" data-raw-source="[&lt;strong&gt;MediaFrontImageInfo&lt;/strong&gt;](mediafrontimageinfo.md)"><strong>MediaFrontImageInfo</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

指定的值说明了确切宽度 （像素），将使用当前生成的最终输出图像[ **ScanTicket** ](scanticket.md)要验证的设置。 此宽度包括旋转和扫描程序可能再传输到客户端扫描图像执行任何调整。

## <a name="see-also"></a>请参阅


[**MediaBackImageInfo**](mediabackimageinfo.md)

[**MediaFrontImageInfo**](mediafrontimageinfo.md)

[**ScanTicket**](scanticket.md)

 

 






