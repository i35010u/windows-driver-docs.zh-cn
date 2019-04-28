---
title: enableNotListedLanguages XML 元素
description: EnableNotListedLanguages XML 元素是空元素，用于 enableNotListedLanguages 标志设置为 ON，将配置 DPInst 若要启用的所有受支持的语言 XML 元素 DPInst.xml 文件中未显式启用的语言。
ms.assetid: 7584b222-71b0-4532-84be-3444a4a7003b
keywords:
- enableNotListedLanguages XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- enableNotListedLanguages XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9aeed2c3718fc679de8b72f52ce705a1dc914779
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346152"
---
# <a name="enablenotlistedlanguages-xml-element"></a>enableNotListedLanguages XML 元素


\[DIFx 已被弃用，有关详细信息，请参阅[DIFx 准则](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)。\]

**EnableNotListedLanguages** XML 元素为空元素，用于设置**enableNotListedLanguages**标志为 ON，将配置 DPInst 若要启用的所有不受支持语言通过显式启用[**语言**](language-xml-element.md)中的 XML 元素*DPInst.xml*文件。

### <a name="element-tag"></a>元素标记

```cpp
<enableNotListedLanguages>
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
<td align="left"><p><a href="dpinst-xml-element.md" data-raw-source="[&lt;strong&gt;dpinst&lt;/strong&gt;](dpinst-xml-element.md)"><strong>dpinst</strong></a></p></td>
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

默认情况下，所有的 DPInst 支持的语言均启用如果*DPInst.xml*文件不包含任何**语言**元素。 但是，如果*DPInst.xml*文件包含**语言**元素，只能通过显式指定的语言**语言**之外的元素及其所有隐式禁用了其他语言。 若要启用的所有隐式禁用了语言，请设置**enableNotListedLanguages**通过包括标志为 ON **enableNotListedLanguages**元素的子元素作为**dpinst** XML 元素，或使用 **/el** 命令行开关。

下面的代码示例演示**enableNotListedLanguages**元素。

```cpp
<dpinst>
  ...
  <enableNotListedLanguages/>
  ...
</dpinst>
```

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

 

 






