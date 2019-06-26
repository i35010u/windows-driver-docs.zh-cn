---
title: eulaNoButton XML 元素
description: eulaNoButton XML 元素
ms.assetid: d3e47943-10c6-4a87-b39e-d13fc49aadd4
keywords:
- eulaNoButton XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- eulaNoButton XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3814050045d847fb9aea604baa52e6351470f815
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364093"
---
# <a name="eulanobutton-xml-element"></a>eulaNoButton XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)。\]

**EulaNoButton** XML 元素自定义与 DPInst EULA 页上的 do not 接受选项按钮关联的文本。

### <a name="element-tag"></a>元素标记

```cpp
<eulaNoButton>
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
<td align="left"><p>自定义与 DPInst EULA 页上的 do not 接受选项按钮关联的文本的字符串</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>备注

下面的代码示例演示**eulaNoButton**自定义 DPInst EULA 页上的 do not 接受选项按钮的文本的元素。 指定不接受选项按钮的自定义文本的文本所示粗体的字体样式。

```cpp
<dpinst>
  ...
  <language code="0x0409">
    ...
    <eulaNoButton>I do n&ot accept this EULA</eulaNoButton>
    ...
  </language>
  ...
</dpinst>
```

如果**eulaNoButton**元素未指定，DPInst 显示默认 DPInst EULA 页面显示的默认按钮文本。

## <a name="see-also"></a>请参阅


[**eula**](eula-xml-element.md)

[**eulaYesButton**](eulayesbutton-xml-element.md)

[**language**](language-xml-element.md)

 

 






