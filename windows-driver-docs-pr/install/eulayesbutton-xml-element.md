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
ms.openlocfilehash: 3be0874c97881b9669c65ec62845ba08f01f292c
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095357"
---
# <a name="eulayesbutton-xml-element"></a>eulaYesButton XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**EulaYesButton** XML 元素自定义与 DPInst EULA 页面上的 "接受" 选项按钮关联的文本。

### <a name="element-tag"></a>**元素标记**

```cpp
<eulaYesButton>
```

### <a name="xml-attributes"></a>**XML 特性**

无

### <a name="element-information"></a>**元素信息**

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
<td align="left"><p>自定义与 DPInst EULA 页面上 "接受" 选项按钮关联的文本的字符串</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a name="remarks"></a><a href="" id="comments"></a>注释

下面的代码示例演示了自定义 DPInst EULA 页面上的 "接受" 选项按钮文本的 **eulaYesButton** 元素。 指定 "接受" 选项按钮的自定义文本的文本以粗体显示。

```cpp
<dpinst>
  ...
  <language code="0x0409">
    ...
    <eulaYesButton>I &accept this EULA</eulaYesButton>
    ...
  </language>
  ...
</dpinst>
```

如果未指定 **eulaYesButton** 元素，则 DPInst 将显示默认 DPInst EULA 页上显示的默认选项按钮文本。

## <a name="see-also"></a>另请参阅


[**协议**](eula-xml-element.md)

[**eulaNoButton**](eulanobutton-xml-element.md)

[**语言**](language-xml-element.md)

 

