---
title: eulaNoButton XML 元素
description: eulaNoButton XML 元素
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
ms.openlocfilehash: d5940f2be7418e91304fd08bba5dd1ebe84a068d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830019"
---
# <a name="eulanobutton-xml-element"></a>eulaNoButton XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**EulaNoButton** XML 元素自定义与 DPInst EULA 页面上的 "不接受" 选项按钮关联的文本。

### <a name="element-tag"></a>元素标记

```cpp
<eulaNoButton>
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
<td align="left"><p>自定义与 DPInst EULA 页面上的 "不接受" 选项按钮关联的文本的字符串</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a name="remarks"></a><a href="" id="comments"></a>注释

下面的代码示例演示一个 **eulaNoButton** 元素，该元素自定义 DPInst EULA 页上 "不接受" 选项按钮的文本。 指定 "不接受" 选项按钮的自定义文本的文本以粗体显示。

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

如果未指定 **eulaNoButton** 元素，则 DPInst 将显示默认 DPInst EULA 页面上显示的默认按钮文本。

## <a name="see-also"></a>请参阅


[**协议**](eula-xml-element.md)

[**eulaYesButton**](eulayesbutton-xml-element.md)

[**语言**](language-xml-element.md)

 

