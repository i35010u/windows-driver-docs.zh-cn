---
title: eulaHeaderTitle XML 元素
description: eulaHeaderTitle XML 元素
ms.assetid: 65b8e793-ed7b-4d2c-8a55-9860e6188b77
keywords:
- eulaHeaderTitle XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- eulaHeaderTitle XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d7bc2abd4800c7deeb55604ca868f8026dad976a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380280"
---
# <a name="eulaheadertitle-xml-element"></a>eulaHeaderTitle XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)。\]

**EulaHeaderTitle** XML 元素自定义 DPInst EULA 页面上的标题栏下方直接显示的最终用户许可协议标头标题的文本。

### <a name="element-tag"></a>元素标记

```cpp
<eulaHeaderTitle>
```

### <a name="xml-attributes"></a>XML 特性

无

### <a name="element-information"></a>元素信息

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>父元素</strong></p></td>
<td align="left"><p><a href="language-xml-element.md" data-raw-source="[&lt;strong&gt;language&lt;/strong&gt;](language-xml-element.md)"><strong>language</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据的内容</strong></p></td>
<td align="left"><p>自定义 DPInst EULA 页面上的标题的字符串</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>备注

下面的代码示例演示**eulaHeaderTitle**自定义标头标题的 DPInst EULA 页面的元素。 指定自定义标头标题的文本所示粗体的字体样式。

```cpp
<dpinst>
  ...
  <language code="0x0409">
    . . .
    <eulaHeaderTitle>End User License Agreement</eulaHeaderTitle>
    . . .
  </language>
  ...
</dpinst>
```

如果**eulaHeaderTitle**元素未指定，DPInst 显示默认默认 DPInst EULA 页面显示的最终用户许可协议标头标题。

## <a name="see-also"></a>请参阅


[**language**](language-xml-element.md)

 

 






