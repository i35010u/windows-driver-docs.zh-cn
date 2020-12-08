---
title: finishText XML 元素
description: finishText XML 元素
keywords:
- finishText XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- finishText XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 11cdfcba8bcfe866b778bdbd1b5cc53ebeb3ee35
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820197"
---
# <a name="finishtext-xml-element"></a>finishText XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**FinishText** XML 元素自定义 DPInst 在 DPInst 完成页上显示的主文本。

### <a name="element-tag"></a>元素标记

```cpp
<finishText>
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
<td align="left"><p>自定义 "完成" 页上的主文本的字符串</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a name="remarks"></a><a href="" id="comments"></a>注释

下面的代码示例演示一个 **finishText** 元素，该元素自定义 DPInst 为成功安装显示的 "完成" 页上的主文本。 指定自定义完成文本的文本以粗体显示。

```cpp
dpinst>
  ...
  <language code="0x0409">
    ...
    <finishText>Enjoy using the Toaster.</finishText>
    ...
  </language>
  ...
</dpinst>
```

如果未指定 **finishText** 元素，则 DPInst 会显示默认完成文本，指示安装是成功还是失败。

## <a name="see-also"></a>请参阅


[**finishTitle**](finishtitle-xml-element.md)

[**语言**](language-xml-element.md)

 

