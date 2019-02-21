---
title: NumberOfLines 元素
description: 所需的 NumberOfLines 元素描述的确切的高度，以像素为单位，最终输出图像。
ms.assetid: 9f7f96d4-fd88-4d14-b000-7abefe96775f
keywords:
- NumberOfLines 元素成像设备
topic_type:
- apiref
api_name:
- wscn NumberOfLines
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 519cacdacbfc62c1c8bbb7be60111b5ddb47d53a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542526"
---
# <a name="numberoflines-element"></a>NumberOfLines 元素


所需**NumberOfLines**元素描述的确切的高度，以像素为单位，最终输出图像。

<a name="usage"></a>用法
-----

```xml
<wscn:NumberOfLines>
  text
</wscn:NumberOfLines>
```

<a name="attributes"></a>属性
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

指定的值说明了确切的高度，以像素为单位或行，将为当前生成的最终输出映像数[ **ScanTicket** ](scanticket.md)要验证的设置。 此高度包括旋转和扫描程序可能再传输到客户端扫描图像执行任何调整。

## <a name="see-also"></a>另请参阅


[**MediaBackImageInfo**](mediabackimageinfo.md)

[**MediaFrontImageInfo**](mediafrontimageinfo.md)

[**ScanTicket**](scanticket.md)

 

 






