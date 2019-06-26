---
title: headerPath XML 元素
description: headerPath XML 元素
ms.assetid: 9764fed5-75bc-4679-bae0-5bfe738268e2
keywords:
- headerPath XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- headerPath XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3a9b0a869b6993cae7d9494e7f542244f138abe1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386414"
---
# <a name="headerpath-xml-element"></a>headerPath XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)。\]

**HeaderPath** XML 元素指定有关 DPInst DPInst EULA 页面和 DPInst 安装页的右上角显示的自定义标头位图源文件名。

### <a name="element-tag"></a>元素标记

```cpp
<headerPath>
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
<td align="left"><p>指定的标头位图的 DPInst DPInst EULA 和安装页右上角显示的文件名的字符串。 标头位图文件必须位于 DPInst 根目录下，这是包含 DPInst 可执行文件的目录 (<em>DPInst.exe</em>)，或在 DPInst 根目录下的子目录中。 如果标头位图文件的子目录中，指定是相对于 DPInst 根目录的完全限定的文件名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>备注

一个**headerPath**自定义，但未进行本地化，如果它是子元素的元素**dpinst** XML 元素。 一个**headerPath**元素是自定义的如果它是子元素的已本地化**语言**XML 元素。

下面的代码示例演示**headerPath**指定的元素*数据\\Header.bmp*作为 DPInst 显示在右上角的 DPInst EULA 的标头位图文件和安装页和安装页中。 指定自定义标头位图文件的文本所示粗体的字体样式。

```cpp
<dpinst>
  ...
  <headerPath>Data\Header.bmp</headerPath>
  ...
</dpinst>
```

如果**headerPath**元素未指定，DPInst 将使用默认标头位图。

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

[**language**](language-xml-element.md)

 

 






