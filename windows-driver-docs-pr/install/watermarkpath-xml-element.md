---
title: watermarkPath XML 元素
description: watermarkPath XML 元素
ms.assetid: 3c64738b-4ead-4e78-a1bd-45d098a11dad
keywords:
- watermarkPath XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- watermarkPath XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 02359f3886acbad1a5c846c85ea9194fd6b81e4c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540514"
---
# <a name="watermarkpath-xml-element"></a>watermarkPath XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)。\]

**WatermarkPath**元素指定 DPInst 左侧和右侧的 DPInst 欢迎页和 DPInst 完成页显示的自定义水印位图的源文件。

### <a name="element-tag"></a>元素标记

```cpp
<watermarkPath>
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
<td align="left"><p><a href="dpinst-xml-element.md" data-raw-source="[&lt;strong&gt;dpinst&lt;/strong&gt;](dpinst-xml-element.md)"><strong>dpinst</strong> </a>或<a href="language-xml-element.md" data-raw-source="[&lt;strong&gt;language&lt;/strong&gt;](language-xml-element.md)"><strong>语言</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据的内容</strong></p></td>
<td align="left"><p>指定包含水印位图 DPInst 左侧和右侧的欢迎页和完成页上显示的文件的名称的字符串。 水印文件必须位于 DPInst 根目录下，这是包含 DPInst 可执行文件的目录 (<em>DPInst.exe</em>)，或在 DPInst 根目录下的子目录中。 如果水印位图文件的子目录中，指定是相对于 DPInst 根目录的完全限定的文件名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>备注

一个**watermarkPath**自定义，但未进行本地化，如果它是子元素的元素**dpinst**元素。 一个**watermarkPath**元素是自定义的如果它是子元素的已本地化**语言**元素。

下面的代码示例演示**watermarkPath**指定的元素*数据\\Watermark.bmp*作为 DPInst 显示在左侧和右侧的水印位图的源欢迎使用日期和完成页。 指定自定义水印位图文件的文本所示粗体的字体样式。

```cpp
<dpinst>
  ...
  <watermarkPath>Data\Watermark.bmp</watermarkPath>
  ...
</dpinst>
```

如果**watermarkPath**元素未指定，DPInst 将使用默认水印。

## <a name="see-also"></a>另请参阅


[**dpinst**](dpinst-xml-element.md)

[**language**](language-xml-element.md)

 

 






