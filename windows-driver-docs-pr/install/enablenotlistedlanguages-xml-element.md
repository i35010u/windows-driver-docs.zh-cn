---
title: enableNotListedLanguages XML 元素
description: EnableNotListedLanguages XML 元素是一个空元素，该元素将 enableNotListedLanguages 标志设置为 ON，这将配置 DPInst，以启用 DPInst.xml 文件中的语言 XML 元素未显式启用的所有受支持的语言。
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
ms.openlocfilehash: d59da5a4163daa3f250a2b93ea7bb2b82b6dfa92
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096059"
---
# <a name="enablenotlistedlanguages-xml-element"></a>enableNotListedLanguages XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**EnableNotListedLanguages** XML 元素是一个空元素，该元素将**enableNotListedLanguages**标志设置为 ON，这将配置 DPInst，以启用*DPInst.xml*文件中的[**语言**](language-xml-element.md)XML 元素未显式启用的所有受支持的语言。

### <a name="element-tag"></a>元素标记

```cpp
<enableNotListedLanguages>
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
<td align="left"><p><a href="dpinst-xml-element.md" data-raw-source="[&lt;strong&gt;dpinst&lt;/strong&gt;](dpinst-xml-element.md)"><strong>dpinst</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据内容</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a name="remarks"></a><a href="" id="comments"></a>注释

默认情况下，如果 *DPInst.xml* 文件不包含任何 **语言** 元素，则会启用所有支持 DPInst 的语言。 但是，如果 *DPInst.xml* 文件包含 **语言** 元素，则只会启用 **语言** 元素显式指定的语言，并隐式禁用所有其他语言。 若要启用隐式禁用的所有语言，请将**enableNotListedLanguages**元素包含为**dpinst** XML 元素的子元素，或使用 **/el**命令行开关，将**enableNotListedLanguages**标志设置为 ON   。

下面的代码示例演示了 **enableNotListedLanguages** 元素。

```cpp
<dpinst>
  ...
  <enableNotListedLanguages/>
  ...
</dpinst>
```

## <a name="see-also"></a>另请参阅


[**dpinst**](dpinst-xml-element.md)

 

