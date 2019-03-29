---
title: finishText XML 元素
description: finishText XML 元素
ms.assetid: b8c63f75-e0d3-458f-9265-a19d6f64ac6b
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
ms.openlocfilehash: 40d0d7d4b1093e6d4d38f7baf2c5cff1e346b9e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576216"
---
# <a name="finishtext-xml-element"></a>finishText XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)。\]

**FinishText** XML 元素自定义 DPInst DPInst 完成页显示的主文本。

### <a name="element-tag"></a>元素标记

```cpp
<finishText>
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
<td align="left"><p>自定义完成页上的主文本的字符串</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>备注

下面的代码示例演示**finishText**自定义 DPInst 显示成功安装的完成页面上的主文本的元素。 指定自定义完成文本的文本所示粗体的字体样式。

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

如果**finishText**元素未指定，DPInst 显示默认完成文本指示安装是否成功或失败。

## <a name="see-also"></a>请参阅


[**finishTitle**](finishtitle-xml-element.md)

[**language**](language-xml-element.md)

 

 






