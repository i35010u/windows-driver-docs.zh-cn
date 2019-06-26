---
title: finishTitle XML 元素
description: finishTitle XML 元素
ms.assetid: d8730b49-9cc0-46f4-88a1-fd5543063277
keywords:
- finishTitle XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- finishTitle XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3d8580cc4ac00744c39de0c1f24d2493b7fd9a3d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360303"
---
# <a name="finishtitle-xml-element"></a>finishTitle XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)。\]

**FinishTitle** XML 元素自定义显示在 DPInst 完成页顶部的完成标题的文本。

### <a name="element-tag"></a>**元素标记**

```cpp
<finishTitle>
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
<td align="left"><p>自定义完成页顶部的标题文本的字符串。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>备注

下面的代码示例演示**finishTitle**自定义完成页顶部的标题文本的元素。 指定的自定义标题文本的文本所示粗体的字体样式。

```cpp
dpinst>
  ...
  <language code="0x0409">
    ...
    <finishTitle>Congratulations! You are finished installing your Toaster device.</finishTitle>
    ...
  </language>
  ...
</dpinst>
```

如果**finishTitle**元素未指定，DPInst 显示默认值完成页显示的默认标题文本。

## <a name="see-also"></a>请参阅


[**finishText**](finishtext-xml-element.md)

[**language**](language-xml-element.md)

 

 






