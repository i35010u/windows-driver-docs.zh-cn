---
title: 最终用户许可协议的 XML 元素
description: 最终用户许可协议的 XML 元素
ms.assetid: ab647583-b0e1-4f40-86af-9b7923f5535c
keywords:
- 最终用户许可协议 XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- eula XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 09533b410f89ef9461e45f120373be7859b33cd8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525727"
---
# <a name="eula-xml-element"></a>最终用户许可协议的 XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)。\]

**Eula** XML 元素是否包含指定包含自定义文本 DPInst EULA 页面的最终用户许可协议文本文件的两个属性的空 XML 元素。

### <a name="element-tag"></a>元素标记

```cpp
<eula>
```

### <a name="xml-attributes"></a>XML 特性

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Type</strong></p></td>
<td align="left"><p>供应商提供最终用户许可协议的类型。 此属性的值必须设置为字符串&quot;txt&quot;，指示一个纯文本文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Path</strong></p></td>
<td align="left"><p>一个字符串，标识包含 DPInst EULA 页面的文本的文件的名称。 最终用户许可协议文本文件必须使用 utf-8 编码进行编码。 EULA 文件必须位于 DPInst 根目录下，这是包含 DPInst 可执行文件的目录 (<em>DPInst.exe</em>)，或 DPInst 根目录下的子目录。 如果 EULA 文件的子目录中，指定是相对于 DPInst 根目录的完全限定的文件名。</p></td>
</tr>
</tbody>
</table>

 

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
<td align="left"><p>不允许</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>备注

下面的代码示例演示**eula**指定的元素*数据\\Eula409.txt*包含自定义最终用户许可协议文本。 *Eula409.txt*文件位于*数据*目录中，它必须是 DPInst 根目录下的子目录。 下面指定的自定义 EULA 文件的文本是使用&lt;eula&gt;标记。

```cpp
<dpinst>
  ...
  <language code="0x0409">
    ...
    <eula type="txt" path="Data\Eula409.txt"/>
    ...
  </language>
  ...
</dpinst>
```

## <a name="see-also"></a>另请参阅


[**language**](language-xml-element.md)

 

 






