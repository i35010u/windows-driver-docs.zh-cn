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
ms.openlocfilehash: 65b1bf3a9f48f417d84df6ba79427b29cd503eed
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095369"
---
# <a name="eulaheadertitle-xml-element"></a>eulaHeaderTitle XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**EulaHeaderTitle** XML 元素自定义 eula 标题标题的文本，该文本直接显示在 DPInst EULA 页上的标题栏的下方。

### <a name="element-tag"></a>元素标记

```cpp
<eulaHeaderTitle>
```

### <a name="xml-attributes"></a>XML 属性

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
<td align="left"><p><a href="language-xml-element.md" data-raw-source="[&lt;strong&gt;language&lt;/strong&gt;](language-xml-element.md)"><strong>语言</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据内容</strong></p></td>
<td align="left"><p>自定义 DPInst EULA 页上的标题的字符串</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a name="remarks"></a><a href="" id="comments"></a>注释

下面的代码示例演示一个自定义 DPInst EULA 页面标题标题的 **eulaHeaderTitle** 元素。 指定自定义标题标题的文本以粗体显示。

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

如果未指定 **eulaHeaderTitle** 元素，则 DPInst 将显示默认 DPInst eula 页面上显示的默认 EULA 标题标题。

## <a name="see-also"></a>另请参阅


[**语言**](language-xml-element.md)

 

