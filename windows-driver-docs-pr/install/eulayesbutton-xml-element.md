---
title: eulaYesButton XML 元素
description: eulaYesButton XML 元素
ms.assetid: 7d91d3ec-af0a-4b6a-83d8-fa14a527378b
keywords:
- eulaYesButton XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- eulaYesButton XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a275f253e87da2085fc1557ef5f5964d4dcc19b0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569042"
---
# <a name="eulayesbutton-xml-element"></a>eulaYesButton XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)。\]

**EulaYesButton** XML 元素自定义与 DPInst EULA 页上的接受选项按钮相关联的文本。

### <a name="element-tag"></a>**元素标记**

```cpp
<eulaYesButton>
```

### <a name="xml-attributes"></a>**XML 特性**

无

### <a name="element-information"></a>**元素的信息**

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
<td align="left"><p>自定义与 DPInst EULA 页上的接受选项按钮相关联的文本的字符串</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>备注

下面的代码示例演示**eulaYesButton**自定义 DPInst EULA 页面上的接受选项按钮文本的元素。 指定接受选项按钮的自定义文本的文本所示粗体的字体样式。

```cpp
<dpinst>
  ...
  <language code="0x0409">
    ...
    <eulaYesButton>I &amp;accept this EULA</eulaYesButton>
    ...
  </language>
  ...
</dpinst>
```

如果**eulaYesButton**元素未指定，DPInst 显示默认 DPInst EULA 页面显示的默认选项按钮文本。

## <a name="see-also"></a>请参阅


[**eula**](eula-xml-element.md)

[**eulaNoButton**](eulanobutton-xml-element.md)

[**language**](language-xml-element.md)

 

 






